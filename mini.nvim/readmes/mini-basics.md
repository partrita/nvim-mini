---
title: "mini.basics"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-basics_readme.png?raw=true" alt="mini.basics" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 공통 설정 프리셋

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-basics.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-basics)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-basics.mp4?raw=true)

## 기능 {#features}

- 일반적인 옵션들에 대한 프리셋을 제공합니다. 이전에 수동으로 설정되지 않은 경우에만 옵션을 변경합니다. 자세한 내용은 [`:h MiniBasics.config.options`](../doc/mini-basics.qmd#minibasics.config.options)를 참조하세요.
- 일반적인 매핑들에 대한 프리셋을 제공합니다. 이전에 수동으로 생성되지 않은 경우에만 매핑을 추가합니다. 자세한 내용은 [`:h MiniBasics.config.mappings`](../doc/mini-basics.qmd#minibasics.config.mappings)를 참조하세요.
- 일반적인 자동 명령(autocommands)들에 대한 프리셋을 제공합니다. 자세한 내용은 [`:h MiniBasics.config.autocommands`](../doc/mini-basics.qmd#minibasics.config.autocommands)를 참조하세요.
- 하위 호환성을 최우선으로 생각합니다. 기존 동작을 변경하려는 모든 결정은 매우 신중하게 이루어집니다.

참고:

- 이 모듈의 주요 목표는 Neovim 초보 사용자들에게 더 나은 "즉시 사용 가능(works out of the box)"한 경험을 제공하는 동시에, 학습할 만한 관련 옵션/매핑/자동 명령을 문서화하여 제공하는 것입니다. 이는 Neovim 사용자들을 대상으로 한 설문 조사와 개인적인 선호도를 기반으로 합니다.
- 하지만 숙련된 사용자들도 유용한 기능을 찾을 수 있을 것입니다.
- 그럼에도 불구하고, 사용된 옵션/매핑/자동 명령에 대해 읽어보고 자신에게 필요한지 결정하는 것이 권장됩니다. 이를 위한 주된 방법은 Neovim의 도움말 페이지(도움말 파일에 링크됨)와 이 모듈의 소스 코드(이해를 돕기 위해 상세히 문서화됨)를 읽는 것입니다.

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
    | Main   | `add('nvim-mini/mini.basics')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.basics', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.basics', version = false },` |
    | Stable | `{ 'nvim-mini/mini.basics', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.basics'`                         |
    | Stable | `Plug 'nvim-mini/mini.basics', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.basics').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 옵션. 필드를 `false`로 설정하면 비활성화됩니다.
  options = {
    -- 기본 옵션 ('number', 'ignorecase' 등 다수)
    basic = true,

    -- 추가 UI 기능 ('winblend', 'listchars', 'pumheight' 등)
    extra_ui = false,

    -- 창 테두리 프리셋 ('single', 'double' 등)
    -- 기본값 'auto'는 'winborder' 옵션에서 유추합니다.
    win_borders = 'auto',
  },

  -- 매핑. 필드를 `false`로 설정하면 비활성화됩니다.
  mappings = {
    -- 기본 매핑 (개선된 'jk', Ctrl+S로 저장 등)
    basic = true,

    -- 공통 옵션('wrap', 'spell' 등)을 토글하는 매핑의 접두사.
    -- 이러한 매핑을 생성하지 않으려면 빈 문자열을 입력하세요.
    option_toggle_prefix = [[\]],

    -- <C-hjkl>로 창 탐색, <C-arrow>로 크기 조정
    windows = false,

    -- Insert, Command, Terminal 모드에서 <M-hjkl>로 커서 이동
    move_with_alt = false,
  },

  -- 자동 명령. 필드를 `false`로 설정하면 비활성화됩니다.
  autocommands = {
    -- 기본 자동 명령 (yank 시 하이라이트, 터미널에서 Insert 모드 시작 등)
    basic = true,

    -- 줄 단위 및 블록 단위 비주얼 모드에서만 'relativenumber' 설정
    relnum_in_visual_mode = false,
  },

  -- 에러가 아닌 피드백 표시 여부
  silent = false,
}
```

## 유사한 플러그인 {#similar-plugins}

- [tpope/vim-sensible](https://github.com/tpope/vim-sensible)
- [tpope/vim-unimpaired](https://github.com/tpope/vim-unimpaired)
