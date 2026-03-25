---
title: "mini.indentscope"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-indentscope_readme.png?raw=true" alt="mini.indentscope" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 들여쓰기 범위(indent scope) 시각화 및 작업

- 커스터마이징 가능한 디바운스 지연 시간, 애니메이션 스타일, 범위 계산 옵션을 제공합니다.
- 범위 관련 이동(motions) 및 텍스트 오브젝트를 구현합니다.

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-indentscope.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-indentscope)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-indentscope.mp4?raw=true)

## 기능 {#features}

- **애니메이션**이 적용된 수직선으로 범위를 시각화합니다. 매우 빠르며 비차단(non-blocking) 방식으로 자동 수행되므로 커서 이동 등의 다른 작업을 동시에 할 수 있습니다. 디바운스 지연 시간과 애니메이션 규칙을 커스터마이징할 수 있습니다.
- 범위 계산 옵션의 커스터마이징은 전역 수준([`MiniIndentscope.config`](../doc/mini-indentscope.qmd#miniindentscope.config)), 특정 버퍼(`vim.b.miniindentscope_config` 변수 사용), 또는 호출 내부([`MiniIndentscope.get_scope()`](../doc/mini-indentscope.qmd#miniindentscope.get_scope)의 `opts` 변수 사용)에서 수행할 수 있습니다.
- 경계(border) 개념을 커스터마이징할 수 있습니다: 들여쓰기가 엄격하게 더 적은 인접한 줄을 경계로 인식할지 여부를 결정합니다. Python이나 일반 텍스트와 같은 특정 파일 타입에 유용합니다.
- 줄을 "경계 우선(border first)"으로 간주하는 방식을 커스터마이징할 수 있습니다. 예를 들어 함수 헤더에 커서를 두고 해당 함수의 본문 범위를 얻고 싶을 때 유용합니다.
- 범위 내에서 작동하는 텍스트 오브젝트와 이동(motions) 기능을 제공합니다. `v:count` 및 연산자 대기(operator pending) 모드에서의 점 반복(dot-repeat)을 지원합니다.

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

    | 브랜치 | 코드 스니펫                                                          |
    |--------|-----------------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.indentscope')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.indentscope', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.indentscope', version = false },` |
    | Stable | `{ 'nvim-mini/mini.indentscope', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                                |
    |--------|-------------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.indentscope'`                         |
    | Stable | `Plug 'nvim-mini/mini.indentscope', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.indentscope').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 그리기 옵션
  draw = {
    -- 이벤트 발생 후 범위 표시기가 그려지기 시작할 때까지의 지연 시간 (ms)
    delay = 100,

    -- 범위가 처음 그려질 때의 애니메이션 규칙. 다음 단계 번호와 전체 단계 번호를 
    -- 인자로 받아 대기 시간(ms)을 반환하는 함수입니다. 내장 옵션은 
    -- |MiniIndentscope.gen_animation|을 참조하세요. 애니메이션을 비활성화하려면 
    -- `require('mini.indentscope').gen_animation.none()`을 사용하세요.
    animation = --<함수: 단계 사이의 20ms 간격을 일정하게 유지함>,

    -- 범위를 자동으로 그릴지 여부: 그릴 경우 `true`, 그렇지 않으면 `false` 반환.
    -- 기본값은 완전히 계산된 범위만 그립니다 (`options.n_lines` 참조).
    predicate = function(scope) return not scope.body.is_incomplete end,

    -- 기호 우선순위. 더 많은 기호 위에 표시하려면 값을 높이세요.
    priority = 2,
  },

  -- 모듈 매핑. 비활성화하려면 `''`(빈 문자열)을 사용하세요.
  mappings = {
    -- 텍스트 오브젝트
    object_scope = 'ii',
    object_scope_with_border = 'ai',

    -- 이동 (해당하는 경계 줄로 이동, 없으면 본문 줄로 이동)
    goto_top = '[i',
    goto_bottom = ']i',
  },

  -- 범위 계산을 제어하는 옵션
  options = {
    -- 범위 경계 유형: 어느 줄을 경계로 분류할지 결정합니다.
    -- 'both', 'top', 'bottom', 'none' 중 하나가 될 수 있습니다.
    border = 'both',

    -- 참조 들여쓰기를 계산할 때 커서 열(cursor column)을 사용할지 여부.
    -- 가로 커서 이동에 따라 점진적인 범위를 확인하는 데 유용합니다.
    indent_at_cursor = true,

    -- 범위를 계산할 위아래 최대 줄 수
    n_lines = 10000,

    -- 먼저 입력된 줄이 인접 범위의 경계인지 확인할지 여부.
    -- 함수 헤더에 커서를 두고 해당 함수의 본문 범위를 얻고 싶을 때 사용하세요.
    try_as_border = false,
  },

  -- 범위 표시기를 그리는 데 사용할 문자
  symbol = '╎',
}
```

## 유사한 플러그인 {#similar-plugins}

- [lukas-reineke/indent-blankline.nvim](https://github.com/lukas-reineke/indent-blankline.nvim)
- [michaeljsmith/vim-indent-object](https://github.com/michaeljsmith/vim-indent-object)
