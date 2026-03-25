---
title: "mini.completion"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-completion_readme.png?raw=true" alt="mini.completion" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 자동 완성 및 시그니처 헬프(signature help) 플러그인

- 비동기식(커스터마이징 가능한 '디바운스' 지연 시간 포함) '2단계 체인 자동 완성'을 지원합니다: 먼저 내장 LSP를 시도하고, 실패 시 설정된 폴백(fallback)을 실행합니다.
- 자동 완성 항목 정보 및 함수 시그니처 표시 기능을 제공합니다 (둘 다 설정 가능한 지연 시간 후 플로팅 창에 표시됨).

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-completion.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-completion)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-completion.mp4?raw=true)

## 기능 {#features}

- 2단계 체인 자동 완성:
    - 1단계는 LSP 자동 완성입니다. `additionalTextEdits`(자동 임포트 등) 및 스니펫( ["스니펫"](#snippets) 참조)을 지원합니다. (최상의 결과를 위해 ['mini.snippets'](https://nvim-mini.org/mini.nvim/readmes/mini-snippets) 의존성이 권장됩니다).
    - 1단계가 설정되지 않았거나 결과가 없는 경우, 폴백 동작이 실행됩니다. 가장 많이 테스트된 동작은 Neovim의 내장 Insert 모드 자동 완성입니다.
- 자동 완성 항목 정보('completionItem/resolve' 요청을 통해) 및 시그니처 헬프(LSP 서버가 정보를 제공하는 경우 활성 매개변수 하이라이트 포함)를 플로팅 창에 자동으로 표시합니다. 정보/시그니처 창 모두에서 스크롤이 가능합니다 (기본값 `<C-f>` / `<C-b>`).
- 자동화된 동작은 설정 가능한 지연 시간 후에 수행됩니다. 이는 계산 부하를 줄이고 빠른 타이핑(자동 완성 및 시그니처 헬프) 및 항목 선택(항목 정보)을 가능하게 합니다.
- 사용자가 2단계/폴백 자동 완성을 강제로 실행할 수 있습니다 (기본값 `<C-Space>` / `<A-Space>`).
- LSP 항목의 하이라이트를 커스터마이징할 수 있습니다 (Neovim>=0.11 필요). 다음을 지원합니다:
    - 항목 레이블: 기본적으로 항목이 사용 중단(deprecated)으로 표시되었는지만 확인하고 `MiniCompletionDeprecated` 하이라이트 그룹을 설정합니다.
    - LSP 종류(Kind, 예: "Function", "Keyword" 등): ['mini.icons'](https://nvim-mini.org/mini.nvim/readmes/mini-icons) 모듈이 활성화되어 있어야 합니다 (해당 모듈의 "lsp" 카테고리를 사용함).

## 의존성 {#dependencies}

완전한 경험을 위해 권장되는 사항입니다 (권장 사항 없이도 작동합니다):

- LSP 종류(Kind)를 하이라이트하기 위해 ['mini.icons'](https://nvim-mini.org/mini.nvim/readmes/mini-icons) 모듈 활성화 (Neovim>=0.11 필요). 없는 경우 [`MiniCompletion.default_process_items()`](../doc/mini-completion.qmd#minicompletion.default_process_items)는 하이라이트를 추가하지 않습니다. [`MiniIcons.tweak_lsp_kind()`](../doc/mini-icons.qmd#miniicons.tweak_lsp_kind)도 확인해 보세요.
- 더 나은 스니펫 처리를 위해 ['mini.snippets'](https://nvim-mini.org/mini.nvim/readmes/mini-snippets) 모듈 활성화 (**적극 권장**). 없는 경우 및 커스텀 스니펫 삽입이 설정되지 않은 경우, Neovim>=0.10에서는 `vim.snippet.expand()`가 사용됩니다 (이전 버전에서는 추가 작업이 수행되지 않습니다). [`:h MiniCompletion.default_snippet_insert()`](../doc/mini-completion.qmd#minicompletion.default_snippet_insert)를 참조하세요.

## 스니펫 {#snippets}

LSP 사양에 따라, 일부 자동 완성 항목은 스니펫 형태로 제공될 수 있습니다. 스니펫은 미리 정의된 텍스트와 사용자가 스니펫 세션 동안 대화식으로 텍스트를 변경/추가할 수 있는 위치("탭스탑, tabstops")가 포함된 템플릿입니다.

'mini.completion'에서 스니펫을 삽입하는 항목은 팝업창에 "S" 심볼이 표시됩니다. 스니펫을 실제로 삽입하려면:

- `<C-n>` / `<C-p>`를 통해 항목을 선택합니다. 시각적 떨림을 줄이기 위해 항목의 레이블(보통 전체 스니펫이 아님)이 먼저 삽입됩니다. LSP 서버가 항목에 대한 자체 정보를 제공하지 않는 경우 전체 스니펫 텍스트가 정보 창에 표시됩니다.
- `<C-y>`를 누르거나 키워드가 아닌 문자(예: `<CR>`; 입력된 문자는 제거됨)를 입력하려고 시도합니다. 그러면 이전 단계의 텍스트를 지우고, 커서를 설정한 다음 스니펫 텍스트와 함께 `lsp_completion.snippet_insert`를 호출합니다.
- 스니펫 삽입을 취소하고 자동 완성을 제대로 종료하려면 `<C-e>`를 누르세요.

삽입된 스니펫을 다루는 방법에 대한 개요는 [`:h MiniCompletion.default_snippet_insert()`](../doc/mini-completion.qmd#minicompletion.default_snippet_insert)를 참조하세요.

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

    | 브랜치 | 코드 스니펫                                                         |
    |--------|----------------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.completion')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.completion', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' library:

    | Branch | Code snippet                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- Standalone plugin:

    | Branch | Code snippet                                        |
    |--------|-----------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.completion', version = false },` |
    | Stable | `{ 'nvim-mini/mini.completion', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                               |
    |--------|------------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.completion'`                         |
    | Stable | `Plug 'nvim-mini/mini.completion', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.completion').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 특정 Neovim 이벤트와 동작 사이의 지연 시간 (ms 단위, 디바운스 타입).
  -- 매우 높은 지연 시간(예: 10^7)을 설정하여 특정 자동 동작을 
  -- (가상으로) 비활성화할 수 있습니다.
  delay = { completion = 100, info = 100, signature = 50 },

  -- 전용 창 설정:
  -- - `height` 및 `width`는 최대 크기입니다.
  -- - `border`는 테두리를 정의합니다 (`nvim_open_win()` 방식; 기본값 "single").
  window = {
    info = { height = 25, width = 80, border = nil },
    signature = { height = 25, width = 80, border = nil },
  },

  -- 모듈이 LSP 자동 완성을 수행하는 방식
  lsp_completion = {
    -- `source_func`는 'completefunc' 또는 'omnifunc' 중 하나여야 합니다.
    source_func = 'completefunc',

    -- `auto_setup`은 모든 `BufEnter` 이벤트에서 LSP 자동 완성을 
    -- 설정할지 여부를 나타내는 불리언 값입니다.
    auto_setup = true,

    -- LSP 'textDocument/completion' 응답 항목(각 항목은 해당 서버에 대한 
    -- `client_id` 필드를 가짐)과 자동 완성할 단어를 인자로 받는 함수입니다.
    -- 출력은 입력과 동일한 형태의 테이블이어야 합니다. 일반적인 용도는 
    -- 사용자 정의 필터링/정렬입니다. 기본값: `default_process_items`
    process_items = nil,

    -- 스니펫을 문자열로 받아 커서 위치에 삽입하는 함수입니다.
    -- 기본값: `default_snippet_insert`는 'mini.snippets' 사용을 시도하고 
    -- Neovim>=0.10에서는 `vim.snippet.expand`로 폴백합니다.
    snippet_insert = nil,
  },

  -- 함수 또는 문자열 형태의 폴백(fallback) 동작. Insert 모드에서 실행됩니다.
  -- 내장 자동 완성(`:h ins-completion`)을 사용하려면 해당 매핑을 
  -- 문자열로 설정하세요. 예: '전체 줄' 자동 완성의 경우 '<C-x><C-l>'.
  fallback_action = '<C-n>',

  -- 모듈 매핑. 비활성화하려면 `''`(빈 문자열)을 사용하세요. 
  -- 일부는 시스템 매핑과 충돌할 수 있습니다.
  mappings = {
    -- 2단계/폴백 자동 완성 강제 실행
    force_twostep = '<C-Space>',
    force_fallback = '<A-Space>',

    -- 정보/시그니처 창을 아래/위로 스크롤. 덮어쓸 때 팝업 메뉴용 
    -- 내장 키와 충돌하는지 확인하세요 (예: `source_func`이 
    -- 'completefunc'/'omnifunc'인 경우 `<C-u>`/`<C-o>`, 또는 `<C-n>`/`<C-p>`).
    scroll_down = '<C-f>',
    scroll_up = '<C-b>',
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [hrsh7th/nvim-cmp](https://github.com/hrsh7th/nvim-cmp)
- [Shougo/ddc.vim](https://github.com/Shougo/ddc.vim)
