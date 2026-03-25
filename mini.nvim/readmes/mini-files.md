---
title: "mini.files"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-files_readme.png?raw=true" alt="mini.files" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 파일 시스템 탐색 및 조작

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-files.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-files)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-files.mp4?raw=true)

## 기능 {#features}

- 중첩된 디렉터리를 표시하기 위한 컬럼 뷰(Miller columns)를 사용하여 파일 시스템을 탐색합니다. 개요는 [`:h MiniFiles-navigation`](../doc/mini-files.qmd#minifiles-navigation)을 참조하세요.

- 커서 아래의 파일이나 디렉터리를 미리 볼 수 있는 기능을 제공합니다 (옵트인).

- 텍스트 버퍼를 편집하여 파일과 디렉터리를 조작합니다: 생성, 삭제, 복사, 이름 변경, 이동. 개요는 [`:h MiniFiles-manipulation`](../doc/mini-files.qmd#minifiles-manipulation)을 참조하세요.

- `netrw` 대신 기본 파일 탐색기로 사용할 수 있습니다.

- 커스터마이징 가능:
    - 파일 시스템 항목의 필터/접두사/정렬.
    - 일반적인 탐색 동작에 사용되는 매핑.
    - UI 옵션: 커서 아래 항목 미리보기 여부 등.
    - 더 빠른 탐색을 위한 북마크.

일반적인 설정 예제는 [`:h MiniFiles-examples`](../doc/mini-files.qmd#minifiles-examples)를 참조하세요.

참고:

- 이 모듈은 Linux에서 작성되고 철저히 테스트되었습니다. 다른 플랫폼/OS(Windows, MacOS 등) 지원이 목표이지만 보장되지는 않습니다.

- 이 모듈은 권한 부족에 대해 별도의 에러 없이 반응합니다:
    - 파일이 보이지 않는 경우, 해당 파일 또는 부모 디렉터리의 읽기 권한을 확인하세요.
    - 조작 결과가 없는 경우, 쓰기 권한을 확인하세요.

## 의존성 {#dependencies}

완전한 경험을 위해 권장되는 사항입니다 (권장 사항 없이도 작동합니다):

- 파일/디렉터리 이름 옆에 아이콘을 표시하기 위해 ['mini.icons'](https://nvim-mini.org/mini.nvim/readmes/mini-icons) 모듈 활성화. [nvim-tree/nvim-web-devicons](https://github.com/nvim-tree/nvim-web-devicons) 플러그인이 있으면 그것을 사용할 수도 있습니다.

## 빠른 시작 {#quick-start}

### 탐색 (Navigation)

- `:lua MiniFiles.open()`을 실행합니다.

- 탐색:
    - `j`/`k`를 눌러 아래/위로 이동합니다.
    - `l`을 눌러 커서 아래의 항목을 확장합니다: 디렉터리를 보여주거나 가장 최근 창에서 파일을 엽니다.
    - `h`를 눌러 부모 디렉터리로 이동합니다.
    - `m<문자>`를 입력하여 현재 포커스된 창의 디렉터리 경로를 북마크 `<문자>`로 설정합니다. `'<문자>`로 해당 점프로 이동합니다. `''`로 점프 이전 위치로 돌아갑니다.
    - 사용할 수 있는 다른 매핑과 북마크에 대한 정보를 보려면 `g?`를 입력하세요.
    - 다른 버퍼에서와 마찬가지로 이동합니다 (`$`, `G`, `f`/`t` 등).

자세한 개요는 [`:h MiniFiles-navigation`](../doc/mini-files.qmd#minifiles-navigation)을 참조하세요.

### 조작 (Manipulation)

- 조작을 수행할 디렉터리로 이동합니다.

- 파일 시스템 동작을 나타내는 방식으로 버퍼를 편집합니다:
    - **파일/디렉터리 생성**: `file` 또는 `dir/`와 같이 새 줄을 만듭니다.
    - **하위 디렉터리에 파일/디렉터리 생성**: `dir/file` 또는 `dir/nested/`와 같이 새 줄을 만듭니다.
    - **파일/디렉터리 삭제**: 해당 항목을 나타내는 줄 전체를 삭제합니다.
    - **파일/디렉터리 이름 변경**: 항목 아이콘 오른쪽의 텍스트를 변경합니다.
    - **파일/디렉터리 복사**: 줄 전체를 복사하여 대상 디렉터리에 붙여넣습니다.
    - **파일/디렉터리 이동**: 줄 전체를 잘라내어 대상 디렉터리에 붙여넣습니다.

- `=`를 누릅니다. **확인 대화 상자를 읽습니다.** `y`/`<CR>`로 확인하거나 `n`/`<Esc>`로 취소합니다.

자세한 개요는 [`:h MiniFiles-manipulation`](../doc/mini-files.qmd#minifiles-manipulation)을 참조하세요.

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
    | Main   | `add('nvim-mini/mini.files')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.files', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.files', version = false },` |
    | Stable | `{ 'nvim-mini/mini.files', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.files'`                         |
    | Stable | `Plug 'nvim-mini/mini.files', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.files').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 표시되는 내용의 커스터마이징
  content = {
    -- 어떤 파일 시스템 항목을 보여줄지 결정하는 서술어(predicate)
    filter = nil,
    -- 파일 시스템 항목에 사용할 하이라이트 그룹
    highlight = nil,
    -- 파일 시스템 항목 왼쪽에 표시할 접두사(prefix) 텍스트 및 하이라이트
    prefix = nil,
    -- 파일 시스템 항목을 표시할 순서
    sort = nil,
  },

  -- 탐색기 내부에서만 생성되는 모듈 매핑.
  -- 생성하지 않으려면 `''`(빈 문자열)을 사용하세요.
  mappings = {
    close       = 'q',
    go_in       = 'l',
    go_in_plus  = 'L',
    go_out      = 'h',
    go_out_plus = 'H',
    mark_goto   = "'",
    mark_set    = 'm',
    reset       = '<BS>',
    reveal_cwd  = '@',
    show_help   = 'g?',
    synchronize = '=',
    trim_left   = '<',
    trim_right  = '>',
  },

  -- 일반 옵션
  options = {
    -- 영구 삭제할지, 모듈 전용 휴지통으로 이동할지 여부
    permanent_delete = true,
    -- 디렉터리 편집을 위한 기본 탐색기로 사용할지 여부
    use_as_default_explorer = true,
  },

  -- 탐색기 창의 커스터마이징
  windows = {
    -- 나란히 표시할 창의 최대 개수
    max_number = math.huge,
    -- 커서 아래의 파일/디렉터리 미리보기 여부
    preview = false,
    -- 포커스된 창의 너비
    width_focus = 50,
    -- 포커스되지 않은 창의 너비
    width_nofocus = 15,
    -- 미리보기 창의 너비
    width_preview = 25,
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [nvim-tree/nvim-tree.lua](https://github.com/nvim-tree/nvim-tree.lua)
- [stevearc/oil.nvim](https://github.com/stevearc/oil.nvim)
- [nvim-neo-tree/neo-tree.nvim](https://github.com/nvim-neo-tree/neo-tree.nvim)
