---
title: "mini.test"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-test_readme.png?raw=true" alt="mini.test" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 방대한 Neovim 플러그인 테스트 작성 및 사용

- 계층적 테스트, 후크(hooks), 파라미터화, 필터링(현재 파일 또는 커서 위치 기준 등), 화면 테스트, "busted-style" 에뮬레이션, 사용자 정의 리포터 등을 지원합니다.
- 자식 Neovim 프로세스를 관리하기 위해 제공되는 래퍼(wrapper)와 함께 사용하도록 설계되었습니다.

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-test.qmd)를 참조하세요. 예제 기반의 시각적 입문서는 [TESTING.md](https://nvim-mini.org/mini.nvim/TESTING)를, 더 심층적인 사용 사례는 ['mini.nvim' 테스트 코드](https://github.com/nvim-mini/mini.nvim/tree/main/tests)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-test)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-test.mp4?raw=true)

## 기능 {#features}

- 테스트 액션은 테이블의 이름이 있는 호출 가능한 엔트리로 정의됩니다.
- 테스트에서 사용하도록 설계된 자식 Neovim 프로세스 생성 도우미를 제공합니다 (스크린샷 촬영 및 검증 포함). 도움말의 [`MiniTest.new_child_neovim()`](../doc/mini-test.qmd#minitest.new_child_neovim) 및 [`MiniTest.expect.reference_screenshot()`](../doc/mini-test.qmd#minitest.expect.reference_screenshot)을 참조하세요.
- 사용자 지정 후크, 파라미터화 및 사용자 데이터를 사용하여 테스트를 계층적으로 구성할 수 있습니다. 도움말의 [`MiniTest.new_set()`](../doc/mini-test.qmd#minitest.new_set)을 참조하세요.
- [Olivine-Labs/busted](https://github.com/Olivine-Labs/busted) 인터페이스(`describe`, `it` 등)의 에뮬레이션을 지원합니다.
- 작지만 유용한 기본 기대치(`assert`와 유사한 함수) 세트를 제공합니다. 도움말의 [`MiniTest.expect`](../doc/mini-test.qmd#minitest.expect)를 참조하세요.
- 테스트할 파일을 자유롭게 정의할 수 있습니다.
- 테스트 케이스 필터링이 가능합니다. 파일 단위 테스트([`MiniTest.run_file()`](../doc/mini-test.qmd#minitest.run_file))나 현재 커서 위치와 같은 특정 위치의 테스트 케이스 실행([`MiniTest.run_at_location()`](../doc/mini-test.qmd#minitest.run_at_location))을 위한 사전 정의된 래퍼가 제공됩니다.
- 출력 결과에 대한 리포터를 커스터마이징할 수 있습니다. 두 가지가 기본 제공됩니다:
    - 대화형 사용을 위한 [`MiniTest.gen_reporter.buffer()`](../doc/mini-test.qmd#minitest.gen_reporter.buffer).
    - 헤드리스(headless) Neovim을 위한 [`MiniTest.gen_reporter.stdout()`](../doc/mini-test.qmd#minitest.gen_reporter.stdout).
- 프로젝트별 프로젝트별 스크립트를 커스터마이징할 수 있습니다.
- Unix 계열(Linux, MacOS 등)과 Windows에서 모두 작동합니다.

## 설치 {#installation}

이 플러그인은 'mini.nvim' 라이브러리의 일부로 설치하거나(**권장**), 독립적인 Git 저장소로 설치할 수 있습니다.

두 가지 브랜치 중 하나를 골라 설치할 수 있습니다:

- `main` (기본값, **권장**): 플러그인의 최신 개발 버전입니다. 마지막 안정 릴리스 이후의 모든 변경 사항은 베타 테스트 단계(알파 테스트를 통과하고 어느 정도 안정됨을 의미)로 간주되어야 합니다.
- `stable`: `main` 브랜치에서 공개 베타 테스트를 거친 코드가 포함된 릴리스 시에만 업데이트됩니다.

다음은 몇 가지 일반적인 설치 방법의 코드 스니펫입니다 (하나만 사용하세요):

<details>
<summary><a href="https://nvim-mini.org/mini.nvim/readmes/mini-test">mini.test</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | *권장되는 'mini.deps' 설치 방법을 따르세요* |
    | Stable | *권장되는 'mini.deps' 설치 방법을 따르세요* |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                                   |
    |--------|----------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.test')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.test', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' library:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.test', version = false },` |
    | Stable | `{ 'nvim-mini/mini.test', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.test'`                         |
    | Stable | `Plug 'nvim-mini/mini.test', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.test').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 테스트 케이스 수집 옵션. [`:h MiniTest.collect()`](../doc/mini-test.qmd#minitest.collect)를 참조하세요.
  collect = {
    -- 'busted' 테스트 프레임워크의 함수들을 임시로 에뮬레이션합니다
    -- (`describe`, `it`, `before_each`, `after_each` 등)
    emulate_busted = true,

    -- 수집할 파일 경로 배열을 반환하는 함수.
    -- 기본값: 'tests' 디렉터리 내의 'test_'로 시작하는 모든 Lua 파일.
    find_files = function()
      return vim.fn.globpath('tests', '**/test_*.lua', true, true)
    end,

    -- 테스트 케이스를 실행할지 여부를 나타내는 서술어(predicate) 함수
    filter_cases = function(case) return true end,
  },

  -- 테스트 케이스 실행 옵션. [`:h MiniTest.execute()`](../doc/mini-test.qmd#minitest.execute)를 참조하세요.
  execute = {
    -- 호출 가능한 `start()`, `update()`, `finish()` 필드를 가진 테이블
    reporter = nil,

    -- 첫 번째 에러 발생 시 실행을 중단할지 여부
    stop_on_error = false,
  },

  -- 프로젝트별 테스트 실행을 처리하는 스크립트 경로 (현재 디렉터리 기준 상대 경로)
  script_path = 'scripts/minitest.lua',

  -- 에러가 아닌 피드백 표시를 비활성화할지 여부
  silent = false,
}
```

## 유사한 플러그인 {#similar-plugins}

- [nvim-lua/plenary.nvim](https://github.com/nvim-lua/plenary.nvim) ('test_harness', 'busted', 'luassert' 모듈)
