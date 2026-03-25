---
title: "mini.doc"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-doc_readme.png?raw=true" alt="mini.doc" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### EmmyLua 스타일 주석으로부터 도움말 파일 생성

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-doc.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-doc)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-doc.mp4?raw=true)

## 기능 {#features}

- EmmyLua 스타일의 어노테이션 주석을 작성하여 코드 바로 옆에 문서를 유지할 수 있습니다. 주석은 그대로 파싱되므로 포맷팅은 내장 가이드를 따라야 합니다. 하지만 출력 도움말 파일을 더 세밀하게 관리하기 위해 많은 생성 단계에서 커스텀 훅(hooks)이 허용됩니다.
- 정해진 파일 세트를 한 줄씩 처리하여 생성을 수행합니다. 각 줄은 (설정 가능한 특정 패턴과 일치하는 경우) 문서 블록의 일부로 간주되거나, 그렇지 않은 경우 문서 블록의 "애프터라인(afterline)"으로 간주됩니다. 자세한 내용은 [`MiniDoc.generate()`](../doc/mini-doc.qmd#minidoc.generate) 도움말을 참조하세요.
- 도움말 파일의 특정 부분을 설명하는 중첩된 데이터 구조(섹션, 블록, 파일, 문서)를 사용하여 처리가 수행됩니다. 자세한 내용은 [`MiniDoc-data-structures`](../doc/mini-doc.qmd#minidoc-data-structures) 도움말 페이지를 참조하세요.
- 훅 함수를 통해 출력 결과물을 유연하게 커스터마이징할 수 있습니다.
- 프로젝트별 스크립트는 설정 가능한 경로를 가진 일반 Lua 파일로 작성할 수 있습니다. 자세한 내용은 [`MiniDoc.generate()`](../doc/mini-doc.qmd#minidoc.generate) 도움말을 참조하세요.

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

    | 브랜치 | 코드 스니펫                                                  |
    |--------|---------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.doc')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.doc', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                 |
    |--------|----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.doc', version = false },` |
    | Stable | `{ 'nvim-mini/mini.doc', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                        |
    |--------|-----------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.doc'`                         |
    | Stable | `Plug 'nvim-mini/mini.doc', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.doc').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 줄에 문서 어노테이션이 있는지 확인하기 위한 Lua 문자열 패턴.
  -- 첫 번째 캡처 그룹은 가능한 섹션 ID를 설명해야 합니다. 기본값은 
  -- 어노테이션 줄이 다음과 같아야 함을 의미합니다:
  -- - 첫 번째 열에서 `---`로 시작.
  -- - `---` 뒤의 공백이 아닌 문자는 새 섹션 ID로 처리됨.
  -- - 기본 텍스트 시작 부분의 단일 공백은 무시됨.
  annotation_pattern = '^%-%-%-(%S*) ?',

  -- 첫 번째 캡처된 식별자 이전까지의 블록 어노테이션 줄의 식별자
  default_section_id = '@text',

  -- 문서 라이프 사이클의 특정 단계에서 적용될 훅(hooks).
  -- 인자로 받은 데이터를 직접 수정해야 합니다 (새 데이터를 반환하지 않음).
  hooks = {
    -- 다른 무엇보다 먼저 블록에 적용됨
    block_pre = --<함수: 헤더 섹션(태그 및/또는 시그니처) 유추>,

    -- 다른 무엇보다 먼저 섹션에 적용됨
    section_pre = --<함수: 현재 앨리어스(alias) 교체>,

    -- 섹션이 특정 캡처 ID를 가진 경우 적용됨
    sections = {
      ['@alias'] = --<함수: MiniDoc.current.aliases에 앨리어스 등록>,
      ['@class'] = --<함수>,
      -- 가장 일반적인 사용법은 |MiniDoc.afterlines_to_code| 참조
      ['@eval'] = --<함수: 줄을 평가하고 반환값으로 교체>,
      ['@field'] = --<함수>,
      ['@param'] = --<함수>,
      ['@private'] = --<함수: 삭제를 위해 블록 등록>,
      ['@return'] = --<함수>,
      ['@seealso'] = --<함수>,
      ['@signature'] = --<함수: 문서화된 객체의 시그니처 포맷팅>,
      ['@tag'] = --<함수: 줄을 적절한 태그 줄로 변환>,
      ['@text'] = --<함수: 의도적으로 아무것도 하지 않음>,
      ['@type'] = --<함수>,
      ['@usage'] = --<함수>,
    },

    -- 이전 모든 단계 후에 섹션에 적용됨
    section_post = --<함수: 현재 아무것도 하지 않음>,

    -- 이전 모든 단계 후에 블록에 적용됨
    block_post = --<함수: 여러 작업을 수행함>,

    -- 이전 모든 단계 후에 파일에 적용됨
    file = --<함수: 구분자 추가>,

    -- 이전 모든 단계 후에 문서에 적용됨
    doc = --<함수: modeline 추가>,

    -- 출력 파일이 쓰여지기 전에 적용됨. 줄 배열을 인자로 받음.
    write_pre = --<함수: 상단의 구분자 제거>,

    -- 출력 도움말 파일이 쓰여진 후에 적용됨. 문서를 인자로 받음.
    write_post = --<함수: 다양한 편의 동작>,
  },

  -- 프로젝트별 도움말 파일 생성(커스텀 입력 파일, 훅 등)을 처리하는 
  -- 스크립트 경로 (현재 디렉터리 기준).
  script_path = 'scripts/minidoc.lua',

  -- 에러가 아닌 피드백 표시 여부
  silent = false,
}
```

## 유사한 플러그인 {#similar-plugins}

- [tjdevries/tree-sitter-lua](https://github.com/tjdevries/tree-sitter-lua)
- [numToStr/lemmy-help](https://github.com/numToStr/lemmy-help) (커맨드 라인 도구)
