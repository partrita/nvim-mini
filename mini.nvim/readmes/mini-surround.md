---
title: "mini.surround"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-surround_readme.png?raw=true" alt="mini.surround" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 빠르고 강력한 서라운드(Surround) 액션

- 주변 문자(괄호 쌍, 따옴표 등)를 추가, 삭제, 교체, 찾기, 하이라이트합니다.
- 텍스트 편집 시 점 반복(dot-repeat), `v:count`, 다양한 검색 방식, "이전(last)"/"다음(next)" 확장 매핑, Lua 패턴 또는 함수를 통한 커스터마이징 등을 지원합니다.
- 괄호, 함수 호출, 태그, 사용자 프롬프트 및 모든 영숫자/문장 부호/공백 문자에 대한 내장 설정을 포함합니다.
- 'tpope/vim-surround'와 유사한 설정을 유지하고 있습니다.

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-surround.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-surround)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-surround.mp4?raw=true)

## 기능 {#features}

- 설정 가능한 매핑을 통한 액션 제공 (텍스트 편집 액션은 기본적으로 점 반복이 가능하며 `[count]`를 준수합니다):
    - `sa`로 주변 문자 추가 (비주얼 모드 또는 모션 사용 시).
    - `sd`로 주변 문자 삭제.
    - `sr`로 주변 문자 교체.
    - `sf` 또는 `sF`로 주변 문자 찾기 (커서를 오른쪽 또는 왼쪽으로 이동).
    - `sh`로 주변 문자 하이라이트.
- 주변 문자는 "입력"(삭제/교체 시작, 찾기, 하이라이트 시)과 "출력"(추가/교체 완료 시) 모두에서 단일 문자로 식별됩니다:
    - 'f' - 함수 호출 (영숫자, '_' 또는 '.'로 이루어진 문자열 뒤에 균형 잡힌 '()'가 오는 형태). "입력" 시 함수 호출을 찾고, "출력" 시 사용자에게 함수 이름을 입력받습니다.
    - 't' - 태그. "입력" 시 동일한 식별자를 가진 태그를 찾고, "출력" 시 사용자에게 태그 이름을 입력받습니다.
    - '()', '[]', '{}', '<>' 모든 괄호 기호. "입력" 시 균형 잡힌 괄호를 나타내며(여는 괄호는 공백 패딩 포함, 닫는 괄호는 미포함), "출력" 시 괄호의 왼쪽과 오른쪽 부분을 나타냅니다.
    - '?' - 대화형. 사용자에게 왼쪽과 오른쪽 부분을 직접 입력받습니다.
    - 그 외 모든 단일 문자 식별자(`getcharstr()`에서 지원하는 문자)는 왼쪽과 오른쪽이 동일한 주변 문자를 나타냅니다.
- 단순히 감싸고 있는 정보뿐만 아니라 다음, 이전 또는 가장 가까운 주변 문자를 찾기 위한 설정 가능한 검색 방식을 제공합니다. 자세한 내용은 도움말의 [`MiniSurround.config`](../doc/mini-surround.qmd#minisurround.config)를 참조하세요.
- 주변 문자를 찾는 모든 액션(삭제, 교체, 찾기, 하이라이트)은 검색 방식을 이전/뒤로 변경하는 접미사(suffix)와 함께 사용할 수 있습니다. 자세한 내용은 도움말의 [`MiniSurround.config`](../doc/mini-surround.qmd#minisurround.config)를 참조하세요.

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

    | 브랜치 | 코드 스니펫                                                       |
    |--------|--------------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.surround')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.surround', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                      |
    |--------|---------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.surround', version = false },` |
    | Stable | `{ 'nvim-mini/mini.surround', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                             |
    |--------|----------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.surround'`                         |
    | Stable | `Plug 'nvim-mini/mini.surround', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.surround').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 내장 설정 외에 추가할 스니펫 설정을 정의합니다.
  -- 예제와 함께 자세한 내용은 [`:h MiniSurround.config`](../doc/mini-surround.qmd#minisurround.config)를 참조하세요.
  custom_surroundings = nil,

  -- [`MiniSurround.highlight()`](../doc/mini-surround.qmd#minisurround.highlight) 호출 시 하이라이트 지속 시간 (ms)
  highlight_duration = 500,

  -- 모듈 매핑. 비활성화하려면 `''`(빈 문자열)을 사용하세요.
  mappings = {
    add = 'sa', -- 노멀 및 비주얼 모드에서 주변 문자 추가
    delete = 'sd', -- 주변 문자 삭제
    find = 'sf', -- 주변 문자 찾기 (오른쪽으로)
    find_left = 'sF', -- 주변 문자 찾기 (왼쪽으로)
    highlight = 'sh', -- 주변 문자 하이라이트
    replace = 'sr', -- 주변 문자 교체

    suffix_last = 'l', -- "이전(prev)" 검색 방식을 위한 접미사
    suffix_next = 'n', -- "다음(next)" 검색 방식을 위한 접미사
  },

  -- 주변 문자를 검색할 줄 수
  n_lines = 20,

  -- 선택 영역 타입을 존중할지 여부:
  -- - 줄 단위(linewise) 모드에서는 주변 문자를 별도의 줄에 배치합니다.
  -- - 블록 단위(blockwise) 모드에서는 각 줄에 주변 문자를 배치합니다.
  respect_selection_type = false,

  -- 주변 문자를 검색하는 방법 (먼저 현재 줄 내부를 찾고, 그 다음 주변 검색).
  -- 'cover', 'cover_or_next', 'cover_or_prev', 'cover_or_nearest', 'next', 'prev', 'nearest' 중 하나.
  -- 자세한 내용은 [`:h MiniSurround.config`](../doc/mini-surround.qmd#minisurround.config)를 참조하세요.
  search_method = 'cover',

  -- 에러가 아닌 피드백 표시를 비활성화할지 여부.
  -- 이는 사용자 입력이 필요할 때 유휴 시간 이후에 표시되는 (순수하게 정보 제공용인) 도움말 메시지에도 영향을 줍니다.
  silent = false,
}
```

## 유사한 플러그인 {#similar-plugins}

- [tpope/vim-surround](https://github.com/tpope/vim-surround)
- [kylechui/nvim-surround](https://github.com/kylechui/nvim-surround)
- [machakann/vim-sandwich](https://github.com/machakann/vim-sandwich)
