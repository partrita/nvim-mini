---
title: "mini.base16"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-base16_readme.png?raw=true" alt="mini.base16" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 수동으로 제공된 팔레트를 위한 [chriskempson/base16](https://github.com/chriskempson/base16) 테마의 빠른 구현

- 30개 이상의 플러그인 연동을 지원합니다.
- 배경색과 전경색만 있으면 되는 독특한 팔레트 생성기를 갖추고 있습니다.
- 엄선된 몇 가지 테마가 기본으로 포함되어 있습니다.

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-base16.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-base16)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

[`minischeme`](../doc/mini-base16.qmd#minischeme) 컬러 스킴 사용 시:

<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-base16_minischeme-dark.png?raw=true"> <img alt="minischeme dark" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-base16_minischeme-dark.png?raw=true" style="width: 45%"/> </a>
<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-base16_minischeme-light.png?raw=true"> <img alt="minischeme light" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-base16_minischeme-light.png?raw=true" style="width: 45%"/> </a>

[`minicyan`](../doc/mini-base16.qmd#minicyan) 컬러 스킴 사용 시:

<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-base16_minicyan-dark.png?raw=true"> <img alt="minicyan dark" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-base16_minicyan-dark.png?raw=true" style="width: 45%"/> </a>
<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-base16_minicyan-light.png?raw=true"> <img alt="minicyan light" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-base16_minicyan-light.png?raw=true" style="width: 45%"/> </a>

## 기능 {#features}

지원되는 하이라이트 그룹:

- 내장 Neovim LSP 및 진단.
- 플러그인 (직접 정의되거나 기본 하이라이트가 적절히 작동함을 확인한 플러그인):
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
    - [ggandor/lightspeed.nvim](https://github.com/ggandor/lightspeed.nvim)
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

    | 브랜치 | 코드 스니펫                                                     |
    |--------|------------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.base16')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.base16', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.base16', version = false },` |
    | Stable | `{ 'nvim-mini/mini.base16', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.base16'`                         |
    | Stable | `Plug 'nvim-mini/mini.base16', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 적절한 `palette`와 함께 `require('mini.base16').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
{
  -- `base00`에서 `base0F`까지의 이름을 필드로, "#RRGGBB" 형식의 
  -- HEX 색상 문자열을 값으로 가지는 테이블입니다. 참고: 이는 `setup()`에서 
  -- 명시적으로 제공되어야 합니다.
  palette = nil,

  -- cterm 색상 지원 여부. 불리언(boolean), `nil`(`false`와 동일), 
  -- 또는 cterm 색상 테이블이 될 수 있습니다. 자세한 내용은 `setup()` 
  -- 문서를 참조하세요.
  use_cterm = nil,

  -- 플러그인 연동. 모든 연동을 비활성화하려면 `default = false`를 사용하세요.
  -- 플러그인별로 설정할 수도 있습니다 (|MiniBase16.config| 참조).
  plugins = { default = true },
}
```

## 유사한 플러그인 {#similar-plugins}

- [chriskempson/base16-vim](https://github.com/chriskempson/base16-vim)
