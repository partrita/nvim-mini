---
title: "mini.align"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-align_readme.png?raw=true" alt="mini.align" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 대화형 텍스트 정렬

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-align.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-align)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-align.mp4?raw=true)

## 기능 {#features}

- 정렬은 크게 세 단계로 진행됩니다:
    - **분리(Split)**: Lua 패턴 또는 사용자 정의 규칙을 기반으로 줄을 여러 부분으로 나눕니다.
    - **정렬(Justify)**: 열 내에서 특정 측면의 너비가 같아지도록 각 부분을 조정합니다.
    - **병합(Merge)**: 커스터마이징 가능한 구분자를 사용하여 각 부분을 다시 하나의 줄로 합칩니다.

    각 주요 단계 전에는 고도로 커스터마이징된 결과를 얻기 위한 다른 단계(사전 단계, pre-steps)가 올 수 있습니다. [`:h MiniAlign.config`](../doc/mini-align.qmd#minialign.config)의 `steps` 값을 참조하세요. 자세한 내용은 [`:h MiniAlign-glossary`](../doc/mini-align.qmd#minialign-glossary) 및 [`:h MiniAlign-algorithm`](../doc/mini-align.qmd#minialign-algorithm)을 확인하세요.
- 사용자는 커스터마이징 가능한 수식어(정렬 단계나 옵션이 어떻게 변경되어야 하는지 나타내는 단일 키)를 눌러 정렬을 대화식으로 제어할 수 있습니다. 기본 수식어의 일부:
    - `s`: 분리(Split)할 Lua 패턴을 입력합니다.
    - `j`: 사용 가능한 정렬 방식("left", "center", "right", "none") 중에서 선택합니다.
    - `m`: 병합(Merge) 구분자를 입력합니다.
    - `f`: 영향을 받을 부분을 구성하기 위한 필터 Lua 표현식을 입력합니다 (예: "첫 번째 열만 정렬").
    - `i`: 일반적으로 원치 않는 일부 분리 일치를 무시합니다.
    - `p`: 인접한 부분을 쌍으로 묶어 함께 정렬합니다.
    - `t`: 각 부분의 공백을 제거(Trim)합니다.
    - `<BS>` (백스페이스): 마지막 사전 단계를 삭제합니다.

    자세한 내용은 [`:h MiniAlign-modifiers-builtin`](../doc/mini-align.qmd#minialign-modifiers-builtin) 및 [`:h MiniAlign-examples`](../doc/mini-align.qmd#minialign-examples)를 참조하세요.
- 정렬은 실시간 미리보기(수식어를 누를 때마다 결과가 업데이트됨)를 사용하거나 사용하지 않고 수행할 수 있습니다.
- 모든 사용자 상호작용에는 현재 정렬 프로세스에 대한 관련 정보를 보여주는 도움말 상태 메시지가 동반됩니다.

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
    | Main   | `add('nvim-mini/mini.align')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.align', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.align', version = false },` |
    | Stable | `{ 'nvim-mini/mini.align', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.align'`                         |
    | Stable | `Plug 'nvim-mini/mini.align', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.align').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 모듈 매핑. 비활성화하려면 `''`(빈 문자열)을 사용하세요.
  mappings = {
    start = 'ga',
    start_with_preview = 'gA',
  },

  -- 정렬 단계 및/또는 옵션을 변경하는 수식어(Modifiers)
  modifiers = {
    -- 주요 옵션 수식어
    ['s'] = --<함수: 분리 패턴 입력>,
    ['j'] = --<함수: 정렬 측면 선택>,
    ['m'] = --<함수: 병합 구분자 입력>,

    -- 사전 단계를 추가하는 수식어
    ['f'] = --<함수: Lua 표현식을 입력하여 부분 필터링>,
    ['i'] = --<함수: 일부 분리 일치 무시>,
    ['p'] = --<함수: 부분 쌍 구성>,
    ['t'] = --<함수: 부분 트리밍>,

    -- 마지막 사전 단계 삭제
    ['<BS>'] = --<함수: 마지막 사전 단계 삭제>,

    -- 일반적인 분리에 대한 특수 구성
    ['='] = --<함수: '='에 대해 강화된 설정>,
    [','] = --<함수: ','에 대해 강화된 설정>,
    ['|'] = --<함수: '|'에 대해 강화된 설정>,
    [' '] = --<함수: ' '에 대해 강화된 설정>,
  },

  -- 정렬 프로세스를 제어하는 기본 옵션
  options = {
    split_pattern = '',
    justify_side = 'left',
    merge_delimiter = '',
  },

  -- 정렬을 수행하는 기본 단계 (`nil`인 경우 기본값 사용)
  steps = {
    pre_split = {},
    split = nil,
    pre_justify = {},
    justify = nil,
    pre_merge = {},
    merge = nil,
  },

  -- 에러가 아닌 피드백 표시 여부
  -- 사용자 입력이 필요한 경우 유휴 시간 후에 표시되는 (순수 정보성) 헬퍼 메시지에도 영향을 미칩니다.
  silent = false,
}
```

## 유사한 플러그인 {#similar-plugins}

- [junegunn/vim-easy-align](https://github.com/junegunn/vim-easy-align)
- [godlygeek/tabular](https://github.com/godlygeek/tabular)
- [tommcdo/vim-lion](https://github.com/tommcdo/vim-lion)
- [Vonr/align.nvim](https://github.com/Vonr/align.nvim)
