---
title: "mini.map"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-map_readme.png?raw=true" alt="mini.map" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 버퍼 텍스트 개요, 스크롤바 및 하이라이트 표시

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-map.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-map)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-map.mp4?raw=true)

## 기능 {#features}

- 현재 버퍼 텍스트의 자동으로 업데이트되는 개요(overview)를 보여주는 특별한 플로팅 창을 표시하고 관리합니다. 창은 Neovim 인스턴스의 전체 높이를 차지하며 왼쪽 또는 오른쪽에 고정됩니다. 맵(map)의 콘텐츠는 현재 모든 줄을 가져와 이진 공백/비공백 마스크로 변환하고, 적절한 크기로 조정(rescale)한 다음, 특수 인코딩 기호로 구성된 문자열로 다시 변환하여 계산됩니다. 이 모든 과정이 **매우 빠르고 비동기적으로** 이루어집니다.

    [`:h MiniMap.open()`](../doc/mini-map.qmd#minimap.open), [`:h MiniMap.refresh()`](../doc/mini-map.qmd#minimap.refresh), [`:h MiniMap.close()`](../doc/mini-map.qmd#minimap.close), [`:h MiniMap.toggle()`](../doc/mini-map.qmd#minimap.toggle), [`:h MiniMap.toggle_side()`](../doc/mini-map.qmd#minimap.toggle_side)를 참조하세요.

    일반적인 개요 및 팁은 [`:h mini.map-usage`](../doc/mini-map.qmd#mini.map-usage)를 참조하세요.

- 맵 콘텐츠 옆에 스크롤바를 표시합니다. 스크롤바는 현재 줄(line)과 뷰(view, 상단 및 하단 가시 줄)를 나타냅니다. 스크롤바만 표시하도록 설정하여 맵 창을 "순수 스크롤바"로 사용할 수도 있습니다.

- 현재 버퍼의 특정 데이터를 나타내는 맵 줄을 하이라이트합니다. 이는 확장 가능한 콜러블(callables) 세트인 통합(integrations) 기능을 통해 수행됩니다. 일반적인 사용 사례를 위한 사전에 빌드된 생성기들이 제공됩니다:
    - 내장 검색.
    - 내장 진단(diagnostic).
    - ['mini.diff'](https://nvim-mini.org/mini.nvim/readmes/mini-diff)에서 제공되는 일반적인 Diff 헝크(hunks).
    - ['lewis6991/gitsigns.nvim'](https://github.com/lewis6991/gitsigns.nvim)에서 제공되는 헝크.
    자세한 내용은 [`:h MiniMap.gen_integration`](../doc/mini-map.qmd#minimap.gen_integration)을 참조하세요.

- 맵 창에 포커스를 맞춰 현재 (소스) 버퍼를 빠르게 훑어볼 수 있습니다. 맵 창 안에서 이동하면 소스 창의 커서 위치가 업데이트되어 빠르고 정확한 버퍼 탐색이 가능합니다. 다시 원래대로 돌아오려면 `<CR>`을 눌러 탐색된 위치를 수락하거나, `<Esc>`를 눌러 원래 위치로 돌아갑니다. [`:h MiniMap.toggle_focus()`](../doc/mini-map.qmd#minimap.toggle_focus)를 참조하세요.

- 커스터마이징 가능:
    - 다양한 해상도(기본값 3x2)의 이진 정보를 표시하는 데 사용되는 인코딩 기호. 다양한 기본 문자군과 해상도를 위한 사전에 빌드된 생성기가 있습니다. [`:h MiniMap.gen_encode_symbols`](../doc/mini-map.qmd#minimap.gen_encode_symbols)를 참조하세요.
    - 줄(line)과 뷰(view)를 위한 별도의 스크롤바 기호. 너비를 자유롭게 설정할 수 있습니다 (0으로 설정하면 사실상 스크롤바를 비활성화함).
    - 맵 줄 하이라이트를 생성하는 통합(integrations) 기능.
    - 창 옵션: 위치(왼쪽/오른쪽), 너비, 'winblend' 등.

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
    | Main   | `add('nvim-mini/mini.map')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.map', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.map', version = false },` |
    | Stable | `{ 'nvim-mini/mini.map', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.map'`                         |
    | Stable | `Plug 'nvim-mini/mini.map', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.map').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 하이라이트 통합 (기본적으로 없음)
  integrations = nil,

  -- 데이터를 표시하는 데 사용될 기호들
  symbols = {
    -- 인코딩 기호. 명세는 [`:h MiniMap.config`](../doc/mini-map.qmd#minimap.config)를,
    -- 사전에 빌드된 것들은 [`:h MiniMap.gen_encode_symbols`](../doc/mini-map.qmd#minimap.gen_encode_symbols)를 참조하세요.
    -- 기본값: 3x2 해상도의 꽉 찬 블록.
    encode = nil,

    -- 뷰(view) 및 줄(line)을 위한 스크롤바 기호. 비활성화하려면 빈 문자열을 사용하세요.
    scroll_line = '█',
    scroll_view = '┃',
  },

  -- 창 옵션
  window = {
    -- 일반적인 방식(`wincmd` 또는 마우스)으로 창에 포커스를 맞출 수 있는지 여부
    focusable = false,

    -- 고정될 위치 ('left' 또는 'right')
    side = 'right',

    -- 여러 통합 하이라이트의 개수 표시 여부
    show_integration_count = true,

    -- 전체 너비
    width = 10,

    -- 'winblend' 옵션 값
    winblend = 25,

    -- Z-인덱스
    zindex = 10,
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [wfxr/minimap.vim](https://github.com/wfxr/minimap.vim)
- [dstein64/nvim-scrollview](https://github.com/dstein64/nvim-scrollview)
- [petertriho/nvim-scrollbar](https://github.com/petertriho/nvim-scrollbar)
- [lewis6991/satellite.nvim](https://github.com/lewis6991/satellite.nvim)
