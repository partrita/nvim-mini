---
title: "mini.visits"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-visits_readme.png?raw=true" alt="mini.visits" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 파일 시스템 방문 기록 추적 및 재사용

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-visits.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-visits)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-visits.mp4?raw=true)

**참고**: 이 데모는 [mini.pick](https://nvim-mini.org/mini.nvim/readmes/mini-pick)의 커스텀 `vim.ui.select()`를 사용합니다.

## 기능 {#features}

- 프로젝트 디렉터리별로 파일 시스템 방문(파일 및 디렉터리 모두)을 영구적으로 추적합니다. 저장된 방문 인덱스는 사람이 읽고 편집할 수 있는 형식입니다.

- 방문 인덱스는 써질 때마다 관련 정보를 포함하도록 정규화(normalize)됩니다. 구체적인 세부 사항은 커스터마이징이 가능합니다. `:h MiniVisits.normalize()`를 참조하세요.

- 경로에 라벨(labels)을 지정하여 나중에 영구적으로 사용할 수 있는 기능을 내장하고 있습니다. [`:h MiniVisits.add_label()`](../doc/mini-visits.qmd#minivisits.add_label) 및 [`:h MiniVisits.remove_label()`](../doc/mini-visits.qmd#minivisits.remove_label)을 참조하세요.

- 방문 데이터를 재사용하기 위한 함수를 제공합니다:
    - 커스텀 필터와 정렬(기본적으로 "경고한 최신 빈도(robust frecency)" 사용)을 사용하여 방문한 경로/라벨 목록을 가져옵니다. 선택기(pickers)의 소스로 사용할 수 있습니다.

      [`:h MiniVisits.list_paths()`](../doc/mini-visits.qmd#minivisits.list_paths) 및 [`:h MiniVisits.list_labels()`](../doc/mini-visits.qmd#minivisits.list_labels)를 참조하세요. [`:h MiniVisits.gen_filter`](../doc/mini-visits.qmd#minivisits.gen_filter) 및 [`:h MiniVisits.gen_sort`](../doc/mini-visits.qmd#minivisits.gen_sort)를 참조하세요.

    - `vim.ui.select()`를 사용하여 방문한 경로/라벨을 선택합니다.

      [`:h MiniVisits.select_path()`](../doc/mini-visits.qmd#minivisits.select_path) 및 [`:h MiniVisits.select_label()`](../doc/mini-visits.qmd#minivisits.select_label)을 참조하세요.

    - 대상 방향("순방향", "역방향", "처음", "마지막")으로 방문 경로를 순회합니다. [`:h MiniVisits.iterate_paths()`](../doc/mini-visits.qmd#minivisits.iterate_paths)를 참조하세요.

- 방문 인덱스를 수동으로 업데이트하여 모든 사용자 정보를 영구적으로 추적할 수 있는 기능을 제공합니다. `_index()` 세트 함수를 참조하세요.

참고:

- 모든 데이터는 빠른 동작을 위해 세션 내 Lua 변수에 저장되며, 영구적인 사용을 위해 디스크의 `config.store.path`에 저장됩니다.

- 경로 이름 변경이나 이동은 감지하지 못합니다 (이를 감지할 일반적인 방법이 없기 때문입니다). 일반적으로 변경 후, 하지만 디스크에 쓰기 _전_(보통 세션 종료 전)에 방문 인덱스를 수동으로 수정해야 합니다. 그렇지 않으면 이전 경로를 삭제된 것으로 간주하고 인덱스에서 제거합니다.

    이를 위한 [`MiniVisits.rename_in_index()`](../doc/mini-visits.qmd#minivisits.rename_in_index) 도우미가 제공됩니다.
    만약 이름 변경/이동을 ['mini.files'](https://nvim-mini.org/mini.nvim/readmes/mini-files)로 수행한다면 인덱스는 자동으로 업데이트됩니다.

더 자세한 정보는 도움말의 다음 섹션들을 참조하세요:

- [`:h MiniVisits-overview`](../doc/mini-visits.qmd#minivisits-overview)
- [`:h MiniVisits-index-specification`](../doc/mini-visits.qmd#minivisits-index-specification)
- [`:h MiniVisits-examples`](../doc/mini-visits.qmd#minivisits-examples)

## 개요 {#overview}

### 방문 추적 (Tracking)

파일 시스템 방문(디렉터리 및 파일 모두) 추적은 두 단계로 이루어집니다:

- 전용 이벤트가 발생할 때마다 타이머가 시작(또는 재시작)되어 일정 시간 후에 실제로 방문을 등록합니다.

- 전용 이벤트 발생 없이 지연 시간이 지나면 (즉, 사용자가 특정 버퍼에 "정착"하면), 다음 조건을 모두 만족할 때 방문이 등록됩니다:
    - 모듈이 비활성화되지 않음.
    - 버퍼가 비어 있지 않은 이름(방문 경로로 사용됨)을 가진 일반 버퍼임.
    - 방문 경로가 마지막으로 추적된 경로와 동일하지 않음.

방문은 현재 디렉터리에 대해 자동으로 등록되며, 방문 횟수가 증가하고 최신 방문 시간이 기록됩니다. 자세한 내용은 [`:h MiniVisits-index-specification`](../doc/mini-visits.qmd#minivisits-index-specification)을 참조하세요.

참고:

- 모든 데이터는 빠른 동작을 위해 세션 내 Lua 변수에 저장되며, 영구 사용을 위해 디스크의 한 곳에 저장됩니다. Neovim을 종료하기 전에 자동으로 디스크에 기록됩니다.

- `track.event`에 빈 문자열을 설정하여 자동 추적을 비활성화할 수 있습니다. 이 경우 사용자가 직접 [`MiniVisits.register_visit()`](../doc/mini-visits.qmd#minivisits.register_visit)를 호출해야 합니다.

### 방문 재사용 (Reusing)

방문 데이터는 최소한 다음과 같은 방식으로 재사용될 수 있습니다:

- 방문한 경로 목록을 가져와 방문 기록을 시각화/선택/탐색하는 데 사용합니다.

- 방문한 경로 중 하나를 선택하여 엽니다.

- 방문 기록을 따라 이동합니다.

- 라벨을 활용합니다. 모든 방문 기록에 하나 이상의 라벨("core", "tmp" 등)을 추가할 수 있습니다. 라벨은 방문 기록에 묶여 영구적으로 저장됩니다.

    라벨은 사용자가 특별히 관심을 갖는 파일 및/또는 디렉터리 그룹을 수동으로 만드는 데 사용할 수 있습니다.

    라벨을 사용하는 단 하나의 정착된 방법은 없습니다. 영감을 얻으려면 [`:h MiniVisits-examples`](../doc/mini-visits.qmd#minivisits-examples)를 참조하세요.

- 사용자 정의 데이터를 활용합니다. `_index()` 계열 함수를 사용하여 방문 인덱스를 수동으로 조작할 수 있습니다. 인덱스 내부의 모든 "저장 가능한" 사용자 데이터는 디스크에 기록되므로, 사용자가 원하는 어떤 종류의 워크플로우도 만들 수 있습니다.

실제 설정 및 워크플로우 예시는 [`:h MiniVisits-examples`](../doc/mini-visits.qmd#minivisits-examples)를 참조하세요.

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
    | Main   | `add('nvim-mini/mini.visits')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.visits', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.visits', version = false },` |
    | Stable | `{ 'nvim-mini/mini.visits', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.visits'`                         |
    | Stable | `Plug 'nvim-mini/mini.visits', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.visits').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 방문 인덱스가 경로 목록으로 변환되는 방식
  list = {
    -- 포함할 경로에 대한 서술어 (기본적으로 모두 포함)
    filter = nil,

    -- 방문 데이터를 기반으로 경로 정렬 (기본적으로 견고한 최신 빈도 순)
    sort = nil,
  },

  -- 에러가 아닌 피드백 표시를 비활성화할지 여부
  silent = false,

  -- 방문 인덱스가 저장되는 방식
  store = {
    -- Neovim이 닫히기 전에 모든 방문 기록을 기록할지 여부
    autowrite = true,

    -- 기록된 인덱스가 유효한지 확인하는 함수
    normalize = nil,

    -- 방문 인덱스를 저장할 경로
    path = vim.fn.stdpath('data') .. '/mini-visits-index',
  },

  -- 방문 추적이 수행되는 방식
  track = {
    -- 이 이벤트에서 방문 등록 타이머 시작
    -- 자동으로 수행하지 않으려면 빈 문자열(`''`) 입력
    event = 'BufEnter',

    -- 방문을 등록하기 전 이벤트 발생 후의 디바운스(Debounce) 지연 시간
    delay = 1000,
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [nvim-telescope/telescope-frecency.nvim](https://github.com/nvim-telescope/telescope-frecency.nvim)
- [ThePrimeagen/harpoon](https://github.com/ThePrimeagen/harpoon)
