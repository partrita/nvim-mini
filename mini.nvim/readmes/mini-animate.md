---
title: "mini.animate"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-animate_readme.png?raw=true" alt="mini.animate" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 일반적인 Neovim 동작 애니메이션화

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-animate.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-animate)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-animate.mp4?raw=true)

## 기능 {#features}

- 단 한 줄의 `require('mini.animate').setup()`으로 즉시 사용 가능합니다. 별도의 매핑이나 명령이 필요하지 않습니다.
- 커스터마이징 가능한 경로를 표시하여 동일한 버퍼 내에서의 **커서 이동**을 애니메이션화합니다.
- 일련의 하위 스크롤로 **스크롤**을 애니메이션화합니다 ("부드러운 스크롤").
- 모든 창의 크기를 점진적으로 변경하여 **창 크기 조정**을 애니메이션화합니다.
- 시각적으로 업데이트되는 플로팅 창을 사용하여 **창 열기/닫기**를 애니메이션화합니다.
- 모든 동작의 타이밍을 개별적으로 커스터마이징할 수 있습니다.
- 각 동작의 애니메이션을 개별적으로 활성화하거나 비활성화할 수 있습니다.
- 모든 애니메이션은 비동기/비차단(non-blocking) 방식으로 작동하며, 애니메이션 완료 후 동작을 수행하는 데 사용할 수 있는 특정 이벤트를 트리거합니다.
- 자신만의 애니메이션을 구현하는 데 사용할 수 있는 [`MiniAnimate.animate()`](../doc/mini-animate.qmd#minianimate.animate) 함수를 제공합니다.

참고:

- 스크롤 및 크기 조정 애니메이션은 효과를 내기 위해 실제로 Neovim의 상태를 변경하며 비동기적으로 작동합니다. 이로 인해 다음과 같은 문제가 발생할 수 있습니다:
    - 이동 후 중앙으로 맞추도록 매핑한 경우(예: `nzvzz` 또는 `<C-d>zz`), 해당 매핑을 변경해야 합니다. 매핑을 제거하거나 [`MiniAnimate.execute_after()`](../doc/mini-animate.qmd#minianimate.execute_after)를 사용하도록 업데이트하세요 ([`:h MiniAnimate.config.scroll`](../doc/mini-animate.qmd#minianimate.config.scroll) 참조).
    - 마우스 휠을 사용한 스크롤이 느려 보이거나 시각적인 떨림이 발생할 수 있습니다. 이는 보통 초당 휠 회전 수가 많아 각 회전이 이전 애니메이션을 덮어쓰고 새로운 애니메이션을 시작하기 때문입니다. 이를 완화하려면 'mousescroll' 옵션을 수정하거나(세로 스크롤을 1로 설정하고 빠른 회전 속도를 사용하거나, 높은 값으로 설정하고 한 번에 한 번씩 회전), `config.scroll`을 수정하여 스크롤 애니메이션의 시점과 방식을 미세하게 조정하세요.

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

    | 브랜치 | 코드 스니펫                                                      |
    |--------|-------------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.animate')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.animate', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                     |
    |--------|--------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.animate', version = false },` |
    | Stable | `{ 'nvim-mini/mini.animate', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                            |
    |--------|---------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.animate'`                         |
    | Stable | `Plug 'nvim-mini/mini.animate', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.animate').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 커서 경로
  cursor = {
    -- 애니메이션 활성화 여부
    enable = true,

    -- 애니메이션 타이밍 (시간에 따른 단계 진행 방식)
    timing = --<함수: 250ms 동안 선형 애니메이션 구현>,

    -- 시각화된 커서 이동을 위한 경로 생성기
    path = --<함수: 1000자 이내의 최단 경로 구현>,
  },

  -- 세로 스크롤
  scroll = {
    -- 애니메이션 활성화 여부
    enable = true,

    -- 애니메이션 타이밍 (시간에 따른 단계 진행 방식)
    timing = --<함수: 250ms 동안 선형 애니메이션 구현>,

    -- 전체 스크롤을 기반으로 한 하위 스크롤 생성기
    subscroll = --<함수: 최대 60단계의 균등 스크롤 구현>,
  },

  -- 창 크기 조정
  resize = {
    -- 애니메이션 활성화 여부
    enable = true,

    -- 애니메이션 타이밍 (시간에 따른 단계 진행 방식)
    timing = --<함수: 250ms 동안 선형 애니메이션 구현>,

    -- 모든 크기 조정 단계에 대한 하위 생성기
    subresize = --<함수: 균등한 선형 단계 구현>,
  },

  -- 창 열기
  open = {
    -- 애니메이션 활성화 여부
    enable = true,

    -- 애니메이션 타이밍 (시간에 따른 단계 진행 방식)
    timing = --<함수: 250ms 동안 선형 애니메이션 구현>,

    -- 특정 창을 시각화하는 플로팅 창 설정 생성기
    winconfig = --<함수: 25단계 동안의 정적 창 구현>,

    -- 플로팅 창의 'winblend' (창 투명도) 생성기
    winblend = --<함수: 80에서 100까지의 균등 선형 단계 구현>,
  },

  -- 창 닫기
  close = {
    -- 애니메이션 활성화 여부
    enable = true,

    -- 애니메이션 타이밍 (시간에 따른 단계 진행 방식)
    timing = --<함수: 250ms 동안 선형 애니메이션 구현>,

    -- 특정 창을 시각화하는 플로팅 창 설정 생성기
    winconfig = --<함수: 25단계 동안의 정적 창 구현>,

    -- 플로팅 창의 'winblend' (창 투명도) 생성기
    winblend = --<함수: 80에서 100까지의 균등 선형 단계 구현>,
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [Neovide](https://neovide.dev/) (Neovim GUI, 플러그인이 아님)
- [edluffy/specs.nvim](https://github.com/edluffy/specs.nvim)
- [karb94/neoscroll.nvim](https://github.com/karb94/neoscroll.nvim)
- [anuvyklack/windows.nvim](https://github.com/anuvyklack/windows.nvim)
