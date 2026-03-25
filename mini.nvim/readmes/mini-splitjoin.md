---
title: "mini.splitjoin"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-splitjoin_readme.png?raw=true" alt="mini.splitjoin" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 인자(Arguments) 나누기 및 합치기

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-splitjoin.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-splitjoin)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-splitjoin.mp4?raw=true)

## 기능 {#features}

- 커서 아래의 인자들(허용된 구분자 사이의 괄호 안 영역)을 수정하는 매핑과 Lua 함수를 제공합니다.

  지원되는 액션:
    - 전환(Toggle) - 인자들이 한 줄에 있으면 나누고(split), 그렇지 않으면 합칩니다(join). 이 모듈의 핵심 기능입니다. 도움말의 [`MiniSplitjoin.toggle()`](../doc/mini-splitjoin.qmd#minisplitjoin.toggle)을 참조하세요.
    - 나누기(Split) - 모든 인자 구분자가 각각의 줄 끝에 오도록 만듭니다. 도움말의 [`MiniSplitjoin.split()`](../doc/mini-splitjoin.qmd#minisplitjoin.split)을 참조하세요.
    - 합치기(Join) - 모든 인자를 한 줄로 합칩니다. 도움말의 [`MiniSplitjoin.join()`](../doc/mini-splitjoin.qmd#minisplitjoin.join)을 참조하세요.

- 매핑은 노멀 모드에서 점 반복(dot-repeatable)이 가능하며, 비주얼 모드에서도 작동합니다.

- 인자 감지 방식을 커스터마이징할 수 있습니다 (도움말의 [`MiniSplitjoin.config.detect`](../doc/mini-splitjoin.qmd#minisplitjoin.config.detect) 참조):
    - 인자를 포함할 수 있는 괄호의 종류.
    - 인자를 구분할 수 있는 문자열.
    - 구분자를 찾을 때 제외할 영역 (중첩된 괄호나 따옴표 내부 등).

- 나누기와 합치기 각각에 대해 커스터마이징 가능한 pre 및 post 후크(hooks)를 제공합니다. 도움말의 [`MiniSplitjoin.config`](../doc/mini-splitjoin.qmd#minisplitjoin.config) 내 `split`과 `join` 항목을 참조하세요.

- 개선된 들여쓰기 개념을 사용하여 주석 내부에서도 작동합니다. 도움말의 [`MiniSplitjoin.get_indent_part()`](../doc/mini-splitjoin.qmd#minisplitjoin.get_indent_part)를 참조하세요.

- 특정 위치에서 나누기와 합치기를 수행하기 위한 저수준 Lua 함수를 제공합니다. 도움말의 [`MiniSplitjoin.split_at()`](../doc/mini-splitjoin.qmd#minisplitjoin.split_at) 및 [`MiniSplitjoin.join_at()`](../doc/mini-splitjoin.qmd#minisplitjoin.join_at)을 참조하세요.

참고:

- 인자 검색은 Lua 패턴(정규 표현식과 유사한 방식)을 사용하여 수행됩니다. 어느 정도의 오탐지(false positives)가 발생할 수 있습니다.

- 이 모듈은 주로 [`MiniSplitjoin.toggle()`](../doc/mini-splitjoin.qmd#minisplitjoin.toggle)을 중심으로 설계되었습니다. 만약 초기 나누기 위치들이 서로 다른 줄에 있다면, 먼저 합친 뒤에 나누기를 시도하세요.

- 비주얼 모드 선택 영역에 대해서도 액션을 수행할 수 있으며, 이는 주로 초기 영역 감지가 올바르지 않을 때를 대비한 안전책으로 제공됩니다. 이는 [`MiniSplitjoin.get_visual_region()`](../doc/mini-splitjoin.qmd#minisplitjoin.get_visual_region)을 사용하며, 선택 영역을 전체 괄호로 취급합니다 (`vi)`가 아닌 `va)`를 사용하세요).

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

    | 브랜치 | 코드 스니펫                                                        |
    |--------|---------------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.splitjoin')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.splitjoin', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                       |
    |--------|----------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.splitjoin', version = false },` |
    | Stable | `{ 'nvim-mini/mini.splitjoin', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                              |
    |--------|-----------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.splitjoin'`                         |
    | Stable | `Plug 'nvim-mini/mini.splitjoin', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.splitjoin').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 모듈 매핑. 비활성화하려면 `''`(빈 문자열)을 사용하세요.
  -- 노멀 모드와 비주얼 모드 모두에 생성됩니다.
  mappings = {
    toggle = 'gS',
    split = '',
    join = '',
  },

  -- 감지 옵션: 나누기/합치기가 수행될 위치
  detect = {
    -- 인자 영역을 감지하기 위한 Lua 패턴 배열.
    -- 기본값: { '%b()', '%b[]', '%b{}' }
    brackets = nil,

    -- 인자 구분자를 정의하는 문자열 Lua 패턴
    separator = ',',

    -- 구분자를 제외할 하위 영역 Lua 패턴 배열.
    -- 중첩된 괄호나 따옴표가 있는 경우에도 올바른 감지를 가능하게 합니다.
    -- 기본값: { '%b()', '%b[]', '%b{}', '%b""', "%b''" }
    exclude_regions = nil,
  },

  -- 나누기(Split) 옵션
  split = {
    hooks_pre = {},
    hooks_post = {},
  },

  -- 합치기(Join) 옵션
  join = {
    hooks_pre = {},
    hooks_post = {},
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [FooSoft/vim-argwrap](https://github.com/FooSoft/vim-argwrap)
- [AndrewRadev/splitjoin.vim](https://github.com/AndrewRadev/splitjoin.vim)
- [Wansmer/treesj](https://github.com/Wansmer/treesj)
