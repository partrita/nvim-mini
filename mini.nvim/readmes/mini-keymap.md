---
title: "mini.keymap"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-keymap_readme.png?raw=true" alt="mini.keymap" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 특수 키 매핑

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-keymap.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-keymap)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-keymap.mp4?raw=true)

## 기능 {#features}

- 설정 가능한 다단계 액션을 수행하도록 키를 매핑합니다: 첫 번째 단계의 조건이 참이면 해당 액션을 실행하고, 그렇지 않으면 두 번째 단계를 확인하는 식으로 진행하다가 마지막에는 원래 키를 실행합니다. 이는 주로 "스마트(smart)" 키(예: "smart tab")라고 불립니다. [`:h MiniKeymap.map_multistep()`](../doc/mini-keymap.qmd#minikeymap.map_multistep)을 참조하세요.

  포커스된 입력(Insert) 모드 매핑을 위해 `<Tab>`, `<S-Tab>`, `<CR>`, `<BS>`와 같은 특수 키를 위한 다양한 내장 단계들을 제공합니다:
  - 내장 입력 모드 보완(completion) 탐색 및 수락. [mini.completion](https://nvim-mini.org/mini.nvim/readmes/mini-completion)에 유용합니다.
  - [mini.snippets](https://nvim-mini.org/mini.nvim/readmes/mini-snippets) 탐색 및 확장.
  - [mini.pairs](https://nvim-mini.org/mini.nvim/readmes/mini-pairs)를 고려한 `<CR>` 및 `<BS>` 실행.
  - 현재 Tree-sitter 노드 이전/이후로 점프.
  - 여는 문자와 닫는 문자(괄호 및 따옴표) 앞뒤로 점프.
  - 커서가 들여쓰기 내부에 있을 때 들여쓰기 늘리기/줄이기.
  - 왼쪽의 모든 공백 삭제 ("hungry backspace").
  - 내장 스니펫 엔진 탐색 (`:h vim.snippet`).
  - [hrsh7th/nvim-cmp](https://github.com/hrsh7th/nvim-cmp) 보완 탐색 및 수락.
  - [Saghen/blink.cmp](https://github.com/Saghen/blink.cmp) 보완 탐색 및 수락.
  - [L3MON4D3/LuaSnip](https://github.com/L3MON4D3/LuaSnip) 스니펫 탐색 및 확장.
  - [windwp/nvim-autopairs](https://github.com/windwp/nvim-autopairs)를 고려한 `<CR>` 및 `<BS>` 실행.

- 키를 "콤보(combo)"로 매핑합니다: 각 키는 즉시 작동함과 동시에, 설정된 시간 내에 모든 키가 입력되면 추가 액션을 실행합니다. [`:h MiniKeymap.map_combo()`](../doc/mini-keymap.qmd#minikeymap.map_combo)를 참조하세요.

  일반적인 사용 사례는 다음과 같습니다:
    - 입력 및 커맨드 라인 모드에서 노멀 모드로 나가기 위해 입력 가능한 키(예: "jk", "kj") 매핑.
    - 동일한 이동 키를 연달아 너무 많이 누르는 나쁜 습관을 방지하기 위해 알림 표시.

더 자세한 정보는 다음을 참조하세요:

- [`:h MiniKeymap-examples`](../doc/mini-keymap.qmd#minikeymap-examples)

## 빠른 시작 {#quickstart}

### 다단계 (Multi-step)

'mini.completion' 및 'mini.pairs'와 잘 어울리는 설정:

```lua
local map_multistep = require('mini.keymap').map_multistep

map_multistep('i', '<Tab>',   { 'pmenu_next' })
map_multistep('i', '<S-Tab>', { 'pmenu_prev' })
map_multistep('i', '<CR>',    { 'pmenu_accept', 'minipairs_cr' })
map_multistep('i', '<BS>',    { 'minipairs_bs' })
```

### 콤보 (Combos)

`<Esc>` 키까지 손을 뻗지 않고도 노멀 모드로 나가는 "더 나은 이스케이프":

```lua
local map_combo = require('mini.keymap').map_combo

-- 대부분의 일반 모드 지원. 't'를 포함할 수도 있지만,
-- 터미널 내부에서 `<Esc>`를 누르는 것만을 의미하게 됩니다.
local mode = { 'i', 'c', 'x', 's' }
map_combo(mode, 'jk', '<BS><BS><Esc>')

-- 키 순서에 신경 쓰지 않도록 "kj"도 매핑
map_combo(mode, 'kj', '<BS><BS><Esc>')

-- 터미널 모드에서 노멀 모드로 탈출
map_combo('t', 'jk', '<BS><BS><C-\\><C-n>')
map_combo('t', 'kj', '<BS><BS><C-\\><C-n>')
```

동일한 키를 반복하여 너무 많이 움직일 때 알림 표시:

```lua
local notify_many_keys = function(key)
  local lhs = string.rep(key, 5)
  local action = function() vim.notify('Too many ' .. key) end
  require('mini.keymap').map_combo({ 'n', 'x' }, lhs, action)
end
notify_many_keys('h')
notify_many_keys('j')
notify_many_keys('k')
notify_many_keys('l')
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

    | 브랜치 | 코드 스니펫                                                     |
    |--------|------------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.keymap')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.keymap', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                    |
    |--------|-------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.keymap', version = false },` |
    | Stable | `{ 'nvim-mini/mini.keymap', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                           |
    |--------|--------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.keymap'`                         |
    | Stable | `Plug 'nvim-mini/mini.keymap', { 'branch': 'stable' }` |

</details>

**중요**: `require('mini.keymap').setup()`을 반드시 호출할 필요는 없으나, 사용 편의성을 높이기 위해 호출할 수 있습니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{}
```

## 유사한 플러그인 {#similar-plugins}

- [max397574/better-escape.nvim](https://github.com/max397574/better-escape.nvim)
- [abecodes/tabout.nvim](https://github.com/abecodes/tabout.nvim)
