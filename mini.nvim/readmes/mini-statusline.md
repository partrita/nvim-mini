---
title: "mini.statusline"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-statusline_readme.png?raw=true" alt="mini.statusline" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 세련된 기본 외관을 갖춘 최소한의 빠른 상태 표시줄(Statusline) 모듈

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-statusline.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-statusline)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-statusline.mp4?raw=true)

## 기능 {#features}

- 활성 및 비활성 창에 대해 고유한 상태 표시줄 구조를 정의합니다. 이는 |statusline|에 적합한 문자열을 반환하는 함수를 통해 이루어집니다. 해당 코드는 다음과 같은 구조를 가진 기본 코드와 유사해야 합니다:
    - 표시하려는 각 섹션에 대한 문자열 데이터를 계산합니다.
    - [`MiniStatusline.combine_groups()`](../doc/mini-statusline.qmd#ministatusline.combine_groups)를 사용하여 그룹으로 결합합니다.
- 색상과 함께 현재 모드를 표시하는 기본 인디케이터를 포함합니다.
- 창의 너비가 너무 좁을 경우 섹션에서 일부 정보를 숨길 수 있습니다 (각 섹션별로 숨김 기준이 되는 창 너비를 설정할 수 있습니다).

## 의존성 {#dependencies}

완전한 경험을 위해 필요합니다 (아래 도구들이 없어도 여전히 작동합니다):

- 파일 형식 아이콘을 표시하기 위한 [Nerd font](https://www.nerdfonts.com/) 및 활성화된 ['mini.icons'](https://nvim-mini.org/mini.nvim/readmes/mini-icons) 모듈. [nvim-tree/nvim-web-devicons](https://github.com/nvim-tree/nvim-web-devicons) 플러그인으로 대체할 수도 있습니다.

- Git 및 diff 관련 정보를 표시하기 위해 활성화된 ['mini.git'](https://nvim-mini.org/mini.nvim/readmes/mini-git) 및 ['mini.diff'](https://nvim-mini.org/mini.nvim/readmes/mini-diff) 모듈. [lewis6991/gitsigns.nvim](https://github.com/lewis6991/gitsigns.nvim) 플러그인으로 대체할 수도 있습니다.

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
    | Main   | `add('nvim-mini/mini.statusline')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.statusline', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                        |
    |--------|-----------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.statusline', version = false },` |
    | Stable | `{ 'nvim-mini/mini.statusline', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.statusline'`                         |
    | Stable | `Plug 'nvim-mini/mini.statusline', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.statusline').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 상태 표시줄 문자열을 반환하는 함수들을 통해 상태 표시줄 콘텐츠를 성정합니다.
  -- `:h statusline` 및 기본 콘텐츠 코드를 참조하세요 (`nil` 대신 사용됨).
  content = {
    -- 활성 창용 콘텐츠
    active = nil,
    -- 비활성 창용 콘텐츠
    inactive = nil,
  },

  -- 기본적으로 아이콘을 사용할지 여부
  use_icons = true,
}
```

## 유사한 플러그인 {#similar-plugins}

- [nvim-lualine/lualine.nvim](https://github.com/nvim-lualine/lualine.nvim)
