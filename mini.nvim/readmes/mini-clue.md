---
title: "mini.clue"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-clue_readme.png?raw=true" alt="mini.clue" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 다음 키 힌트(clue) 표시

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-clue.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-clue)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-clue.mp4?raw=true)

## 기능 {#features}

- 대상 키 조합에 도달하기 위한 사용자 정의 키 쿼리 프로세스를 구현합니다:
    - 커스터마이징 가능한 옵트인(opt-in) 트리거(모드 + 키) 후에 시작됩니다.
    - 각 키 입력은 가능한 대상 세트를 좁힙니다.
    - `<BS>`를 누르면 이전에 입력한 내용이 제거됩니다.
    - `<Esc>` 또는 `<C-c>`를 누르면 프로세스가 조기에 중단됩니다.
    - 'timeoutlen'에 의존하지 않으며 'langmap'을 기본적으로 지원합니다.
    - 대상이 하나만 남거나 사용자가 `<CR>`을 누르면 종료됩니다. 결과적으로 모든 쿼리 키와 가능한 포스트키(postkeys)를 누른 것처럼 에뮬레이션됩니다.

- 힌트가 포함된 창을 (설정 가능한 지연 시간 후에) 보여줍니다. 사용 가능한 다음 키와 그에 대한 설명(기존 키맵의 설명과 사용자가 제공한 힌트에서 자동 생성되며 전자를 선호함)을 나열합니다.

- 키 조합에 대한 설정 가능한 "포스트키(postkeys)"를 제공합니다 - 키 쿼리 프로세스 중에 조합에 도달한 후 에뮬레이션될 키들입니다.

- 일반적인 내장 키/개념들에 대해 커스터마이징 가능한 고정 힌트 세트를 제공합니다:
    - `g` 키.
    - `z` key.
    - 창(Window) 명령.
    - 내장 자동 완성.
    - 마크(Marks).
    - 레지스터(Registers).

- 트리거를 전역적으로 또는 버퍼별로 비활성화/활성화하는 Lua 함수를 제공합니다.

더 자세한 정보는 도움말의 다음 부분을 참조하세요:

