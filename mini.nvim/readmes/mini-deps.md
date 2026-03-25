---
title: "mini.deps"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-deps_readme.png?raw=true" alt="mini.deps" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 플러그인 매니저

[`git`](https://git-scm.com/) CLI 도구가 설치되어 있고 호출 가능해야 합니다. 미리 설정되어 있는지 확인하세요.

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-deps.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-deps)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-deps.mp4?raw=true)

**참고**: 이 데모에서는 [mini.notify](https://nvim-mini.org/mini.nvim/readmes/mini-notify)의 커스텀 `vim.notify()`를 사용합니다.

## 기능 {#features}

- Git과 내장 패키지(built-in packages)를 활용하여 다음 동작으로 플러그인을 관리합니다:
    - 현재 세션에 플러그인 추가, 없는 경우 다운로드.
    - 확인 유무 선택, 새 데이터 병렬 다운로드 여부 선택과 함께 업데이트.
    - 확인 유무 선택과 함께 사용하지 않는 플러그인 삭제.
    - 스냅샷 가져오기 / 설정 / 저장 / 로드.

- 최소한의 설정으로 유연한 플러그인 사양 정의:
    - 플러그인 소스.
    - 대상 플러그인 디렉터리 이름.
    - 체크아웃 대상: 브랜치, 커밋, 태그 등.
    - 체크아웃하지 않고 업데이트를 추적하기 위한 모니터(monitor) 브랜치.
    - 대상 플러그인보다 먼저 설정되어야 하는 의존성.
    - 플러그인이 생성/변경되기 전후에 호출할 훅(hooks).

- 2단계 시작(startup)을 구현하는 헬퍼: `now()` 및 `later()`.

더 자세한 정보는 도움말의 다음 부분을 참조하세요:

- [`:h MiniDeps-overview`](../doc/mini-deps.qmd#minideps-overview)
- [`:h MiniDeps-plugin-specification`](../doc/mini-deps.qmd#minideps-plugin-specification)
- [`:h MiniDeps-commands`](../doc/mini-deps.qmd#minideps-commands)

## 설치 {#installation}

이 플러그인은 'mini.nvim' 라이브러리의 일부로 설치하거나(**권장**), 독립적인 Git 저장소로 설치할 수 있습니다.

적절한 디렉터리에서 `git clone`을 통해 수동으로 설치해야 합니다. 다음은 'init.lua' 상단에 넣을 수 있는 권장 스니펫입니다:

```lua
-- 'mini.nvim'을 'mini.deps'가 관리하는 방식으로 직접 클론합니다.
local path_package = vim.fn.stdpath('data') .. '/site/'
local mini_path = path_package .. 'pack/deps/start/mini.nvim'
if not vim.loop.fs_stat(mini_path) then
  vim.cmd('echo "Installing [`mini.nvim`](../doc/mini-nvim.qmd#mini.nvim)" | redraw')
  local clone_cmd = {
    'git', 'clone', '--filter=blob:none',
    'https://github.com/nvim-mini/mini.nvim', mini_path
  }
  vim.fn.system(clone_cmd)
  vim.cmd('packadd mini.nvim | helptags ALL')
  vim.cmd('echo "Installed [`mini.nvim`](../doc/mini-nvim.qmd#mini.nvim)" | redraw')
end

-- 'mini.deps' 설정 (취향에 맞게 조정하세요)
require('mini.deps').setup({ path = { package = path_package } })
```

기본 'main' 브랜치를 사용해도 괜찮습니다. (지금까지는) 거기서 발생한 변경 사항이 실수로 무언가를 고장 내는 일은 거의 없었습니다. 하지만 더욱 안전하게 'mini.nvim'의 안정된 릴리스만 사용하고 싶다면, 'mini.deps' 설정 후에 `MiniDeps.add({ name = 'mini.nvim', checkout = 'stable' })`를 추가하고 `:DepsUpdateOffline mini.nvim`을 실행하세요.

독립 저장소에서 설치하려면 위 코드 스니펫에서 'mini.nvim'을 모두 'mini.deps'로 바꾸면 됩니다.

**참고**: 'mini.nvim'은 항상 'mini.deps' 세션에 포함되도록 'pack/deps/opt'가 아닌 'pack/deps/start'에 설치됩니다. (다른 설치된 플러그인들처럼) "opt" 플러그인으로 만들고 싶다면 'pack/deps/opt'를 사용하되, 'mini.deps' 설정 후에 `MiniDeps.add('mini.nvim')`을 호출하세요.

## 개요 {#overview}

'mini.deps'를 어떻게 사용할 수 있는지에 대한 빠른 데모로 [예시 'init.lua' 파일](../scripts/init-deps-example.lua)을 보고 사용해 보세요:

- 내용을 '~/.config/nvim-deps/init.lua' 파일(UNIX 시스템 기준)에 복사합니다.
- `NVIM_APPNAME=nvim-deps nvim -- ~/.config/nvim-deps/init.lua`를 실행합니다. (Neovim<0.10에서는 첫 실행 시 tree-sitter 관련 문제가 표시될 수 있습니다.) 이렇게 하면 해당 'init.lua'만을 설정으로 사용하여 Neovim을 실행하며, **현재 설정에는 전혀 영향을 주지 않습니다.**

### 디렉터리 구조

이 모듈은 현재 세션에서 플러그인을 사용할 수 있도록 내장 패키지(built-in packages)를 사용합니다. `config.path.package` 디렉터리 내부의 "pack/deps" 패키지와 함께 작동합니다.

기본적으로 "opt" 서브디렉터리는 [`MiniDeps.add()`](../doc/mini-deps.qmd#minideps.add)를 통해 필요할 때 로드되는 선택적 플러그인을 설치하는 데 사용됩니다. "start" 서브디렉터리에 있는 비선택적 플러그인도 지원되지만, 초기 설치 후 수동으로 이동한 경우에만 해당됩니다.

### 플러그인 추가

[`MiniDeps.add()`](../doc/mini-deps.qmd#minideps.add)를 사용하여 현재 세션에 플러그인을 추가합니다. 플러그인의 URL 소스를 문자열로 제공하거나 일반적인 플러그인 사양을 제공합니다. 플러그인이 "pack/deps" 패키지에 없으면 다른 것을 처리하기 전에 먼저 생성(즉, 설치)됩니다.

플러그인을 추가하는 권장 방법은 'init.lua' 파일에서 [`MiniDeps.add()`](../doc/mini-deps.qmd#minideps.add)를 호출하는 것입니다 ([MiniDeps.setup()`](../doc/mini-deps.qmd#minideps.setup)이 먼저 호출되었는지 확인하세요):

```lua
local add = MiniDeps.add

-- 현재 세션에 추가 (없는 경우 설치)
add({
  source = 'neovim/nvim-lspconfig',
  -- 대상 플러그인 근처에 의존성 제공
  depends = { 'williamboman/mason.nvim' },
})

add({
  source = 'nvim-treesitter/nvim-treesitter',
  -- 'main' 브랜치의 업데이트를 모니터링하면서 'master'를 사용
  checkout = 'master',
  monitor = 'main',
  -- 매 체크아웃 후에 동작 수행
  hooks = { post_checkout = function() vim.cmd('TSUpdate') end },
})
-- 추가된 플러그인에 의존하는 코드를 즉시 실행하는 것도 가능합니다
require('nvim-treesitter.configs').setup({
  ensure_installed = { 'lua', 'vimdoc' },
  highlight = { enable = true },
})
```

참고:

- 성능 향상을 위해 `add()`는 디바이스에 존재 여부만 확인하며 그 외의 것은 하지 않습니다. 특히 `opts.checkout` 상태를 보장하지 않습니다. 플러그인 상태를 명시적으로 업데이트하거나 수정하세요 (다음 섹션 참조).

### 플러그인 사양 (Plugin specification)

사양은 단일 문자열일 수 있으며 다음과 같이 유추됩니다:

- "/"를 포함하지 않으면 플러그인 `name`.
- 그렇지 않으면 플러그인 `source`.

기본적으로 사양은 다음 필드를 갖는 테이블입니다 (더 자세한 내용은 [`:h MiniDeps-plugin-specification`](../doc/mini-deps.qmd#minideps-plugin-specification) 참조):

| 필드       | 설명                          |
|------------|------------------------------|
| `source`   | 플러그인 소스의 URI           |
| `name`     | 디스크에서 사용할 이름        |
| `checkout` | 대상 상태                     |
| `monitor`  | 모니터 브랜치                 |
| `depends`  | 플러그인 의존성 배열          |
| `hooks`    | 훅(hooks) 테이블              |

### 지연 로딩 (Lazy loading)

모든 지연 로딩은 적절한 시점에 [`MiniDeps.add()`](../doc/mini-deps.qmd#minideps.add)를 호출하여 수동으로 수행되는 것으로 가정합니다. 이 모듈은 특수하고 안전한 2단계 로딩을 구현하는 헬퍼를 제공합니다:

- [`MiniDeps.now()`](../doc/mini-deps.qmd#minideps.now)는 코드를 즉시 안전하게 실행합니다. 초기 화면 그리기에 필요한 UI 플러그인을 로드할 때 사용하세요.
- [`MiniDeps.later()`](../doc/mini-deps.qmd#minideps.later)는 코드가 나중에 안전하게 실행되도록 예약하며 순서를 유지합니다. 정확한 타이밍이 필요하지 않은 다른 모든 것들에 사용하세요 (주의 요망). 곧 다음 이벤트 루프 중 하나에서 실행될 것입니다.

```lua
local now, later = MiniDeps.now, MiniDeps.later

-- 즉시 안전하게 실행
now(function() vim.cmd('colorscheme miniwinter') end)
now(function() require('mini.statusline').setup() end)

-- 나중에 안전하게 실행
later(function() require('mini.pick').setup() end)
```

### 업데이트

현재 세션의 플러그인을 소스의 새로운 데이터로 업데이트하려면 [`:DepsUpdate`](../doc/mini-deps.qmd#depsupdate)를 사용하세요. 이는 (멀티 코어를 활용하여) 업데이트를 다운로드하고 확인 버퍼를 보여줍니다. 업데이트를 완료하려면 상단의 지침을 따르세요.

참고: 이는 디스크 상의 플러그인을 업데이트하는 것이며, 현재 세션에는 영향을 주지 않을 가능성이 큽니다. 제대로 로드하려면 Nvim을 재시작하세요.

### 수정 (Modify)

플러그인의 사양을 변경하려면(예: 다른 `checkout` 설정 등):

- 해당 [`MiniDeps.add()`](../doc/mini-deps.qmd#minideps.add) 호출을 업데이트합니다.
- `:DepsUpdateOffline <plugin_name>`을 실행합니다.
- 변경 사항을 검토하고 확인합니다.
- Nvim을 재시작합니다.

참고: 이전에 `add()`에서 단일 소스 문자열을 사용했다면, 인자를 `{ source = '<이전_인자>', checkout = '<상태>' }`로 변환해야 합니다.

### 스냅샷 (Snapshots)

[`:DepsSnapSave`](../doc/mini-deps.qmd#depssnapsave)를 사용하여 현재 세션의 모든 플러그인 상태를 스냅샷 파일에 저장합니다 (`config.path.snapshot` 참조).

[`:DepsSnapLoad`](../doc/mini-deps.qmd#depssnapload)를 사용하여 스냅샷을 로드합니다. 이는 (확인 없이) 디스크의 상태를 변경합니다. 스냅샷 파일과 현재 세션 모두에 존재하는 플러그인이 영향을 받습니다. 효과를 보려면 Nvim을 재시작하세요.

참고: 스냅샷 로딩은 [`MiniDeps.add()`](../doc/mini-deps.qmd#minideps.add) 호출 내부에 정의된 플러그인의 사양을 변경하지 않습니다. 즉, 다음 업데이트 시 플러그인의 상태가 변경될 수 있습니다. 영구적으로 유지하려면 플러그인을 수동으로 대상 상태에 고정(freeze)하세요.

### 고정 (Freeze)

플러그인 사양의 `checkout`이 태그, 상태(커밋 해시) 또는 'HEAD'(현재 상태로 고정)와 같은 고정된 대상을 가리키도록 수정합니다.

고정된 플러그인은 업데이트를 받지 않습니다. [`:DepsUpdate`](../doc/mini-deps.qmd#depsupdate) 후에 확인 버퍼에 표시될 `monitor` 브랜치를 "구독"하여 소스의 새로운 변경 사항을 모니터링할 수 있습니다.

예: `checkout = 'v0.10.0'`을 사용하여 플러그인을 "v0.10.0" 태그에 고정하면서 동시에 `monitor`(보통 기본 브랜치)의 로그에서 새로운 버전을 모니터링합니다.

### 롤백 (Rollback)

업데이트가 만족스럽지 않을 때 되돌리는 방법:

- 작동했던 마지막 상태의 식별자를 가져옵니다:
    - [`:DepsShowLog`](../doc/mini-deps.qmd#depsshowlog)를 사용하여 업데이트 로그를 보고, 플러그인 이름을 찾아 "State before:"로 나열된 식별자를 복사합니다.
    - 이전에 저장된 스냅샷 파일에서 플러그인 이름을 찾고 그 옆의 식별자를 복사합니다.
- 적절한 브랜치를 모니터링하면서 해당 상태로 플러그인을 고정합니다. 업데이트를 다시 시작하려면 [`MiniDeps.add()`](../doc/mini-deps.qmd#minideps.add) 호출을 이전 형태로 되돌립니다.

### 제거 (Remove)

- 현재 세션에 대상 플러그인이 등록되어 있지 않은지 확인합니다. 보통 해당하는 [`MiniDeps.add()`](../doc/mini-deps.qmd#minideps.add) 호출을 제거하는 것을 의미합니다.
- [`:DepsClean`](../doc/mini-deps.qmd#depsclean)을 실행합니다. 디스크에서 삭제될 플러그인 목록이 포함된 확인 버퍼가 나타납니다. 상단의 지침을 따라 청소를 완료하세요.

또는 "pack/deps" 패키지에서 플러그인 디렉터리를 수동으로 삭제할 수도 있습니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- CLI 작업 파라미터
  job = {
    -- 사용할 병렬 스레드 수. 기본값: 가용 스레드의 80%.
    n_threads = nil,

    -- 강제 종료 전 각 작업의 타임아웃 (ms)
    timeout = 30000,
  },

  -- 데이터 저장 위치 경로
  path = {
    -- 내장 패키지 디렉터리.
    -- 모든 플러그인은 실제로 'pack/deps' 서브디렉터리에 저장됩니다.
    package = vim.fn.stdpath('data') .. '/site',

    -- 기본 스냅샷 파일 경로
    snapshot = vim.fn.stdpath('config') .. '/mini-deps-snap',

    -- 로그 파일
    log = vim.fn.stdpath('log') .. '/mini-deps.log'
  },

  -- 에러가 아닌 피드백 표시 여부
  silent = false,
}
```

## 유사한 플러그인 {#similar-plugins}

- [folke/lazy.nvim](https://github.com/folke/lazy.nvim)
- [savq/paq-nvim](https://github.com/savq/paq-nvim)
- [junegunn/vim-plug](https://github.com/junegunn/vim-plug)
