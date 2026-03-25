---
title: "mini.operators"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-operators_readme.png?raw=true" alt="mini.operators" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 텍스트 편집 연산자(Operators)

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-operators.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-operators)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-operators.mp4?raw=true)

## 기능 {#features}

- 연산자(Operators):
    - 텍스트를 평가(Evaluate)하고 출력값으로 교체합니다.
    - 텍스트 영역을 서로 교환(Exchange)합니다.
    - 텍스트를 배가(Multiply, 복제)합니다.
    - 텍스트를 레지스터 내용으로 교체(Replace)합니다.
    - 텍스트를 정렬(Sort)합니다.

- 텍스트 오브젝트, 줄, 선택 영역에서 작동하도록 구성 가능한 매핑을 자동으로 수행합니다. 더 세밀한 제어를 위해 자동 매핑을 비활성화하고 [`MiniOperators.make_mappings()`](../doc/mini-operators.qmd#minioperators.make_mappings)를 사용할 수 있습니다.

- 모든 연산자는 `[count]`와 점 반복(dot-repeat)을 지원합니다.

더 자세한 정보는 도움말의 다음 섹션들을 참조하세요:
- [`:h MiniOperators-overview`](../doc/mini-operators.qmd#minioperators-overview)
- [`:h MiniOperators.config`](../doc/mini-operators.qmd#minioperators.config)

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
    | Main   | `add('nvim-mini/mini.operators')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.operators', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.operators', version = false },` |
    | Stable | `{ 'nvim-mini/mini.operators', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.operators'`                         |
    | Stable | `Plug 'nvim-mini/mini.operators', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.operators').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 각 엔트리는 하나의 연산자를 설정합니다.
  -- `prefix`는 `setup()` 중에 매핑되는 키를 정의합니다: 노멀 모드에서는 
  -- 텍스트 오브젝트 및 줄 단위로, 비주얼 모드에서는 선택 영역에 대해 작동합니다.

  -- 텍스트 평가 및 결과로 교체
  evaluate = {
    prefix = 'g=',

    -- 평가를 수행하는 함수
    func = nil,
  },

  -- 텍스트 영역 교환
  exchange = {
    -- 참고: 기본 `gx`는 `gX`로 리매핑됩니다.
    prefix = 'gx',

    -- 이전 들여쓰기에 맞춰 새 텍스트의 들여쓰기를 자동 조정할지 여부
    reindent_linewise = true,
  },

  -- 텍스트 배가(복제)
  multiply = {
    prefix = 'gm',

    -- 배가하기 전 텍스트를 수정할 수 있는 함수
    func = nil,
  },

  -- 레지스터 내용으로 텍스트 교체
  replace = {
    -- 참고: 기본 `gr*` LSP 매핑은 제거됩니다.
    prefix = 'gr',

    -- 이전 들여쓰기에 맞춰 새 텍스트의 들여쓰기를 자동 조정할지 여부
    reindent_linewise = true,
  },

  -- 텍스트 정렬
  sort = {
    prefix = 'gs',

    -- 정렬을 수행하는 함수
    func = nil,
  }
}
```

## 유사한 플러그인 {#similar-plugins}

- [gbprod/substitute.nvim](https://github.com/gbprod/substitute.nvim)
- [svermeulen/vim-subversive](https://github.com/svermeulen/vim-subversive)
- [tommcdo/vim-exchange](https://github.com/tommcdo/vim-exchange)
- [christoomey/vim-sort-motion](https://github.com/christoomey/vim-sort-motion)