- [`:h MiniClue-key-query-process`](../doc/mini-clue.qmd#miniclue-key-query-process)
- [`:h MiniClue-examples`](../doc/mini-clue.qmd#miniclue-examples)
- [`:h MiniClue.config`](../doc/mini-clue.qmd#miniclue.config)
- [`:h MiniClue.gen_clues`](../doc/mini-clue.qmd#miniclue.gen_clues)

참고:

- 두 가지 다른 작업을 명확히 분리하기 위해 매핑을 직접 생성하는 기능은 포함되어 있지 않습니다.
- 권장되는 가장 좋은 방법은 수동으로 설명을 포함하여 매핑을 생성하는 것입니다 (옵션의 `desc` 필드 사용). 이렇게 하면 힌트 창에 자동으로 사용됩니다.

- 트리거는 특수한 버퍼 로컬 매핑으로 구현됩니다. 이로 인해 다음과 같은 몇 가지 주의 사항이 있습니다:
    - 동일한 일반 버퍼 로컬 매핑을 덮어쓰고 전역 매핑보다 우선순위를 갖습니다.
      예: `<C-w>`를 노멀 모드 트리거로 설정하면 다른 `<C-w>` 매핑이 없어야 함을 의미합니다.
    - 가장 마지막에 생성된 버퍼 로컬 매핑이어야 제대로 작동합니다. 가장 흔한 증상은 힌트 창이 표시된 후에만 일부 매핑이 작동하기 시작하는 것입니다.
      예: `g`가 노멀 모드 트리거로 설정되어 있지만 'mini.comment'의 `gcc`가 즉시 작동하지 않는 경우. 이는 아마도 `g` 트리거용 매핑 이후에 생성된 `g`로 시작하는 다른 버퍼 로컬 매핑이 있기 때문일 것입니다. 보통 LSP 서버의 `on_attach`나 버퍼에서 tree-sitter가 시작될 때 발생합니다.
      트리거가 가장 최근의 버퍼 로컬 매핑인지 확인하려면 `:<mode-char>map <trigger-keys>`를 실행하세요 (앞의 예시라면 `:nmap g`). 트리거 매핑이 목록의 첫 번째여야 합니다.
    - 이 모듈은 대부분의 일반적인 경우에 즉시 작동하도록 최선을 다하지만 완벽하지는 않습니다. 트리거가 모든 버퍼 로컬 매핑 후에 생성되도록 [`MiniClue.setup()`](../doc/mini-clue.qmd#miniclue.setup) 또는 [`MiniClue.ensure_buf_triggers()`](../doc/mini-clue.qmd#miniclue.ensure_buf_triggers)를 실행하는 것이 해결책입니다.

- 기존 매핑의 설명은 사용자가 제공한 힌트보다 우선합니다. 이는 힌트 창에 표시되는 정보가 가능한 한 관련성이 높도록 하기 위함입니다. 기존 매핑의 설명을 추가하거나 커스터마이징하려면 [`MiniClue.set_mapping_desc()`](../doc/mini-clue.qmd#miniclue.set_mapping_desc)를 사용하세요.

- 기술적인 어려움으로 인해 연산자 대기(Operator-pending) 모드 트리거(예: 'mini.ai'의 `a`/`i`)에 대한 지원은 완벽하지 않습니다:
    - 구현의 어려움으로 인해 "임시 노멀 모드"(예: Insert 모드에서의 `<C-o>` 후)의 명령 일부로는 작동하지 않습니다.
    - 사용자 정의 연산자와 함께 사용할 때 예기치 않은 동작이 발생할 수 있습니다.

- 매크로와 관련하여 (대부분 해결된) 이슈가 있습니다:
    - 기술적인 이유로 매크로 기록 중에는 모든 트리거가 비활성화됩니다.
    - `@` 및 `Q` 키는 트리거를 임시로 비활성화하기 위해 [`MiniClue.setup()`](../doc/mini-clue.qmd#miniclue.setup) 내부에서 특수하게 매핑됩니다.

## 설정 빠른 시작 {#config-quick-start}

```lua
local miniclue = require('mini.clue')
miniclue.setup({
  triggers = {
    -- Leader 트리거
    { mode = { 'n', 'x' }, keys = '<Leader>' },

    -- `[` 및 `]` 키
    { mode = 'n', keys = '[' },
    { mode = 'n', keys = ']' },

    -- 내장 자동 완성
    { mode = 'i', keys = '<C-x>' },

    -- `g` 키
    { mode = { 'n', 'x' }, keys = 'g' },

    -- 마크 (Marks)
    { mode = { 'n', 'x' }, keys = "'" },
    { mode = { 'n', 'x' }, keys = '`' },

    -- 레지스터 (Registers)
    { mode = { 'n', 'x' }, keys = '"' },
    { mode = { 'i', 'c' }, keys = '<C-r>' },

    -- 창 명렁
    { mode = 'n', keys = '<C-w>' },

    -- `z` 키
    { mode = { 'n', 'x' }, keys = 'z' },
  },

  clues = {
    -- <Leader> 매핑 그룹에 대한 설명을 추가하여 이를 강화하세요
    miniclue.gen_clues.square_brackets(),
    miniclue.gen_clues.builtin_completion(),
    miniclue.gen_clues.g(),
    miniclue.gen_clues.marks(),
    miniclue.gen_clues.registers(),
    miniclue.gen_clues.windows(),
    miniclue.gen_clues.z(),
  },
})
```

## 설치 {#installation}

이 플러그인은 'mini.nvim' 라이브러리의 일부로 설치하거나(**권장**), 독립적인 Git 저장소로 설치할 수 있습니다.

두 가지 브랜치 중 하나를 골라 설치할 수 있습니다:

- `main` (기본값, **권장**): 플러그인의 최신 개발 버전입니다. 마지막 안정 릴리스 이후의 모든 변경 사항은 베타 테스트 단계(알파 테스트를 통과하고 어느 정도 안정됨을 의미)로 간주되어야 합니다.
- `stable`: `main` 브랜치에서 공개 베타 테스트를 거친 코드가 포함된 릴리스 시에만 업데이트됩니다.

다음은 몇 가지 일반적인 설치 방법의 코드 스니펫입니다 (하나만 사용하세요):

<details>
<summary><a href="https://nvim-mini.org/mini.nvim/readmes/mini-deps">mini.deps</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | *권장되는 'mini.deps' 설치 방법을 따르세요* |
    | Stable | *권장되는 'mini.deps' 설치 방법을 따르세요* |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                                   |
    |--------|----------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.clue')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.clue', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.clue', version = false },` |
    | Stable | `{ 'nvim-mini/mini.clue', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.clue'`                         |
    | Stable | `Plug 'nvim-mini/mini.clue', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.clue').setup()`을 호출해야 합니다. **트리거 설정이 반드시 필요합니다.**

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 표시할 추가 힌트의 배열
  clues = {},

  -- 사용자 정의 키 쿼리 프로세스를 시작하는 옵트인 트리거의 배열.
  -- **힌트를 보여주려면 무엇이라도 설정되어야 합니다.**
  triggers = {},

  -- 힌트 창 설정
  window = {
    -- 플로팅 창 설정
    config = {},

    -- 힌트 창을 보여주기 전 지연 시간
    delay = 1000,

    -- 힌트 창 내부에서 스크롤하기 위한 키
    scroll_down = '<C-d>',
    scroll_up = '<C-u>',
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [folke/which-key.nvim](https://github.com/folke/which-key.nvim)
- [anuvyklack/hydra.nvim](https://github.com/anuvyklack/hydra.nvim)
