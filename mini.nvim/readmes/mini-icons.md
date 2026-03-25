---
title: "mini.icons"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-icons_readme.png?raw=true" alt="mini.icons" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 아이콘 제공자 (Icon provider)

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-icons.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-icons)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![demo-icons_glyph-dark](https://github.com/nvim-mini/assets/blob/main/demo/demo-icons_glyph-dark.png?raw=true)

![demo-icons_ascii](https://github.com/nvim-mini/assets/blob/main/demo/demo-icons_ascii.png?raw=true)

![demo-icons_glyph-light](https://github.com/nvim-mini/assets/blob/main/demo/demo-icons_glyph-light.png?raw=true)

## 기능 {#features}

- 단일 함수 [`MiniIcons.get()`](../doc/mini-icons.qmd#miniicons.get)을 통해 다양한 카테고리(파일 타입, 파일/디렉터리 경로, 확장자, 운영 체제, LSP 종류 값)에 대한 아이콘과 하이라이팅을 제공합니다. 아이콘 및 카테고리 기본값을 덮어쓸 수 있습니다.

- 커스터마이징 가능한 스타일: "glyph" (아이콘 글리프 사용) 또는 "ascii" (글리프 미지원 환경용 대체 텍스트).

- 컬러 스킴과 더 잘 어우러지도록 고정된 하이라이트 그룹 세트(기본적으로 내장 그룹에 연결됨)를 사용합니다.

- 성능 극대화를 위한 캐싱 기능.

- `vim.filetype.add()` 및 `vim.filetype.match()`와 통합됩니다.

- 'mini.nvim' 외부의 플러그인과 더 잘 통합되도록 'nvim-tree/nvim-web-devicons'의 메서드를 모킹(mocking)할 수 있습니다. [`:h MiniIcons.mock_nvim_web_devicons()`](../doc/mini-icons.qmd#miniicons.mock_nvim_web_devicons)를 참조하세요.

- 아이콘을 포함하도록 내장 "LSP 종류(LSP kind)" 맵을 조정할 수 있습니다. 특히, 이를 통해 ['mini.completion'](https://nvim-mini.org/mini.nvim/readmes/mini-completion)이 LSP 단계에서 아이콘을 사용할 수 있게 됩니다. [`:h MiniIcons.tweak_lsp_kind()`](../doc/mini-icons.qmd#miniicons.tweak_lsp_kind)를 참조하세요.

참고:

- 가능한 모든 사용 사례의 아이콘을 수집하는 것이 목표는 아닙니다. 각 카테고리에 내장 아이콘 데이터로 포함되기 위한 구체적인 기준이 있습니다 ([`:h MiniIcons.get()`](../doc/mini-icons.qmd#miniicons.get) 참조). 주로 지원되는 카테고리는 "filetype"입니다.

'mini.icons'를 의존성으로 사용하는 플러그인 작성자를 위한 권장 사항:

- `_G.MiniIcons` 테이블이 있는지 확인하고(사용자가 'mini.icons'를 명시적으로 활성화했음을 의미), 있는 경우에만 아이콘을 제공하세요.

- [`MiniIcons.get()`](../doc/mini-icons.qmd#miniicons.get) 함수를 사용하여 아이콘 문자열과 관련 데이터를 가져오세요.

- 파일 아이콘의 경우 상대 경로 또는 파일 이름(basename)만 사용하는 것보다 전체 경로를 사용하는 것을 권장합니다. 경로가 부모 디렉터리가 포함된 패턴과 일치할 때 결과가 달라질 수 있기 때문입니다. [`:h MiniIcons.config`](../doc/mini-icons.qmd#miniicons.config)에 관련 예제가 있습니다.

## 의존성 {#dependencies}

권장 의존성:

- 특수 utf8 글리프 표시를 지원하는 터미널 에뮬레이터 (가급적으로 "overflow" 뷰 지원 - 한 칸이 아닌 두 칸에 걸쳐 표시하는 기능). 대부분의 현대적인 터미널 에뮬레이터(WezTerm, Kitty, Alacritty, iTerm2, Ghostty)는 이를 기본으로 지원합니다.

  "overflow" 기능이 없으면 아이콘이 조금 작게 표시될 뿐입니다. 하지만 특수 utf8 글리프 표시 자체를 지원하지 않으면 아이콘 글리프 대신 알 수 없는 기호(또는 물음표 상자)가 표시됩니다.

- 버전 3.0.0 이상의 [Nerd Fonts](https://www.nerdfonts.com) 아이콘(특히 `nf-md-*` 클래스)을 지원하는 폰트.
  이는 Nerd Fonts 아이콘으로 패치된 폰트를 사용하거나, 메인 폰트에서 지원하지 않는 글리프에 대해 [`NerdFontsSymbolsOnly`](https://github.com/ryanoasis/nerd-fonts/releases) 폰트를 대체(fallback) 폰트로 설정하여 터미널 에뮬레이터 수준에서 구성해야 합니다.

아이콘 지원이 가능한 터미널이나 폰트 사용이 불가능한 경우, `config.style = 'ascii'`를 사용하세요. 시각적으로는 덜 화려하지만 글리프가 아닌 아이콘 세트를 사용할 수 있습니다.

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

    | 브랜치 | 코드 스니펫                                                    |
    |--------|-----------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.icons')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.icons', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                   |
    |--------|------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.icons', version = false },` |
    | Stable | `{ 'nvim-mini/mini.icons', version = '*' },   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                          |
    |--------|-------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.icons'`                         |
    | Stable | `Plug 'nvim-mini/mini.icons', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.icons').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 아이콘 스타일: 'glyph' 또는 'ascii'
  style = 'glyph',

  -- 카테고리별 커스터마이징. 자세한 내용은 [`:h MiniIcons.config`](../doc/mini-icons.qmd#miniicons.config) 참조.
  default   = {},
  directory = {},
  extension = {},
  file      = {},
  filetype  = {},
  lsp       = {},
  os        = {},

  -- "file" 해결 시 고려할 확장자를 제어하는 함수
  use_file_extension = function(ext, file) return true end,
}
```

## 유사한 플러그인 {#similar-plugins}

- [nvim-tree/nvim-web-devicons](https://github.com/nvim-tree/nvim-web-devicons)
- [onsails/lspkind.nvim](https://github.com/onsails/lspkind.nvim)
---
title: "mini.icons"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-icons_readme.png?raw=true" alt="mini.icons" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 아이콘 제공자 (Icon provider)

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-icons.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-icons)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![demo-icons_glyph-dark](https://github.com/nvim-mini/assets/blob/main/demo/demo-icons_glyph-dark.png?raw=true)

![demo-icons_ascii](https://github.com/nvim-mini/assets/blob/main/demo/demo-icons_ascii.png?raw=true)

![demo-icons_glyph-light](https://github.com/nvim-mini/assets/blob/main/demo/demo-icons_glyph-light.png?raw=true)

## 기능 {#features}

- 단일 함수 [`MiniIcons.get()`](../doc/mini-icons.qmd#miniicons.get)을 통해 다양한 카테고리(파일 타입, 파일/디렉터리 경로, 확장자, 운영 체제, LSP 종류 값)에 대한 아이콘과 하이라이팅을 제공합니다. 아이콘 및 카테고리 기본값을 덮어쓸 수 있습니다.

- 커스터마이징 가능한 스타일: "glyph" (아이콘 글리프 사용) 또는 "ascii" (글리프 미지원 환경용 대체 텍스트).

- 컬러 스킴과 더 잘 어우러지도록 고정된 하이라이트 그룹 세트(기본적으로 내장 그룹에 연결됨)를 사용합니다.

- 성능 극대화를 위한 캐싱 기능.

- `vim.filetype.add()` 및 `vim.filetype.match()`와 통합됩니다.

- 'mini.nvim' 외부의 플러그인과 더 잘 통합되도록 'nvim-tree/nvim-web-devicons'의 메서드를 모킹(mocking)할 수 있습니다. [`:h MiniIcons.mock_nvim_web_devicons()`](../doc/mini-icons.qmd#miniicons.mock_nvim_web_devicons)를 참조하세요.

- 아이콘을 포함하도록 내장 "LSP 종류(LSP kind)" 맵을 조정할 수 있습니다. 특히, 이를 통해 ['mini.completion'](https://nvim-mini.org/mini.nvim/readmes/mini-completion)이 LSP 단계에서 아이콘을 사용할 수 있게 됩니다. [`:h MiniIcons.tweak_lsp_kind()`](../doc/mini-icons.qmd#miniicons.tweak_lsp_kind)를 참조하세요.

참고:

- 가능한 모든 사용 사례의 아이콘을 수집하는 것이 목표는 아닙니다. 각 카테고리에 내장 아이콘 데이터로 포함되기 위한 구체적인 기준이 있습니다 ([`:h MiniIcons.get()`](../doc/mini-icons.qmd#miniicons.get) 참조). 주로 지원되는 카테고리는 "filetype"입니다.

'mini.icons'를 의존성으로 사용하는 플러그인 작성자를 위한 권장 사항:

- `_G.MiniIcons` 테이블이 있는지 확인하고(사용자가 'mini.icons'를 명시적으로 활성화했음을 의미), 있는 경우에만 아이콘을 제공하세요.

- [`MiniIcons.get()`](../doc/mini-icons.qmd#miniicons.get) 함수를 사용하여 아이콘 문자열과 관련 데이터를 가져오세요.

- 파일 아이콘의 경우 상대 경로 또는 파일 이름(basename)만 사용하는 것보다 전체 경로를 사용하는 것을 권장합니다. 경로가 부모 디렉터리가 포함된 패턴과 일치할 때 결과가 달라질 수 있기 때문입니다. [`:h MiniIcons.config`](../doc/mini-icons.qmd#miniicons.config)에 관련 예제가 있습니다.

## 의존성 {#dependencies}

권장 의존성:

- 특수 utf8 글리프 표시를 지원하는 터미널 에뮬레이터 (가급적으로 "overflow" 뷰 지원 - 한 칸이 아닌 두 칸에 걸쳐 표시하는 기능). 대부분의 현대적인 터미널 에뮬레이터(WezTerm, Kitty, Alacritty, iTerm2, Ghostty)는 이를 기본으로 지원합니다.

  "overflow" 기능이 없으면 아이콘이 조금 작게 표시될 뿐입니다. 하지만 특수 utf8 글리프 표시 자체를 지원하지 않으면 아이콘 글리프 대신 알 수 없는 기호(또는 물음표 상자)가 표시됩니다.

- 버전 3.0.0 이상의 [Nerd Fonts](https://www.nerdfonts.com) 아이콘(특히 `nf-md-*` 클래스)을 지원하는 폰트.
  이는 Nerd Fonts 아이콘으로 패치된 폰트를 사용하거나, 메인 폰트에서 지원하지 않는 글리프에 대해 [`NerdFontsSymbolsOnly`](https://github.com/ryanoasis/nerd-fonts/releases) 폰트를 대체(fallback) 폰트로 설정하여 터미널 에뮬레이터 수준에서 구성해야 합니다.

아이콘 지원이 가능한 터미널이나 폰트 사용이 불가능한 경우, `config.style = 'ascii'`를 사용하세요. 시각적으로는 덜 화려하지만 글리프가 아닌 아이콘 세트를 사용할 수 있습니다.

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

    | 브랜치 | 코드 스니펫                                                    |
    |--------|-----------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.icons')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.icons', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                   |
    |--------|------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.icons', version = false },` |
    | Stable | `{ 'nvim-mini/mini.icons', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                          |
    |--------|-------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.icons'`                         |
    | Stable | `Plug 'nvim-mini/mini.icons', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.icons').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 아이콘 스타일: 'glyph' 또는 'ascii'
  style = 'glyph',

  -- 카테고리별 커스터마이징. 자세한 내용은 [`:h MiniIcons.config`](../doc/mini-icons.qmd#miniicons.config) 참조.
  default   = {},
  directory = {},
  extension = {},
  file      = {},
  filetype  = {},
  lsp       = {},
  os        = {},

  -- "file" 해결 시 고려할 확장자를 제어하는 함수
  use_file_extension = function(ext, file) return true end,
}
```

## 유사한 플러그인 {#similar-plugins}

- [nvim-tree/nvim-web-devicons](https://github.com/nvim-tree/nvim-web-devicons)
- [onsails/lspkind.nvim](https://github.com/onsails/lspkind.nvim)
