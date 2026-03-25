---
title: "mini.pick"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-pick_readme.png?raw=true" alt="mini.pick" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 무엇이든 선택하기

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-pick.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-pick)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-pick.mp4?raw=true)

## 기능 {#features}

- 어떤 배열에서든 요소를 선택할 수 있는 단일 창 범용 인터페이스를 제공합니다.

- 필요에 따라 전환 가능한 미리보기(preview) 및 정보(info) 뷰를 제공합니다.

- 대화형 쿼리 매칭(필터+정렬) 기능을 제공하며, 퍼지 매칭(fuzzy matching)을 지원하고 다른 모드도 가용한 빠르고 비차단(non-blocking) 방식의 기본값을 사용합니다.

- 내장 피커(Pickers):
    - 파일.
    - 패턴 일치 (고정 패턴 또는 실시간 피드백 사용; 둘 다 glob 패턴을 통한 파일 필터링 가능).
    - 버퍼.
    - 도움말 태그.
    - CLI 출력.
    - 최근 피커 재개(Resume).

- 확장 가능한 [`MiniPick.registry`](../doc/mini-pick.qmd#minipick.registry)를 사용하는 [`:Pick`](../doc/mini-pick.qmd#pick) 명령어를 제공합니다.

- `vim.ui.select()` 구현을 제공합니다. 이를 조정하려면 [`MiniPick.ui_select()`](../doc/mini-pick.qmd#minipick.ui_select)를 사용하거나, [`MiniPick.setup()`](../doc/mini-pick.qmd#minipick.setup) 호출 후 수동으로 `vim.ui.select`를 저장/복원하세요.

- 피커가 활성화되어 있을 때 사용할 수 있는 풍부하고 커스터마이징 가능한 내장 액션들을 제공합니다:
    - 현재 포커스된 항목을 수동으로 변경.
    - 수직 및 수평 스크롤.
    - 미리보기 또는 정보 뷰 전환.
    - 나중에 선택할 항목들을 표시(Mark)/해제.
    - 현재 일치하는 항목들을 정제(Refine, 새 피커의 일부로 만듦).
    - 그 외 다수.

- 다음과 같은 최소한이면서도 유연한 소스(source) 명세를 지원합니다:
    - 항목들(Items, 배열, 콜러블, 또는 나중에 수동으로 설정).
    - 소스 이름.
    - 작업 디렉터리.
    - 매칭 알고리즘.
    - 메인 창에 일치 항목이 표시되는 방식.
    - 항목 미리보기.
    - 현재 및 표시된 항목에 대한 "선택 시" 액션.

- 전역, 버퍼별, 또는 피커별로 사용자 정의 액션/키를 설정할 수 있습니다.

- 'ignorecase' 및 'smartcase'를 즉시 지원합니다.

- 반복되는 프롬프트에서 응답성을 높이기 위해 매치 캐싱(Match caching)을 지원합니다.

참고:

- 지원되는 모든 버전에서 작동하지만, Neovim>=0.10에서는 플로팅 창 하단(footer)에 더 많은 시각적 피드백이 제공됩니다.

- 더 많은 피커는 ['mini.extra'](https://nvim-mini.org/mini.nvim/readmes/mini-extra)를 참조하세요.

- CLI 도구들은 항목을 가져오는 데 필요한 기본적인 인자들로만 호출됩니다. 출력을 커스터마이징하려면 각 도구의 설정 방식을 따르세요. 다음은 참고할 수 있는 몇 가지 예시입니다:
  - [ripgrep](https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md#configuration-file)
  - [fd](https://github.com/sharkdp/fd#excluding-specific-files-or-directories)
  - [git](https://git-scm.com/docs/gitignore)

더 자세한 정보는 도움말의 다음 섹션들을 참조하세요:

- [`:h MiniPick-overview`](../doc/mini-pick.qmd#minipick-overview)
- [`:h MiniPick-source`](../doc/mini-pick.qmd#minipick-source)
- [`:h MiniPick-actions`](../doc/mini-pick.qmd#minipick-actions)
- [`:h MiniPick-examples`](../doc/mini-pick.qmd#minipick-examples)
- [`:h MiniPick.builtin`](../doc/mini-pick.qmd#minipick.builtin)

## 의존성 {#dependencies}

완전한 경험을 위해 필요합니다 (아래 도구들이 없어도 여전히 작동합니다):

- 실제 경로를 나타내는 항목 옆에 아이콘을 표시하기 위해 ['mini.icons'](https://nvim-mini.org/mini.nvim/readmes/mini-icons) 모듈을 활성화하세요. [nvim-tree/nvim-web-devicons](https://github.com/nvim-tree/nvim-web-devicons) 플러그인으로 대체할 수도 있습니다.

- 디스크에서 더 빠른 파일 및 패턴 검색을 위해 실행 가능한 [BurntSushi/ripgrep](https://github.com/BurntSushi/ripgrep) CLI 도구가 필요합니다.

## 개요 {#overview}

일반적인 개념은 객체 배열을 가져와 대화형 필터/정렬/탐색/미리보기와 함께 표시하고 하나 이상의 항목을 선택할 수 있게 하는 것입니다.

### 피커를 시작하는 방법

- [`MiniPick.start()`](../doc/mini-pick.qmd#minipick.start)를 호출하며 `opts.source`로 소스를 정의합니다.

    예시: `MiniPick.start({ source = { items = vim.fn.readdir('.') } })`

- [`MiniPick.builtin`](../doc/mini-pick.qmd#minipick.builtin) 피커 중 하나를 직접 사용합니다.

    예시: `MiniPick.builtin.files({ tool = 'git' })`

- [`MiniPick.registry`](../doc/mini-pick.qmd#minipick.registry)의 커스터마이징 가능한 피커들을 사용하는 [`:Pick`](../doc/mini-pick.qmd#pick) 명령어를 사용합니다.

    예시: `:Pick files tool='git'`

### 사용자 인터페이스

UI는 세 가지 다른 뷰를 표시할 수 있는 단일 창으로 구성됩니다:

- "Main" - 현재 쿼리와 일치하는 항목들이 표시되는 곳입니다.
- "Preview" - 현재 항목의 미리보기입니다 (`<Tab>`으로 전환).
- "Info" - 피커 및 그 상태에 대한 일반적인 정보입니다 (`<S-Tab>`으로 전환).

현재 프롬프트는 창 테두리 왼쪽 상단에 표시되며, 세로선은 캐럿(현재 입력 위치)을 나타냅니다.

창 테두리의 하단(Neovim>=0.10)에는 추가적인 시각적 피드백이 표시됩니다:

- 왼쪽은 피커 이름입니다.
- 오른쪽은 다음과 같은 형식의 정보를 포함합니다:

    `<일치 항목 중 현재 인덱스> | <일치 항목 수> | <표시된 항목 수> / <전체 항목 수>`

피커가 작업 중일 때(항목이 아직 설정되지 않았거나 매칭이 활성화된 경우 등)는 유휴 시간이 `config.delay.busy` 밀리초를 지나면 창 테두리 색상이 `MiniPickBorderBusy`로 변경됩니다.

### 라이프 사이클

- 문자를 입력하여 일치 항목을 필터링하고 정렬합니다. 입력된 문자 배열인 `query`와 함께 [`MiniPick.default_match()`](../doc/mini-pick.qmd#minipick.default_match)를 사용합니다. 매칭 방식의 개요:
    - 쿼리가 `'`로 시작하면 정확히 일치(exact match)하는 것을 찾습니다.
    - 쿼리가 `^`로 시작하면 시작 부분이 정확히 일치하는 것을 찾습니다.
    - 쿼리가 `$`로 끝나면 끝부분이 정확히 일치하는 것을 찾습니다.
    - 쿼리가 `*`로 시작하면 강제로 퍼지(fuzzy) 매칭을 수행합니다.
    - 그 외의 경우 퍼지 매칭을 수행합니다.
    - 정렬은 먼저 일치하는 부분의 너비를 최소화하고, 그 다음 일치하는 시작 지점을 최소화하는 방식으로 이루어집니다.
      그 이상의 복잡한 방식(문자열 내 특정 위치를 선호하는 등)은 사용하지 않습니다.

- 특수 키를 입력하여 액션을 수행합니다. 기본적인 것들은 다음과 같습니다:
    - `<C-n>` / `<Down>`은 아래로 이동, `<C-p>` / `<Up>`은 위로 이동합니다.
    - `<Left>` / `<Right>`는 프롬프트 캐럿을 왼쪽/오른쪽으로 이동합니다.
    - `<S-Tab>`은 사용 가능한 모든 매핑이 포함된 정보 창을 전환합니다.
    - `<Tab>`은 미리보기를 전환합니다.
    - `<C-x>` / `<C-a>`는 현재/모든 항목을 표시(Mark) 또는 해제합니다.
    - `<C-Space>` / `<M-Space>`는 모든 일치 항목 또는 표시된 항목들을 새로운 피커로 만듭니다.
    - `<CR>` / `<M-CR>`은 현재/표시된 항목들을 선택합니다.
    - `<Esc>` / `<C-c>`는 피커를 중단합니다.

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
    | Main   | `add('nvim-mini/mini.pick')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.pick', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.pick', version = false },` |
    | Stable | `{ 'nvim-mini/mini.pick', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.pick'`                         |
    | Stable | `Plug 'nvim-mini/mini.pick', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.pick').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 지연 시간 (ms; 최소 1 이상이어야 함)
  delay = {
    -- 비동기 동작을 강제할 때까지의 지연 시간
    async = 10,

    -- 계산 시작 후 시각적 피드백을 표시할 때까지의 지연 시간
    busy = 50,
  },

  -- 액션 수행을 위한 매핑. [`:h MiniPick-actions`](../doc/mini-pick.qmd#minipick-actions)를 참조하세요.
  mappings = {
    caret_left  = '<Left>',
    caret_right = '<Right>',

    choose            = '<CR>',
    choose_in_split   = '<C-s>',
    choose_in_tabpage = '<C-t>',
    choose_in_vsplit  = '<C-v>',
    choose_marked     = '<M-CR>',

    delete_char       = '<BS>',
    delete_char_right = '<Del>',
    delete_left       = '<C-u>',
    delete_word       = '<C-w>',

    mark     = '<C-x>',
    mark_all = '<C-a>',

    move_down  = '<C-n>',
    move_start = '<C-g>',
    move_up    = '<C-p>',

    paste = '<C-r>',

    refine        = '<C-Space>',
    refine_marked = '<M-Space>',

    scroll_down  = '<C-f>',
    scroll_left  = '<C-h>',
    scroll_right = '<C-l>',
    scroll_up    = '<C-b>',

    stop = '<Esc>',

    toggle_info    = '<S-Tab>',
    toggle_preview = '<Tab>',
  },

  -- 일반 옵션
  options = {
    -- 콘텐츠를 아래에서 위로 표시할지 여부
    content_from_bottom = false,

    -- 매치 항목을 캐시할지 여부 (반복 프롬프트 시 속도는 높으나 메모리 사용량이 늘어남)
    use_cache = false,
  },

  -- 소스 정의. [`:h MiniPick-source`](../doc/mini-pick.qmd#minipick-source)를 참조하세요.
  source = {
    items = nil,
    name  = nil,
    cwd   = nil,

    match   = nil,
    show    = nil,
    preview = nil,

    choose        = nil,
    choose_marked = nil,
  },

  -- 창 관련 옵션
  window = {
    -- 플로팅 창 설정 (테이블 또는 이를 반환하는 콜러블)
    config = nil,

    -- 프롬프트에서 캐럿으로 사용할 문자열
    prompt_caret = '▏',

    -- 프롬프트에서 접두사로 사용할 문자열
    prompt_prefix = '> ',
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [nvim-telescope/telescope.nvim](https://github.com/nvim-telescope/telescope.nvim)
- [ibhagwan/fzf-lua](https://github.com/ibhagwan/fzf-lua)
