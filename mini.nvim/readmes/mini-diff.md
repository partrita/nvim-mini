---
title: "mini.diff"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-diff_readme.png?raw=true" alt="mini.diff" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### Diff 헝크(hunk) 작업

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-diff.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-diff)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-diff.mp4?raw=true)

## 기능 {#features}

- 버퍼 텍스트와 설정 가능한 참조(reference) 데이터 간의 차이를 대화식으로 시각화합니다 (입력하는 동안 업데이트됨). 줄 단위로 수행되며, 각 줄이 추가, 변경 또는 삭제된 부분(이를 '헝크, hunk'라고 함)에 속하는지 보여줍니다. 커스터마이징 가능한 컬러 기호(signs) 또는 줄 번호를 통해 시각화할 수 있습니다.

- 텍스트 영역 내에서 더 자세한 헝크 정보를 보여주는 특별한 토글형 오버레이(overlay) 뷰를 제공합니다.

- 참조 텍스트를 최신 상태로 유지하고 상호 작용을 정의하기 위해 버퍼별로 완전히 설정 가능한 소스(source)를 제공합니다. 순서대로 연결을 시도하는 소스 배열일 수 있습니다. 기본적으로 Git 소스를 사용합니다 (Git 인덱스의 버퍼 파일 내용을 참조로 사용).

- Diff 헝크를 관리하기 위한 설정 가능한 매핑:
    - 지정된 영역(비주얼 선택 또는 점 반복 가능한 연산자) 내의 헝크를 적용(stage)하거나 리셋합니다.
    - 연산자의 대상으로 사용할 수 있는 "커서 아래의 헝크 범위" 텍스트 오브젝트를 제공합니다.
    - 첫 번째/이전/다음/마지막 헝크로 탐색합니다.

수행하지 않는 작업:

- (기본) Git 소스에서 헝크를 시각화하고 스테이징(적용)하는 것 외에, Git과 직접적으로 관련된 기능(예: 헝크 스테이징 해제 등)은 지원하지 않습니다.

더 자세한 정보는 도움말의 다음 부분을 참조하세요:

