---
title: "mini.hues"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-hues_readme.png?raw=true" alt="mini.hues" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 설정 가능한 컬러 스킴(Color Scheme) 생성

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-hues.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-hues)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-hues.mp4?raw=true)

### 번들 컬러 스킴 (Bundled color schemes)

#### 사계절 (Four seasons)

- [`miniwinter`](../doc/mini-hues.qmd#miniwinter): 아주르(azure) 배경의 "얼음 겨울" 팔레트

<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-miniwinter-dark.png?raw=true"> <img alt="miniwinter dark" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-miniwinter-dark.png?raw=true" style="width: 45%"/> </a>
<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-miniwinter-light.png?raw=true"> <img alt="miniwinter light" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-miniwinter-light.png?raw=true" style="width: 45%"/> </a>

- [`minispring`](../doc/mini-hues.qmd#minispring): 녹색 배경의 "꽃핀 봄" 팔레트

<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-minispring-dark.png?raw=true"> <img alt="minispring dark" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-minispring-dark.png?raw=true" style="width: 45%"/> </a>
<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-minispring-light.png?raw=true"> <img alt="minispring light" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-minispring-light.png?raw=true" style="width: 45%"/> </a>

- [`minisummer`](../doc/mini-hues.qmd#minisummer): 갈색/노란색 배경의 "뜨거운 여름" 팔레트

<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-minisummer-dark.png?raw=true"> <img alt="minisummer dark" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-minisummer-dark.png?raw=true" style="width: 45%"/> </a>
<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-minisummer-light.png?raw=true"> <img alt="minisummer light" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-minisummer-light.png?raw=true" style="width: 45%"/> </a>

- [`miniautumn`](../doc/mini-hues.qmd#miniautumn): 보라색 배경의 "차분한 가을" 팔레트

<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-miniautumn-dark.png?raw=true"> <img alt="miniautumn dark" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-miniautumn-dark.png?raw=true" style="width: 45%"/> </a>
<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-miniautumn-light.png?raw=true"> <img alt="miniautumn light" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-miniautumn-light.png?raw=true" style="width: 45%"/> </a>

#### [`randomhue`](../doc/mini-hues.qmd#randomhue)

[`randomhue`](../doc/mini-hues.qmd#randomhue)는 같은 색조(hue)의 **무작위로 생성된** 배경과 전경 색상을 사용합니다 (색상은 `:colorscheme randomhue`를 호출할 때마다 변경됩니다):

<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_dark-purple.png?raw=true"> <img alt="Dark purple" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_dark-purple.png?raw=true" style="width: 45%"/> </a>
<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_light-purple.png?raw=true"> <img alt="Light purple" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_light-purple.png?raw=true" style="width: 45%"/> </a>

<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_dark-azure.png?raw=true"> <img alt="Dark azure" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_dark-azure.png?raw=true" style="width: 45%"/> </a>
<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_light-azure.png?raw=true"> <img alt="Light azure" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_light-azure.png?raw=true" style="width: 45%"/> </a>

<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_dark-green.png?raw=true"> <img alt="Dark green" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_dark-green.png?raw=true" style="width: 45%"/> </a>
<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_light-green.png?raw=true"> <img alt="Light green" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_light-green.png?raw=true" style="width: 45%"/> </a>

<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_dark-orange.png?raw=true"> <img alt="Dark orange" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_dark-orange.png?raw=true" style="width: 45%"/> </a>
<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_light-orange.png?raw=true"> <img alt="Light orange" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-randomhue_light-orange.png?raw=true" style="width: 45%"/> </a>

## 설정 예시 {#example-configurations}

```lua
-- 배경색과 전경색 선택
require('mini.hues').setup({ background = '#351721', foreground = '#cdc4c6' }) -- 빨강
require('mini.hues').setup({ background = '#361a0d', foreground = '#cdc5c1' }) -- 주황
require('mini.hues').setup({ background = '#2c2101', foreground = '#c9c6c0' }) -- 노랑
require('mini.hues').setup({ background = '#17280e', foreground = '#c4c8c2' }) -- 초록
require('mini.hues').setup({ background = '#002923', foreground = '#c0c9c7' }) -- 청록(cyan)
require('mini.hues').setup({ background = '#002734', foreground = '#c0c8cc' }) -- 아주르(azure)
require('mini.hues').setup({ background = '#19213a', foreground = '#c4c6cd' }) -- 파랑
require('mini.hues').setup({ background = '#2b1a33', foreground = '#c9c5cb' }) -- 보라

-- 비기본 색조(hue)의 개수 다르게 설정
require('mini.hues').setup({ background = '#002734', foreground = '#c0c8cc', n_hues = 6 })
require('mini.hues').setup({ background = '#002734', foreground = '#c0c8cc', n_hues = 4 })
require('mini.hues').setup({ background = '#002734', foreground = '#c0c8cc', n_hues = 2 })
require('mini.hues').setup({ background = '#002734', foreground = '#c0c8cc', n_hues = 0 })

-- 텍스트 채도(saturation) 다르게 설정
require('mini.hues').setup({ background = '#002734', foreground = '#c0c8cc', saturation = 'low' })
require('mini.hues').setup({ background = '#002734', foreground = '#c0c8cc', saturation = 'lowmedium' })
require('mini.hues').setup({ background = '#002734', foreground = '#c0c8cc', saturation = 'medium' })
require('mini.hues').setup({ background = '#002734', foreground = '#c0c8cc', saturation = 'mediumhigh' })
require('mini.hues').setup({ background = '#002734', foreground = '#c0c8cc', saturation = 'high' })

-- 강조색(accent color) 선택
require('mini.hues').setup({ background = '#002734', foreground = '#c0c8cc', accent = 'yellow' })
require('mini.hues').setup({ background = '#002734', foreground = '#c0c8cc', accent = 'blue' })
```

## 기능 {#features}

- 배경(background)과 전경(foreground) 두 가지 기본 색상을 설정해야 합니다. 이들의 명도 단계와 다른 비기본 색상들은 인간의 인지적으로 합리적인 범위 내에서 최대한 다르게 느껴지도록 계산됩니다.

- 커스터마이징 가능:
    - 비기본 색상에 사용되는 색조(hue)의 수 (0개에서 8개까지).
    - 채도 수준 ('low', 'lowmedium', 'medium', 'mediumhigh', 'high').
    - 일부 선택된 UI 요소에 사용되는 강조색(accent color).
    - 플러그인 통합 (빠른 시작을 위해 선택적으로 활성화 가능).

- 기본 색상을 위한 무작위 생성기. [`randomhue`](../doc/mini-hues.qmd#randomhue) 컬러 스킴에 사용됩니다.

- 컬러 스킴에 사용되는 팔레트를 계산하는 Lua 함수.

- 번들 컬러 스킴 제공. [bundled-color-schemes]()를 참조하세요.

지원되는 하이라이트 그룹:

- 모든 내장 UI 및 문법(syntax) 그룹.

- 내장 Neovim LSP 및 진단(diagnostic).

- Tree-sitter.

- LSP 시맨틱 토큰(semantic tokens).

- 플러그인 (명시적으로 정의되어 있거나 기본 하이라이트가 적절히 작동함이 확인됨):
    - [nvim-mini/mini.nvim](https://nvim-mini.org/mini.nvim)
    - [akinsho/bufferline.nvim](https://github.com/akinsho/bufferline.nvim)
    - [anuvyklack/hydra.nvim](https://github.com/anuvyklack/hydra.nvim)
    - [DanilaMihailov/beacon.nvim](https://github.com/DanilaMihailov/beacon.nvim)
    - [folke/lazy.nvim](https://github.com/folke/lazy.nvim)
    - [folke/noice.nvim](https://github.com/folke/noice.nvim)
    - [folke/snacks.nvim](https://github.com/folke/snacks.nvim)
    - [folke/todo-comments.nvim](https://github.com/folke/todo-comments.nvim)
    - [folke/trouble.nvim](https://github.com/folke/trouble.nvim)
    - [folke/which-key.nvim](https://github.com/folke/which-key.nvim)
    - [ggandor/leap.nvim](https://github.com/ggandor/leap.nvim)
    - [glepnir/dashboard-nvim](https://github.com/glepnir/dashboard-nvim)
    - [glepnir/lspsaga.nvim](https://github.com/glepnir/lspsaga.nvim)
    - [HiPhish/rainbow-delimiters.nvim](https://github.com/HiPhish/rainbow-delimiters.nvim)
    - [hrsh7th/nvim-cmp](https://github.com/hrsh7th/nvim-cmp)
    - [ibhagwan/fzf-lua](https://github.com/ibhagwan/fzf-lua)
    - [justinmk/vim-sneak](https://github.com/justinmk/vim-sneak)
    - [kevinhwang91/nvim-bqf](https://github.com/kevinhwang91/nvim-bqf)
    - [kevinhwang91/nvim-ufo](https://github.com/kevinhwang91/nvim-ufo)
    - [lewis6991/gitsigns.nvim](https://github.com/lewis6991/gitsigns.nvim)
    - [lukas-reineke/indent-blankline.nvim](https://github.com/lukas-reineke/indent-blankline.nvim)
    - [MeanderingProgrammer/render-markdown.nvim](https://github.com/MeanderingProgrammer/render-markdown.nvim)
    - [neoclide/coc.nvim](https://github.com/neoclide/coc.nvim)
    - [NeogitOrg/neogit](https://github.com/NeogitOrg/neogit)
    - [nvim-lualine/lualine.nvim](https://github.com/nvim-lualine/lualine.nvim)
    - [nvim-neo-tree/neo-tree.nvim](https://github.com/nvim-neo-tree/neo-tree.nvim)
    - [nvim-telescope/telescope.nvim](https://github.com/nvim-telescope/telescope.nvim)
    - [nvim-tree/nvim-tree.lua](https://github.com/nvim-tree/nvim-tree.lua)
    - [OXY2DEV/helpview.nvim](https://github.com/OXY2DEV/helpview.nvim)
    - [OXY2DEV/markview.nvim](https://github.com/OXY2DEV/markview.nvim)
    - [phaazon/hop.nvim](https://github.com/phaazon/hop.nvim)
    - [rcarriga/nvim-dap-ui](https://github.com/rcarriga/nvim-dap-ui)
    - [rcarriga/nvim-notify](https://github.com/rcarriga/nvim-notify)
    - [rlane/pounce.nvim](https://github.com/rlane/pounce.nvim)
    - [romgrk/barbar.nvim](https://github.com/romgrk/barbar.nvim)
    - [stevearc/aerial.nvim](https://github.com/stevearc/aerial.nvim)
    - [williamboman/mason.nvim](https://github.com/williamboman/mason.nvim)

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
    |--------|-----------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.hues')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.hues', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.hues', version = false },` |
    | Stable | `{ 'nvim-mini/mini.hues', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.hues'`                         |
    | Stable | `Plug 'nvim-mini/mini.hues', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 **`background`와 `foreground` 필드를 포함하여** `require('mini.hues').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- **필수** 베이스 컬러 ('#rrggbb' 16진수 문자열)
  background = nil,
  foreground = nil,

  -- 비기본 색상에 사용되는 색조(hue)의 수
  n_hues = 8,

  -- 채도(Saturation). 'low', 'lowmedium', 'medium', 'mediumhigh', 'high' 중 하나.
  saturation = 'medium',

  -- 강조색(Accent color). 'bg', 'fg', 'red', 'orange', 'yellow', 'green',
  -- 'cyan', 'azure', 'blue', 'purple' 중 하나.
  accent = 'bg',

  -- 플러그인 통합. `default = false`로 모든 통합을 비활성화할 수 있습니다.
  -- 개별 플러그인별로도 설정 가능합니다 (|MiniHues.config| 참조).
  plugins = { default = true },

  -- 특정 이벤트에 따라 하이라이트 그룹을 자동 조정할지 여부
  autoadjust = true,
}
```

## 유사한 플러그인 {#similar-plugins}

- [mini.base16](https://nvim-mini.org/mini.nvim/readmes/mini-base16)
