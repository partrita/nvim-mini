---
title: "mini.ai"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-ai_readme.png?raw=true" alt="mini.ai" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### `a`/`i` 텍스트 오브젝트 확장 및 생성

- 기존의 일부 내장 텍스트 오브젝트(예: `a(`, `a)`, `a'` 등)를 강화하고, 새로운 오브젝트(예: `a*`, `a<Space>`, `af`, `a?` 등)를 생성하며, 사용자가 직접 자신만의 오브젝트(treesitter 기반 등)를 만들 수 있게 해줍니다.
- 점 반복(dot-repeat), `v:count`, 다양한 검색 방법, 연속 적용을 지원하며 Lua 패턴이나 함수를 통해 커스터마이징이 가능합니다.
- 괄호, 따옴표, 함수 호출, 인자, 태그, 사용자 프롬프트 및 모든 문장 부호/숫자/공백 문자에 대한 내장 기능을 제공합니다.

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-ai.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-ai)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-ai.mp4?raw=true)

## 기능 {#features}

- Lua 패턴과 함수를 사용하여 `a`/`i` 텍스트 오브젝트를 커스터마이징하여 생성할 수 있습니다. 다음을 지원합니다:
    - 점 반복(Dot-repeat).
    - `v:count`.
    - 다양한 검색 방법 ([`:h MiniAi.config`](../doc/mini-ai.qmd#miniai.config) 참조).
    - 연속 적용 (비주얼 모드를 나가지 않고 선택 영역 업데이트).
    - 여러 텍스트 오브젝트에 대한 별칭(Aliases).
- 포괄적인 내장 텍스트 오브젝트 ([`:h MiniAi-builtin-textobjects`](../doc/mini-ai.qmd#miniai-builtin-textobjects)에서 자세히 확인):
    - 균형 잡힌 괄호 (공백 포함 및 미포함) 및 별칭.
    - 균형 잡힌 따옴표 및 별칭.
    - 함수 호출.
    - 인자.
    - 태그.
    - 사용자 프롬프트로부터 유도됨.
    - 라틴 문자 이외의 모든 것에 대한 기본값 (`:h text-objects`로 폴백).
- 텍스트 오브젝트의 왼쪽/오른쪽 끝으로 점프하는 이동 기능.
- 일부 내장 텍스트 오브젝트를 조정하기 위한 사양 생성기 세트 ([`MiniAi.gen_spec`](../doc/mini-ai.qmd#miniai.gen_spec) 도움말 참조).
- Treesitter 텍스트 오브젝트 ([`MiniAi.gen_spec.treesitter()`](../doc/mini-ai.qmd#miniai.gen_spec.treesitter) 헬퍼를 통해 지원).

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

    | 브랜치 | 코드 스니펫                                                 |
    |--------|--------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.ai')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.ai', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                |
    |--------|---------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.ai', version = false },` |
    | Stable | `{ 'nvim-mini/mini.ai', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                       |
    |--------|----------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.ai'`                         |
    | Stable | `Plug 'nvim-mini/mini.ai', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.ai').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 필드로 텍스트 오브젝트 ID를, 값으로 텍스트 오브젝트 사양을 가지는 테이블입니다.
  -- 내장 텍스트 오브젝트를 비활성화할 때도 사용합니다. |MiniAi.config|를 참조하세요.
  custom_textobjects = nil,

  -- 모듈 매핑. 비활성화하려면 `''`(빈 문자열)을 사용하세요.
  mappings = {
    -- 주요 텍스트 오브젝트 접두사
    around = 'a',
    inside = 'i',

    -- 다음(next)/이전(last) 변형
    -- 참고: Neovim>=0.12에서는 내장 LSP 선택 매핑을 덮어씁니다.
    -- 사용하려면 LSP 선택을 수동으로 매핑하세요 ([`:h MiniAi.config`](../doc/mini-ai.qmd#miniai.config) 참조).
    around_next = 'an',
    inside_next = 'in',
    around_last = 'al',
    inside_last = 'il',

    -- `a` 텍스트 오브젝트의 해당 끝으로 커서 이동
    goto_left = 'g[',
    goto_right = 'g]',
  },

  -- 텍스트 오브젝트를 검색할 줄 수
  n_lines = 50,

  -- 오브젝트 검색 방법 (먼저 현재 줄 내부에서 검색한 다음 주변 검색).
  -- 'cover', 'cover_or_next', 'cover_or_prev', 'cover_or_nearest',
  -- 'next', 'previous', 'nearest' 중 하나입니다.
  search_method = 'cover_or_next',

  -- 에러가 아닌 피드백 표시 여부
  -- 사용자 입력이 필요한 경우 유휴 시간 후에 표시되는 (순수 정보성) 헬퍼 메시지에도 영향을 미칩니다.
  silent = false,
}
```

## 유사한 플러그인 {#similar-plugins}

- [wellle/targets.vim](https://github.com/wellle/targets.vim)
- [nvim-treesitter/nvim-treesitter-textobjects](https://github.com/nvim-treesitter/nvim-treesitter-textobjects)
- [kana/vim-textobj-user](https://github.com/kana/vim-textobj-user)