- [`:h MiniDiff-overview`](../doc/mini-diff.qmd#minidiff-overview)
- [`:h MiniDiff-source-specification`](../doc/mini-diff.qmd#minidiff-source-specification)
- [`:h MiniDiff-hunk-specification`](../doc/mini-diff.qmd#minidiff-hunk-specification)
- [`:h MiniDiff-diff-summary`](../doc/mini-diff.qmd#minidiff-diff-summary)

## 개요 {#overview}

### Diff와 헝크 (Diffs and hunks)

"Diff"(difference의 줄임말)는 두 문자열이 어떻게 다른지 계산한 결과입니다. 이는 줄 단위로 수행됩니다. 즉, 두 파일에서 공통된 줄 시퀀스 사이에 차이가 있는 줄 그룹(이를 "헝크, hunks"라고 함)이 끼어 있는 형태를 계산하는 것이 목표입니다.

Diff 계산은 (Git 등에서 사용되는) 일반적인 개념이지만, 이 모듈은 현재 버퍼의 텍스트와 해당 버퍼를 위해 특별히 관리되는 참조 텍스트 간의 차이를 계산합니다. 예를 들어, 기본 참조 텍스트는 Git 인덱스의 파일 내용으로 계산됩니다. 이는 `config.source`에서 커스터마이징할 수 있습니다.

### 라이프 사이클 (Life cycle)

- 적절한(이미 활성화되지 않았고, 유효하며, 텍스트를 표시 중인) 버퍼에 진입하면 Diff 프로세싱 활성화를 시도합니다.
- 활성화하는 동안 소스 연결을 시도합니다. 이는 참조 텍스트가 최신 상태를 유지하는 방식을 설정합니다.
- 텍스트가 변경될 때마다, 설정 가능한 지연 시간(기본값 200ms) 후에 디바운스(debounced) 방식으로 Diff 계산이 예약됩니다.
- Diff가 계산되면 다음 작업을 수행합니다:
    - 설정 가능한 스타일에 따라 시각화를 업데이트합니다: 기호 열(sign column)에 유색 텍스트를 배치하거나 줄 번호에 색상을 입힙니다. 두 스타일 모두 해당 `MiniDiffSign*` 하이라이트 그룹에서 헝크 유형별로 색상이 정의되며, "기호(sign)" 스타일의 기호 텍스트는 `config.view.signs`에서 설정할 수 있습니다.
    - 오버레이 뷰(활성화된 경우)를 업데이트합니다.
    - 현재 버퍼에 대해 `vim.b.minidiff_summary` 및 `vim.b.minidiff_summary_string` 변수를 업데이트합니다. 이는 상태 표시줄(statusline) 등에서 사용할 수 있습니다.
    - `MiniDiffUpdated` `User` 이벤트를 발생시킵니다. 사용 예시는 [`:h MiniDiff-diff-summary`](../doc/mini-diff.qmd#minidiff-diff-summary)를 참조하세요.

참고:

- `:edit` 명령을 사용하여 현재 버퍼를 리셋(비활성화 후 다시 활성화)할 수 있습니다.

### 오버레이 (Overlay)

기본 시각화와 함께 "오버레이"라는 특별한 뷰가 있습니다. 이는 Diff 세부 정보를 일시적으로 확인하기 위한 용도이며 [`MiniDiff.toggle_overlay()`](../doc/mini-diff.qmd#minidiff.toggle_overlay)를 통해 수동으로 토글할 수 있지만, 오버레이가 켜진 상태에서 텍스트를 변경하면 그에 맞춰 반응합니다.

텍스트 영역 내에서 더 많은 Diff 세부 정보를 보여줍니다:

- 추가된 버퍼 줄은 `MiniDiffOverAdd` 하이라이트 그룹으로 강조됩니다.
- 삭제된 참조 줄은 가상 텍스트(virtual text)로 표시되며 `MiniDiffOverDelete` 하이라이트 그룹으로 강조됩니다.
- 변경된 참조 줄은 가상 텍스트로 표시되며 `MiniDiffOverChange` 하이라이트 그룹으로 강조됩니다.

  버퍼 줄과 참조 줄의 개수가 동일한 "변경" 헝크의 경우 특별 처리를 통해 "단어 단위 Diff"를 보여줍니다. 참조 줄이 버퍼 줄 옆에 표시되며, 두 줄의 변경된 부분만 `MiniDiffOverChange`로 강조됩니다. 참조 줄의 나머지 부분은 `MiniDiffOverContext` 하이라이트가 적용됩니다.
  이는 보통 `config.options.linematch`가 활성화되어 있을 때 적용됩니다.

### 매핑 (Mappings)

이 모듈은 Diff와 관련된 일반적인 작업에 대한 매핑을 제공합니다:

- 헝크 적용(apply) 및 리셋(reset).
- "커서 아래의 헝크 범위" 텍스트 오브젝트.
- 첫 번째/이전/다음/마지막 헝크 범위로 이동.

예시:

- `vip` 다음에 `gh` / `gH`를 누르면 현재 단락 내부의 헝크를 적용/리셋합니다. 연산자 형태인 `ghip` / `gHip`으로도 동일한 결과를 얻을 수 있으며, 이는 점 반복이 가능하다는 장점이 있습니다.
- `gh_` / `gH_`는 (전체 헝크가 아니더라도) 현재 줄을 적용/리셋합니다.
- `ghgh` / `gHgh`는 커서 아래의 헝크 범위를 적용/리셋합니다.
- `dgh`는 커서 아래의 헝크 범위를 삭제합니다.
- `[H` / `[h` / `]h` / `]H`는 현재 버퍼의 첫 번째 / 이전 / 다음 / 마지막 헝크 범위로 커서를 이동합니다.

일부 기능에 대한 매핑은 수동으로 수행하는 것을 가정합니다. [`:h MiniDiff.operator()`](../doc/mini-diff.qmd#minidiff.operator)를 참조하세요.

### 버퍼 로컬 변수 (Buffer-local variables)

Diff가 활성화된 각 버퍼는 커스텀 상태 표시줄에서 헝크 개요를 보여주는 데 사용할 수 있는 다음과 같은 버퍼 로컬 변수를 갖습니다:

- `vim.b.minidiff_summary`는 다음과 같은 필드를 갖는 테이블입니다:
    - `source_name` - 소스 이름.
    - `n_ranges` - 헝크 범위(연속된 헝크의 시퀀스) 수.
    - `add` - 추가된 줄 수.
    - `change` - 변경된 줄 수.
    - `delete` - 삭제된 줄 수.

- `vim.b.minidiff_summary_string`은 고정된 형식의 요약 문자열 표현입니다. 그대로 사용하도록 제작되었습니다. 다른 포맷을 사용하려면 `vim.b.minidiff_summary`를 사용하여 직접 만들어 보세요. 가장 좋은 방법은 `MiniDiffUpdated` 이벤트의 콜백에서 `vim.b.minidiff_summary_string`을 덮어쓰는 것입니다:

    ```lua
    local format_summary = function(data)
      local summary = vim.b[data.buf].minidiff_summary
      local t = {}
      if summary.add > 0 then table.insert(t, '+' .. summary.add) end
      if summary.change > 0 then table.insert(t, '~' .. summary.change) end
      if summary.delete > 0 then table.insert(t, '-' .. summary.delete) end
      vim.b[data.buf].minidiff_summary_string = table.concat(t, ' ')
    end
    local au_opts = { pattern = 'MiniDiffUpdated', callback = format_summary }
    vim.api.nvim_create_autocmd('User', au_opts)
    ```

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

    | 브랜치 | 코드 스니펫                                                   |
    |--------|----------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.diff')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.diff', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.diff', version = false },` |
    | Stable | `{ 'nvim-mini/mini.diff', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.diff'`                         |
    | Stable | `Plug 'nvim-mini/mini.diff', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.diff').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 헝크가 시각화되는 방식에 대한 옵션
  view = {
    -- 시각화 스타일. 'sign' 및 'number'가 가능합니다.
    -- 기본값: 줄 번호가 켜져 있으면 'number', 그렇지 않으면 'sign'.
    style = vim.go.number and 'number' or 'sign',

    -- 'sign' 뷰에서 사용되는 기호
    signs = { add = '▒', change = '▒', delete = '▒' },

    -- 사용되는 시각화 extmarks의 우선순위
    priority = 199,
  },

  -- 참조 텍스트가 계산/업데이트되는 방식에 대한 소스
  -- 기본적으로 Git 인덱스의 내용을 사용합니다.
  source = nil,

  -- 비동기 프로세스를 정의하는 지연 시간 (ms)
  delay = {
    -- 텍스트가 변경될 때마다 업데이트하기 전 대기 시간
    text_change = 200,
  },

  -- 모듈 매핑. 비활성화하려면 `''`(빈 문자열)을 사용하세요.
  mappings = {
    -- 비주얼/연산자 영역 내의 헝크 적용
    apply = 'gh',

    -- 비주얼/연산자 영역 내의 헝크 리셋
    reset = 'gH',

    -- 연산자 내부에서 사용될 헝크 범위 텍스트 오브젝트.
    -- 매핑이 apply 및 reset과 다를 경우 비주얼 모드에서도 작동합니다.
    textobject = 'gh',

    -- 해당 방향의 헝크 범위로 이동
    goto_first = '[H',
    goto_prev = '[h',
    goto_next = ']h',
    goto_last = ']H',
  },

  -- 다양한 옵션
  options = {
    -- Diff 알고리즘. `:h vim.diff()` 참조.
    algorithm = 'histogram',

    -- "들여쓰기 휴리스틱(indent heuristic)" 사용 여부. `:h vim.diff()` 참조.
    indent_heuristic = true,

    -- 줄 정렬을 위한 2단계 Diff 양
    linematch = 60,

    -- 헝크 탐색 시 끝에 도달하면 순환(wrap)할지 여부
    wrap_goto = false,
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [lewis6991/gitsigns.nvim](https://github.com/lewis6991/gitsigns.nvim)
