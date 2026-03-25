# 'mini.test'를 이용한 테스트 방법

Neovim Lua 플러그인을 위한 테스트를 작성하는 것은 어렵습니다. 좋은 테스트를 작성하는 것은 더더욱 어렵습니다. 'mini.test' 모듈은 많은 유연성을 허용하면서도 테스트 작성을 합리적으로 쉽게 만들 수 있도록 설계되었습니다. 이 모듈은 [nvim-lua/plenary.nvim](https://github.com/nvim-lua/plenary.nvim) ([Olivine-Labs/busted](https://github.com/Olivine-Labs/busted)의 "busted 스타일 테스트")의 "사람이 읽기 쉬운 DSL 스타일" 접근 방식과는 반대로, 보다 장황하고 프로그램적인 스타일의 테스트 작성을 의도적으로 선호합니다. 물론 후자의 방식도 가능합니다.

이 파일은 예제를 통해 'mini.test'를 실습하며 소개하는 가이드입니다. 더 자세한 내용은 [문서](doc/mini-test.txt)와 이 플러그인 모듈들의 테스트 코드를 참조하세요.

테스트 파일 작성의 일반적인 접근 방식:

- 테스트를 별도의 Lua 파일로 구성합니다.
- 각 파일은 테스트 세트(test set) 테이블(`MiniTest.new_set()`의 출력)과 연결되어야 합니다. 권장되는 방식은 각 테스트 파일에서 이를 수동으로 생성한 다음 반환하는 것입니다.
- 각 테스트 액션은 테스트 세트의 항목에 할당된 별도의 함수로 정의되어야 합니다.
- 테스트 액션 내부에서 실제 테스트를 수행하기 위해 커스텀 Neovim 프로세스를 사용하는 것을 강력히 권장합니다. [자식 프로세스 사용하기](#using-child-process)를 참조하세요.

**참고**:

- 모든 명령은 Neovim 플러그인 프로젝트의 루트 디렉터리를 현재 작업 디렉터리로 하여 실행된다고 가정합니다. 이는 쉘 명령과 Neovim 명령 모두에 해당합니다.
- 모든 경로는 현재 작업 디렉터리에 대한 상대 경로라고 가정합니다.

## 예제 플러그인

이 파일에서는 (기본적인 개념을 소개한 후) 'hello_lines' 플러그인을 테스트할 것입니다. 이 플러그인은 'lua/hello_lines/init.lua'라는 단일 파일에 구현되어 있으며, 줄 앞에 'Hello ' 접두사를 추가하는 기능을 가집니다.

<details><summary>'lua/hello_lines/init.lua'</summary>

```lua
local M = {}

--- 모든 요소 앞에 'Hello '를 추가
---@param lines table 배열. 기본값: { 'world' }.
---@return table 문자열 배열.
M.compute = function(lines)
  lines = lines or { 'world' }
  return vim.tbl_map(function(x) return 'Hello ' .. tostring(x) end, lines)
end

local ns_id = vim.api.nvim_create_namespace('hello_lines')

--- 하이라이트된 'Hello ' 접두사와 함께 줄을 설정
---@param buf_id number 줄을 설정할 버퍼 핸들. 기본값: 0.
---@param lines table 배열. 기본값: { 'world' }.
M.set_lines = function(buf_id, lines)
  buf_id = buf_id or 0
  lines = lines or { 'world' }
  vim.api.nvim_buf_clear_namespace(buf_id, ns_id, 0, -1)
  vim.api.nvim_buf_set_lines(buf_id or 0, 0, -1, true, M.compute(lines))
  for i = 1, #lines do
    local extmark_opts = { end_row = i - 1, end_col = 5, hl_group = 'Special' }
    vim.api.nvim_buf_set_extmark(buf_id, ns_id, i - 1, 0, extmark_opts)
  end
end

return M
```

</details>

## 빠른 데모

다음은 'mini.test'를 이용한 테스트가 어떻게 보이는지에 대한 빠른 데모입니다:

<details><summary>'tests/test_hello_lines.lua'</summary>

```lua
-- 도우미 별칭 정의
local new_set = MiniTest.new_set
local expect, eq = MiniTest.expect, MiniTest.expect.equality

-- 자식 Neovim 객체 생성 (시작은 하지 않음)
local child = MiniTest.new_child_neovim()

-- 이 파일의 메인 테스트 세트 정의
local T = new_set({
  -- 후크(hooks) 등록
  hooks = {
    -- 모든 (중첩된 경우 포함) 케이스 실행 전에 실행됨
    pre_case = function()
      -- 커스텀 'init.lua' 스크립트로 자식 프로세스 재시작
      child.restart({ '-u', 'scripts/minimal_init.lua' })
      -- 테스트할 플러그인 로드
      child.lua([[M = require('hello_lines')]])
    end,
    -- 이 세트의 모든 테스트가 완료된 후 한 번 실행됨
    post_once = child.stop,
  },
})

-- 테스트 세트 필드는 중첩된 구조를 정의할 수 있음
T['compute()'] = new_set()

-- 테스트 액션을 테스트 세트의 호출 가능한 필드로 정의.
-- 에러가 발생하면 테스트는 실패함.
T['compute()']['works'] = function()
  -- 자식 프로세스 내부에서 Lua 코드를 실행하고, 결과를 가져와 
  -- 기대하는 결과와 비교함
  eq(child.lua_get([[M.compute({'a', 'b'})]]), { 'Hello a', 'Hello b' })
end

T['compute()']['uses correct defaults'] = function()
  eq(child.lua_get([[M.compute()]]), { 'Hello world' })
end

-- 파라미터화된 테스트 만들기. 각 케이스에 대해 세 개의 복사본이 생성됨
T['set_lines()'] = new_set({ parametrize = { {}, { 0, { 'a' } }, { 0, { 1, 2, 3 } } } })

-- 테스트 파라미터화의 인자 사용
T['set_lines()']['works'] = function(buf_id, lines)
  -- 더 나은 테스트를 위해 일부 옵션을 직접 수정
  child.o.lines, child.o.columns = 10, 20
  child.bo.readonly = false

  -- 값을 반환하지 않고 Lua 코드 실행
  child.lua('M.set_lines(...)', { buf_id, lines })

  -- 화면 상태 테스트. 첫 실행 시 미리 정의된 위치에 텍스트 및 외관 정보가 
  -- 담긴 참조용 스크린샷을 자동으로 생성함. 이후 실행 시 현재 스크린샷을 
  -- 참조용과 비교함. 정확히 일치하지 않으면 도움이 되는 정보와 함께 에러를 발생시킴.
  expect.reference_screenshot(child.get_screenshot())
end

-- 수집되어 `MiniTest.run()` 내부에서 실행될 테스트 세트를 반환
return T
```

</details>

## 파일 구성

처음에는 조금 벅차게 느껴질 수 있습니다. 사실 대부분의 사람들이 그렇게 느낍니다. 하지만 한 번만 제대로 설정해 두면 그 이후에는 거의 건드릴 필요가 없습니다.

'hello_lines' 플러그인을 테스트하는 데 사용되는 전체 파일 구조 개요:

```
.
├── deps
│   └── mini.nvim # 필수
├── lua
│   └── hello_lines
│       └── init.lua # 필수
├── Makefile # 권장
├── scripts
│   ├── minimal_init.lua # 필수
│   └── minitest.lua # 권장
└── tests
    └── test_hello_lines.lua # 필수
```

테스트를 작성하려면 다음 파일들이 필요합니다:

필수 사항:

- **'lua' 디렉터리에 있는 여러분의 Lua 플러그인**. 여기서는 'hello_lines' 플러그인을 테스트할 것입니다.

- **테스트 파일**. 기본적으로 'tests/' 디렉터리에 위치하며 'test_' 접두사가 붙은 Lua 파일이어야 합니다. 예를 들어, 모든 내용을 'test_hello_lines.lua'에 작성할 것입니다. 일반적으로 다음 템플릿을 따르는 것이 좋습니다 (이 파일의 나머지 부분에서도 이를 가정합니다):

    <details><summary>테스트 파일용 템플릿</summary>

    ```lua
    local new_set = MiniTest.new_set
    local expect, eq = MiniTest.expect, MiniTest.expect.equality

    local T = new_set()

    -- 실제 테스트 정의가 여기에 위치함

    return T
    ```

    </details>

- **'mini.nvim' 의존성**. 'mini.test' 모듈을 사용하는 데 필요합니다. 이를 'deps/mini.nvim' 디렉터리에 저장하는 방식을 제안합니다. `git`을 사용하여 생성하세요:

    ```bash
    mkdir -p deps
    git clone --filter=blob:none https://github.com/nvim-mini/mini.nvim deps/mini.nvim
    ```

- **수동 Neovim 시작 파일** (일명 'init.lua'). 'scripts/minimal_init.lua' 경로를 권장합니다. Neovim 프로세스가 테스트할 플러그인과 'mini.nvim' 의존성을 인식할 수 있도록 하는 데 사용됩니다. 제안되는 최소 내용:

    <details><summary>'scripts/minimal_init.lua'</summary>

    ```lua
    -- 'lua' 파일을 사용할 수 있도록 현재 디렉터리를 'runtimepath'에 추가
    vim.cmd([[let &rtp.=','.getcwd()]])

    -- 헤드리스 Neovim을 호출할 때만 'mini.test' 설정 (예: `make test`)
    if #vim.api.nvim_list_uis() == 0 then
      -- 'mini.test'를 사용할 수 있도록 'mini.nvim'을 'runtimepath'에 추가
      -- 'mini.nvim'이 'deps/mini.nvim'에 저장되어 있다고 가정
      vim.cmd('set rtp+=deps/mini.nvim')

      -- 'mini.test' 설정
      require('mini.test').setup()
    end
    ```

    </details>

권장 사항:

- **Makefile**. 쉘이나 지속적 통합(CI) 서비스(예: Github Actions)에서 테스트 실행을 간소화하기 위해 Makefile을 정의하는 것이 좋습니다. 테스트 실행 단계를 정의합니다. 제안되는 템플릿:

    <details><summary>Makefile 템플릿</summary>

    ```
    # 모든 테스트 파일 실행
    test: deps/mini.nvim
    	nvim --headless --noplugin -u ./scripts/minimal_init.lua -c "lua MiniTest.run()"

    # `$FILE` 환경 변수에 지정된 테스트 파일 실행
    test_file: deps/mini.nvim
    	nvim --headless --noplugin -u ./scripts/minimal_init.lua -c "lua MiniTest.run_file('$(FILE)')"

    # 'mini.test' 테스트 모듈을 사용하기 위해 'mini.nvim' 다운로드
    deps/mini.nvim:
    	@mkdir -p deps
    	git clone --filter=blob:none https://github.com/nvim-mini/mini.nvim $@
    ```

    </details>

- **'scripts/minitest.lua'에 있는 'mini.test' 스크립트**. 무엇을(어떤 파일 등), 어떻게 테스트할지 커스터마이징하는 데 사용합니다. 보통은 필요하지 않지만, 필요한 경우 `MiniTest.run()` 호출의 변형을 포함해야 합니다.

## 테스트 실행

'mini.test' 모듈은 기본적으로 두 가지 주요 테스트 실행 방식을 지원합니다:

- **대화형 (Interactive)**. 모든 테스트 파일이 현재 Neovim 세션 내에서 직접 실행됩니다. 이는 테스트를 작성하면서 디버깅하는 데 매우 유용합니다. 테스트를 실행하려면 단순히 `:lua MiniTest.run()` / `:lua MiniTest.run_file()` / `:lua MiniTest.run_at_location()`을 실행하면 됩니다 (이미 `require('mini.test').setup()`으로 'mini.test'가 설정되어 있다고 가정함). 기본 설정으로는 테스트 실행 결과 정보가 담긴 플로팅 윈도우가 나타납니다. `q`를 눌러 닫을 수 있습니다. **참고**: 현재 설정에 영향을 줄 수 있으므로 주의해야 합니다. 이를 피하려면 테스트 내부에서 [자식 프로세스를 사용](#using-child-process)하세요.
- **헤드리스 (Headless)** (쉘에서 실행). 적절한 시작 파일과 함께 헤드리스 Neovim 프로세스를 시작하고 `lua MiniTest.run()`을 실행합니다. 이전 섹션의 전체 파일 구성을 따랐다면 `make test`로 이를 수행할 수 있습니다. 테스트 실행 결과 정보가 쉘에 직접 표시됩니다.

## 기초

다음 섹션들에서는 'mini.test'의 기본적인 기능들과 사용 방법을 보여줍니다. 모든 예제 코드 블록은 하나의 전체 테스트 파일(예: 'tests/test_basics.lua')을 나타냅니다.

### 첫 번째 테스트

테스트는 테스트 세트의 필드에 할당된 함수로 정의됩니다. 에러가 발생하면 테스트는 실패한 것입니다. 테스트 파일은 단일 테스트 세트를 반환해야 합니다. 예시는 다음과 같습니다:

```lua
local T = MiniTest.new_set()

T['works'] = function()
  local x = 1 + 1
  if x ~= 2 then
    error('`x`가 2와 같지 않습니다')
  end
end

return T
```

`if .. error() .. end`를 작성하는 것은 너무 번거롭습니다. 그래서 'mini.test'는 매우 최소한이지만 보통 충분한 *기대치(expectations)* 세트인 `MiniTest.expect`를 제공합니다. 이는 객체 간의 의도된 기대를 표시하며, 성립하지 않을 경우 정보가 담긴 메시지와 함께 에러를 발생시킵니다. 이전 예제를 다시 작성하면 다음과 같습니다:

```lua
local T = MiniTest.new_set()

T['works'] = function()
  local x = 1 + 1
  MiniTest.expect.equality(x, 2)
end

return T
```

테스트 세트는 중첩될 수 있습니다. 이는 [후크(hooks)](#hooks) 및 [파라미터화](#test-parametrization)와 결합하여 유용하게 쓰입니다:

```lua
local T = MiniTest.new_set()

T['big scope'] = new_set()

T['big scope']['works'] = function()
  local x = 1 + 1
  MiniTest.expect.equality(x, 2)
end

T['big scope']['also works'] = function()
  local x = 2 + 2
  MiniTest.expect.equality(x, 4)
end

T['out of scope'] = function()
  local x = 3 + 3
  MiniTest.expect.equality(x, 6)
end

return T
```

**참고**: 'mini.test'는 기본적으로 busted 스타일 테스트의 에뮬레이션을 지원합니다. 따라서 이전 예제는 다음과 같이 작성할 수도 있습니다:

```lua
describe('big scope', function()
  it('works', function()
    local x = 1 + 1
    MiniTest.expect.equality(x, 2)
  end)

  it('also works', function()
    local x = 2 + 2
    MiniTest.expect.equality(x, 4)
  end)
end)

it('out of scope', function()
  local x = 3 + 3
  MiniTest.expect.equality(x, 6)
end)

-- 참고: 이 스타일을 사용할 때는 테스트 세트를 반환하지 않아도 됩니다
```

이 방식도 가능하지만, 이 파일의 나머지 부분에서는 권장되는 테스트 세트 접근 방식을 사용할 것입니다.

### 내장 기대치 (Builtin expectations)

가장 흔히 사용되는 네 가지 내장 기대치입니다:

```lua
local T = MiniTest.new_set()
local expect, eq = MiniTest.expect, MiniTest.expect.equality

local x = 1 + 1

-- 너무 자주 사용되어서 짧은 별칭을 사용하는 것이 유용합니다
T['expect.equality'] = function()
  eq(x, 2)
end

T['expect.no_equality'] = function()
  expect.no_equality(x, 1)
end

T['expect.error'] = function()
  -- 함수가 에러를 발생시키므로 이 기대치는 통과함
  expect.error(function()
    if x == 2 then error('의도된 에러') end
  end)
end

T['expect.no_error'] = function()
  -- 함수가 에러를 발생시키지 않으므로 이 기대치는 통과함
  expect.no_error(function()
    if x ~= 2 then error('이 에러는 발생해서는 안 됨') end
  end)
end

return T
```

### 커스텀 기대치 작성하기

`if ... error() ... end` 방식을 사용할 수도 있지만, 반복되는 기대치에 대해서는 `MiniTest.new_expectation()`을 사용하여 이 과정을 간소화할 수 있습니다. 이 플러그인에서 사용되는 예시입니다:

```lua
local T = MiniTest.new_set()

local expect_match = MiniTest.new_expectation(
  -- 기대치 대상
  '문자열 매칭',
  -- 서술어(Predicate)
  function(str, pattern) return str:find(pattern) ~= nil end,
  -- 실패 시 컨텍스트
  function(str, pattern)
    return string.format('패턴: %s\n관찰된 문자열: %s', vim.inspect(pattern), str)
  end
)

T['string matching'] = function()
  local x = 'abcd'
  -- 통과함
  expect_match(x, '^a')

  -- 실패함
  expect_match(x, 'x')
end

return T
```

'tests/test_basics.lua' 파일에서 이 내용을 실행하면 다음과 같은 메시지와 함께 실패합니다:

```
FAIL in "tests/test_basics.lua | string matching":
  Failed expectation for 문자열 매칭.
  패턴: "x"
  관찰된 문자열: abcd
  Traceback:
    tests/test_basics.lua:20
```

### 후크 (Hooks)

후크는 테스트 실행의 사전 정의된 단계에서 인자 없이 호출되는 함수입니다. 테스트 세트에 대해 정의됩니다. 네 가지 타입의 후크가 있습니다:

- **pre_once** - (필터링된) 첫 번째 노드 전에 실행됨.
- **pre_case** - 각 케이스(중첩된 경우 포함) 실행 전에 실행됨.
- **post_case** - 각 케이스(중첩된 경우 포함) 실행 후에 실행됨.
- **post_once** - (필터링된) 마지막 노드 후에 실행됨.

예제:

```lua
local new_set = MiniTest.new_set
local expect, eq = MiniTest.expect, MiniTest.expect.equality

local T = new_set()

local n = 0
local increase_n = function() n = n + 1 end

T['hooks'] = new_set({
  hooks = { pre_once = increase_n, pre_case = increase_n, post_case = increase_n, post_once = increase_n },
})

T['hooks']['work'] = function()
  -- `n`은 `pre_once`와 `pre_case`에서 두 번 증가함
  eq(n, 2)
end

T['hooks']['work again'] = function()
  -- `n`은 이전 케이스의 `post_case`와 이번 케이스 전의 `pre_case`에서 두 번 더 증가함
  eq(n, 4)
end

T['after hooks set'] = function()
  -- `n`은 이전 케이스의 `post_case`와 T['hooks'] 테스트 세트의 마지막 케이스 후 
  -- `post_once`에서 다시 두 번 더 증가함
  eq(n, 6)
end

return T
```

### 테스트 파라미터화 (Test parametrization)

'mini.test'의 특징 중 하나는 테스트 파라미터화를 활용할 수 있는 능력입니다. 후크와 마찬가지로 테스트 세트의 기능입니다.

간단한 파라미터화 예제:

```lua
local new_set = MiniTest.new_set
local eq = MiniTest.expect.equality

local T = new_set()

-- 여러 인자를 파라미터화할 수 있도록 각 파라미터는 배열이어야 함
T['parametrize'] = new_set({ parametrize = { { 1 }, { 2 } } })

-- 두 개의 케이스가 생성됨. 첫 번째는 실패함.
T['parametrize']['works'] = function(x)
  eq(x, 2)
end

-- 파라미터화는 중첩될 수 있음. 케이스는 각 파라미터 조합에 따라 "증식"함.
T['parametrize']['nested'] = new_set({ parametrize = { { '1' }, { '2' } } })

-- 네 개의 케이스가 생성됨. 그 중 두 개는 실패함.
T['parametrize']['nested']['works'] = function(x, y)
  eq(tostring(x), y)
end

-- 여러 인자 파라미터화하기
T['parametrize multiple arguments'] = new_set({ parametrize = { { 1, 1 }, { 2, 2 } } })

-- 두 개의 케이스가 생성됨. 모두 통과함.
T['parametrize multiple arguments']['works'] = function(x, y)
  eq(x, y)
end

return T
```

### 재시도 (Retry)

일부 테스트는 본질적으로 불안정(flaky)할 수 있습니다 (테스트 대상 기능이 올바르더라도 무작위로 실패할 수 있음). 예를 들어, 일련의 이벤트가 서로 정확한 지연 시간을 두고 실행되는지 테스트하는 경우입니다. 이러한 테스트는 빠른 기계에서는 안정적으로 작동할 수 있지만, 느린 기계(예: 지속적 통합 체크 중)에서는 기능이 정상이더라도 불규칙하게 실패할 수 있습니다.

불안정성을 줄이기 위해 테스트 세트 기능 중 `n_retry`가 있습니다. 이는 성공할 때까지 각 테스트 케이스를 재시도할 최대 횟수입니다.

사용 방법 예시:

```lua
local new_set = MiniTest.new_set

local T = new_set()

-- 각 케이스는 성공할 때까지 최대 5번 시도함
T['n_retry'] = new_set({ n_retry = 5 })

-- 기본값 `n_retry = 1`일 때 이 케이스는 2번 중 1번꼴로 실패함.
-- `n_retry = 5`일 때 이 케이스는 32번 중 1번꼴로 실패함.
T['n_retry']['case'] = function()
  math.randomseed(vim.loop.hrtime())
  assert(math.random() < 0.5)
end

return T
```

### 현재 케이스에 대한 런타임 액세스

"현재" 테스트 케이스에 대한 정보를 담고 있는 `MiniTest.current` 테이블이 있습니다. 여기에는 현재 실행 중인 모든 테스트를 담은 `all_cases` 필드와 *현재* 케이스를 담은 `case` 필드가 있습니다.

테스트 케이스는 순차적 테스트 실행의 단일 단위입니다. 테스트 케이스를 실행하는 데 필요한 모든 정보와 실행에 관한 데이터가 포함되어 있습니다. 예제:

```lua
local new_set = MiniTest.new_set
local eq = MiniTest.expect.equality

local T = new_set()

T['MiniTest.current.all_cases'] = function()
  -- 유용한 트릭: 런타임 데이터를 다른 무언가와 비교하여 표시하기
  eq(MiniTest.current.all_cases, 0)
end

T['MiniTest.current.case'] = function()
  eq(MiniTest.current.case, 0)
end

return T
```

이는 장황한 실패 결과로 이어집니다:

<details><summary>실패 정보</summary>

```
FAIL in "tests/test_basics.lua | MiniTest.current.all_cases":
  Failed expectation for equality.
  Left: { {
      args = {},
      data = {},
      desc = { "tests/test_basics.lua", "MiniTest.current.all_cases" },
      exec = {
        fails = {},
        notes = {},
        state = "Executing test"
      },
      hooks = {
        post = {},
        pre = {}
      },
      test = <function 1>
    }, {
      args = {},
      data = {},
      desc = { "tests/test_basics.lua", "MiniTest.current.case" },
      hooks = {
        post = {},
        pre = {}
      },
      test = <function 2>
    } }
  Right: 0
  Traceback:
    tests/test_basics.lua:8

FAIL in "tests/test_basics.lua | MiniTest.current.case":
  Failed expectation for equality.
  Left: {
    args = {},
    data = {},
    desc = { "tests/test_basics.lua", "MiniTest.current.case" },
    exec = {
      fails = {},
      notes = {},
      state = "Executing test"
    },
    hooks = {
      post = {},
      pre = {}
    },
    test = <function 1>
  }
  Right: 0
  Traceback:
    tests/test_basics.lua:12
```

</details>

### 케이스 도우미 (Case helpers)

더 견고한 케이스를 작성하는 데 도움이 되는 함수들이 있습니다: `skip()`, `finally()`, `add_note()`. `MiniTest.current` 테이블은 테스트 실행의 현재 상태에 대한 유용한 정보를 포함합니다.

예제:

```lua
local T = MiniTest.new_set()

-- `MiniTest.skip()`을 사용하면 정보가 담긴 노트를 남기면서 테스트 실행의 나머지를 
-- 건너뛸 수 있습니다. 이 테스트는 노트를 동반하여 통과 처리됩니다.
T['skip()'] = function()
  if 1 + 1 == 2 then
    MiniTest.skip('보아하니 1 + 1은 2입니다')
  end
  error('1 + 1은 2가 아닙니다')
end

-- `MiniTest.add_note()`를 사용하면 노트를 추가할 수 있습니다. 
-- 최종 상태에 "노트와 함께(with notes)" 접미사가 붙습니다.
T['add_note()'] = function()
  MiniTest.add_note('이 테스트는 중요하지 않습니다.')
  error('커스텀 에러.')
end

-- `MiniTest.finally()`를 사용하면 이 케이스가 (에러 발생 여부와 상관없이) 
-- 실행을 마친 후에 실행될 함수를 등록할 수 있습니다.
T['finally()'] = function()
  -- 테스트가 실패한 경우에만 노트 추가
  MiniTest.finally(function()
    if #MiniTest.current.case.exec.fails > 0 then
      MiniTest.add_note('이 테스트는 불안정합니다.')
    end
  end)
  error('때때로 발생하는 의도된 에러')
end

return T
```

이는 다음과 같은 메시지 결과를 보여줍니다:

```
NOTE in "tests/test_basics.lua | skip()": 보아하니 1 + 1은 2입니다

FAIL in "tests/test_basics.lua | add_note()": tests/test_basics.lua:16: 커스텀 에러.
NOTE in "tests/test_basics.lua | add_note()": 이 테스트는 중요하지 않습니다.

FAIL in "tests/test_basics.lua | finally()": tests/test_basics.lua:28: 때때로 발생하는 의도된 에러
NOTE in "tests/test_basics.lua | finally()": 이 테스트는 불안정합니다.
```

## 테스트 실행 커스터마이징

테스트 실행은 두 단계로 이루어집니다:

- **수집 (Collection)**. 각 적절한 파일(커스터마이징 가능)을 소싱하고, 모든 테스트 세트를 단일 테스트 세트로 결합하며, 이를 계층적 형태에서 순차적 형태(테스트 케이스 배열)로 변환하고, 커스터마이징 가능한 서술어에 따라 케이스를 필터링합니다.
- **실행 (Execution)**. 테스트 케이스 배열(각 pre-후크, 테스트 액션, post-후크 포함)을 예약된 비동기 방식으로 차례대로 안전하게 실행하며, 진행 상황 정보를 수집하고 커스터마이징 가능한 리포터 메서드를 호출합니다.

모든 설정은 `MiniTest.run()`의 `opts` 인자로 들어갑니다.

### 수집: 커스텀 파일 및 필터

어떤 파일이 소싱될지, 나중에 어떤 케이스가 실행될지 커스터마이징할 수 있습니다. 예제:

```lua
local new_set = MiniTest.new_set

local T = new_set()

-- 쉬운 테스트 관리를 위해 `data` 필드를 사용하여 커스텀 정보를 전달함
T['fast'] = new_set({ data = { type = 'fast' } })
T['fast']['첫 번째 테스트'] = function() end
T['fast']['두 번째 테스트'] = function() end

T['slow'] = new_set({ data = { type = 'slow' } })
T['slow']['첫 번째 테스트'] = function() vim.loop.sleep(1000) end
T['slow']['두 번째 테스트'] = function() vim.loop.sleep(1000) end

return T
```

다음 호출을 통해 이 파일('tests/test_basics.lua')만, 그리고 "fast" 케이스만 실행할 수 있습니다:

```lua
MiniTest.run({
  collect = {
    find_files = function() return { 'tests/test_basics.lua' } end,
    filter_cases = function(case) return case.data.type == 'fast' end,
  }
})
```

### 실행: 커스텀 리포터 및 첫 번째 에러에서 중단

커스텀 리포터(테스트 결과가 실시간으로 표시되는 방식)와 첫 번째 테스트 케이스 실패/에러 후 실행을 중단할지 여부를 커스터마이징할 수 있습니다. 실행 자체는 어떠한 출력도 내지 않고 대신 `MiniTest.current.all_cases`를 인플레이스(in-place)로 업데이트합니다. 각 케이스는 실행 결과 정보를 담은 `exec` 필드를 갖게 됩니다.

모든 과정이 끝난 후 커맨드 라인에 상태 요약 테이블을 표시하는 예제:

```lua
local reporter = {
  -- 그 외 사용되는 메서드로는 `start(cases)`와 `update(case_num)`가 있음
  finish = function()
    local summary = {}
    for _, c in ipairs(MiniTest.current.all_cases) do
      local state = c.exec.state
      summary[state] = (summary[state] or 0) + 1
    end

    print(vim.inspect(summary, { newline = ' ', indent = '' }))
  end,
}

MiniTest.run({ execute = { reporter = reporter } })
```

## 자식 프로세스 사용하기

다른 Lua 테스트 프레임워크와 구별되는 'mini.test'의 주요 특징은 **테스트 내부에서 자식 Neovim 프로세스를 커스텀하게 사용하는 것**을 목표로 설계되었다는 점입니다. 궁극적으로 각 테스트는 최소한의 설정(예: 플러그인 로드 허용 등)으로 초기화된 신선한 Neovim 프로세스에서 수행되어야 합니다. 이를 쉽게 만들기 위해 전용 함수 `MiniTest.new_child_neovim()`이 제공됩니다. 이는 시작/중지/재시작, 리다이렉트된 실행(현재 프로세스에서 코드를 작성하면 자식 프로세스에서 실행됨), 키 타이핑 에뮬레이션, **화면 상태 테스트** 등 많은 유용한 도우미 메서드를 가진 객체를 반환합니다.

### 시작/중지/재시작

이 자식 Neovim 객체와 연결된 자식 프로세스를 시작/중지/재시작할 수 있습니다. 현재 프로세스(테스트가 시작된 곳)와 자식 Neovim 프로세스는 RPC 메시지(`:h RPC` 참조)를 통해 서로 "대화"할 수 있습니다. 즉, 프로그래밍 방식으로 자식 프로세스 내부에서 코드를 실행하고, 현재 프로세스에서 그 출력을 가져와 기대치에 부합하는지 테스트할 수 있습니다. 자식 프로세스는 헤드리스이지만 extmarks, 플로팅 윈도우 등과 같은 것들을 테스트할 수 있도록 완벽하게 작동하는 프로세스입니다.

이 접근 방식은 여러모로 유용하고 효율적이지만, 완벽하지는 않습니다. 다음과 같은 제한 사항이 있습니다:
  - 현재의 RPC 프로토콜 구현으로 인해 함수와 userdata는 자식 프로세스와의 입출력 모두에서 사용할 수 없습니다. 이 문제의 징후는 `Cannot convert given lua type` 에러입니다. 일반적인 해결책은 전역 함수를 생성하고 사용하는 것과 같이 일부 로직을 자식 프로세스 쪽으로 옮기는 것입니다 (단, 다음 재시작 후에는 "잊혀질" 것임을 유의하세요).
  - 때때로 프로세스가 멈추는(hanging) 현상이 발생할 수 있습니다. 출력 없이 실행이 중단되는 경우입니다. 대부분의 경우 Neovim 프로세스가 "차단(blocked)"되었기 때문입니다. 즉, 사용자 입력을 기다리고 있어 다른 호출로부터 반환되지 않는 상태입니다. 흔한 원인은 활성화된 hit-enter-prompt(해결책: 프롬프트 높이를 더 크게 늘림)나 Operator-pending 모드(해결책: 거기서 나옴)입니다. 이러한 경험을 완화하기 위해 대부분의 도우미 메서드는 즉각적인 실행이 멈춤 상태로 이어질 것으로 추론되면 에러를 발생시킵니다.

다음은 자식 프로세스 관리를 위한 권장 설정입니다. 매 테스트 케이스 전에 신선한 Neovim 프로세스를 만듭니다:

```lua
local child = MiniTest.new_child_neovim()

local T = MiniTest.new_set({
  hooks = {
    pre_case = function()
      -- 커스텀 'init.lua' 스크립트로 자식 프로세스 재시작
      child.restart({ '-u', 'scripts/minimal_init.lua' })
      -- 테스트할 플러그인 로드
      child.lua([[M = require('hello_lines')]])
    end,
    -- 모든 테스트 케이스가 끝나면 중지
    post_once = child.stop,
  },
})

-- 여기에 몇 가지 테스트 정의

return T
```

### Lua 코드 실행하기

이전 섹션에서 이미 `child.lua()` 메서드를 사용하는 모습을 보여주었습니다. 이는 단일 문자열 형태의 임의의 Lua 코드를 실행합니다. 기본적으로 `vim.api.nvim_exec_lua()`의 래퍼입니다. 또한 본질적으로 `child.lua('return ' .. s, ...)`와 같은 편의용 래퍼 `child.lua_get()`도 있습니다. 예제:

```lua
local eq = MiniTest.expect.equality

local child = MiniTest.new_child_neovim()

local T = MiniTest.new_set({
  hooks = {
    pre_case = function()
      child.restart({ '-u', 'scripts/minimal_init.lua' })
      child.lua([[M = require('hello_lines')]])
    end,
    post_once = child.stop,
  },
})

T['lua()'] = MiniTest.new_set()

T['lua()']['works'] = function()
  child.lua('_G.n = 0; _G.n = _G.n + 1')
  eq(child.lua('return _G.n'), 1)
end

T['lua()']['can use tested plugin'] = function()
  eq(child.lua('return M.compute()'), { 'Hello world' })
  eq(child.lua([[return M.compute({'a', 'b'})]]), { 'Hello a', 'Hello b' })
end

T['lua_get()'] = function()
  child.lua('_G.n = 0')
  eq(child.lua_get('_G.n'), child.lua('return _G.n'))
end

return T
```

### Neovim 옵션 및 상태 관리하기

임의의 Lua 코드를 실행하는 능력만으로도 기술적으로 모든 테스트를 작성하기에 충분하지만, 문자열 입력만 사용하기 때문에 금방 번거로워집니다. 그래서 현재 Neovim 프로세스에서 코드를 작성하면 자식 프로세스에서 동일한 방식으로 자동 실행되는 것과 같은 개념의 많은 편의용 도우미들이 있습니다. 다음은 그 시연입니다:

```lua
local new_set = MiniTest.new_set
local eq = MiniTest.expect.equality

local child = MiniTest.new_child_neovim()

local T = MiniTest.new_set({
  hooks = {
    pre_case = function()
      child.restart({ '-u', 'scripts/minimal_init.lua' })
      child.lua([[M = require('hello_lines')]])
    end,
    post_once = child.stop,
  },
})

-- 이 메서드들은 각각 `vim.rpcrequest()`와 `vim.rpcnotify()`를 통해 
-- 자식 프로세스로 실행을 "리다이렉트"합니다. `child.api.xxx(...)`를 
-- 호출하면 자식 프로세스 내부에서 실행된 `vim.api.xxx(...)`의 결과를 반환합니다.
T['api()/api_notify()'] = function()
  -- 옵션 설정. 어떤 이유로 첫 번째 버퍼가 'readonly'인 경우 테스트 실행에 
  -- 큰 지연이 발생할 수 있음
  child.api.nvim_buf_set_option(0, 'readonly', false)
  eq(child.api.nvim_buf_get_option(0, 'readonly'), false)

  child.api.nvim_buf_set_lines(0, 0, -1, true, { 'Line 1' })
  eq(child.api.nvim_buf_get_lines(0, 0, -1, true), { 'Line 1' })

  -- `api_notify()`는 결과를 기다리지 않으므로(비동기) 실행 속도가 더 빠름
  child.api_notify.nvim_buf_set_lines(0, 0, -1, true, { 'Line 2' })
  eq(child.api.nvim_buf_get_lines(0, 0, -1, true), { 'Line 2' })
end

-- `child.v`, `child.g`, `child.o`, `child.bo`, `child.wo` 필드를 통해 
-- 각각 전역/변수/옵션에 접근할 수 있음
T['options and variables'] = function()
  child.g.my_var = 'hello'
  eq(child.g.my_var, 'hello')

  child.o.background = 'light'
  eq(child.o.background, 'light')

  child.bo.filetype = 'lua'
  eq(child.bo.filetype, 'lua')
end

-- `child.type_keys()`는 자식 프로세스에서 키 입력을 에뮬레이션함
T['type_keys()'] = function()
  child.type_keys('i', 'hello', '<Esc>')
  eq(child.api.nvim_get_current_line(), 'hello')
end

-- `child.get_cursor()`와 `child.set_cursor()`는 커서 위치 관리 편의 함수
T['cursor management'] = function()
  child.api.nvim_buf_set_lines(0, 0, -1, true, { 'line 1', 'line 2' })
  child.set_cursor(2, 0)
  eq(child.get_cursor(), { 2, 0 })
end

return T
```

### 화면 상태 테스트

가장 강력하고 유용한 'mini.test'의 자식 프로세스 기능 중 하나는 화면 상태 정보를 가져오고 검증하는 능력입니다. 이는 텍스트 내용뿐만 아니라 하이라이트, 가상 텍스트, 플로팅 윈도우 등의 외상태를 테스트할 수 있게 해줍니다.

`child.get_screenshot()` 메서드는 현재 자식 프로세스 화면의 스냅샷을 반환합니다. 이는 텍스트와 모든 위치의 하이라이트 정보를 담고 있는 데이터 구조입니다.

`expect.reference_screenshot()`은 스크린샷을 검사하는 특별한 기대치입니다. 다음 단계에 따라 작동합니다:
- 처음 실행될 때(또는 현재 스크린샷이 존재하지 않을 때) 현재 스크린샷을 참조용(reference)으로 'tests/screenshots' 디렉터리에 자동으로 저장합니다.
- 이후 실행 시에는 현재 스크린샷과 저장된 참조용 스크린샷을 비교합니다.
- 일치하지 않으면 에러를 발생시키며, 두 스크린샷 간의 차이점을 자세히 보여주는 정보(텍스트 차이, 하이라이트 차이 등)를 제공합니다.

이는 UI 요소가 많은 복잡한 기능을 테스트할 때 매우 유용합니다. 테스트하고자 하는 상태로 자식 프로세스를 조작한 뒤 `expect.reference_screenshot(child.get_screenshot())`을 호출하기만 하면 됩니다.

---

이 가이드를 통해 'mini.test'의 기본적인 철학과 사용법을 이해하셨기를 바랍니다. 더 자세하고 심화된 사용 사례는 'mini.nvim' 내의 각 모듈 테스트 코드를 직접 살펴보는 것을 추천합니다. 즐거운 테스트 되세요!
