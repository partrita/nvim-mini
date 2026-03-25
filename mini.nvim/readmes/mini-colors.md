---
title: "mini.colors"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-colors_readme.png?raw=true" alt="mini.colors" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 컬러 스킴 조정 및 저장

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-colors.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-colors)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-colors.mp4?raw=true)

## 기능 {#features}

- 컬러 스킴 오브젝트 생성 ([`:h MiniColors-colorscheme`](../doc/mini-colors.qmd#minicolors-colorscheme) 참조): 수동으로 생성하거나 ([`:h MiniColors.as_colorscheme()`](../doc/mini-colors.qmd#minicolors.as_colorscheme)) 현재 활성화된 컬러 스킴을 포함한 기존 컬러 스킴을 쿼리하여 생성할 수 있습니다 ([`:h MiniColors.get_colorscheme()`](../doc/mini-colors.qmd#minicolors.get_colorscheme)).

- 컬러 스킴에 대한 데이터 유추 및 이를 기반으로 한 수정:
    - 배경색을 제거하여 투명도 추가 (터미널 에뮬레이터의 투명도 설정 필요).
    - GUI 색상을 기반으로 cterm 속성을 유추하여 'notermguicolors' 환경에서도 호환되도록 만듭니다.
    - 하이라이트 그룹 링크를 해결(resolve)합니다.
    - 중복된 하이라이트 그룹을 제거하여 압축합니다.
    - 사용된 색상의 팔레트를 추출하고 이를 기반으로 터미널 색상을 유추합니다.

- 취향이나 목적에 맞게 색상 수정:
    - 색상 HEX 문자열에 임의의 함수를 적용합니다.
    - 채널(명도, 채도, 색상, 온도, RGB 등)을 업데이트합니다.
      직접 정의한 함수나 다음의 구현된 메서드 중 하나를 사용하세요:
        - 채널에 값을 더하거나 계수를 곱합니다. 예를 들어 "모든 색상의 채도에 10 더하기"나 "채도에 2 곱하기"를 통해 색상을 더 선명하게(덜 회색으로) 만들 수 있습니다.
        - 반전(Invert). 예를 들어 "명도 반전"을 통해 다크/라이트 테마 간 변환이 가능합니다.
        - 특정 값으로 설정 (현재 값과 가장 가까운 값을 선택). 예를 들어 "하나 또는 두 개의 색상으로 설정"하여 단색 또는 2색 컬러 스킴을 만들 수 있습니다.
        - 특정 소스로부터 멀어지게(repel) 하여, 가까운 값일수록 더 강한 효과를 줍니다. 예를 들어 "hue 30에서 멀어지기"를 통해 컬러 스킴에서 붉은색을 제거할 수 있습니다. 멀어지는 정도는 설정 가능합니다.
    - 색각 이상(color vision deficiency)을 시뮬레이션합니다.

- 컬러 스킴이 완성되면, 효과를 즉시 확인하기 위해 적용하거나 독립적인 컬러 스킴 파일(Lua)로 저장할 수 있습니다.

- 피드백과 함께 대화식으로 실험해 보세요.

- [`MiniColors.animate()`](../doc/mini-colors.qmd#minicolors.animate) 또는 [`:Colorscheme`](../doc/mini-colors.qmd#colorscheme) 사용자 명령을 통해 컬러 스킴 간의 전환을 애니메이션화합니다.

- 지원되는 색 공간 내에서 색상을 변환합니다 ([`MiniColors.convert()`](../doc/mini-colors.qmd#minicolors.convert)):
    - HEX 문자열.
    - 8비트 숫자 (터미널 색상).
    - RGB.
    - Oklab, Oklch, Okhsl (https://bottosson.github.io/posts/oklab/).

## 조정 빠른 시작 {#tweak-quick-start}

- `:lua require('mini.colors').interactive()`를 실행합니다.
- 노출된 컬러 스킴 메서드 호출을 작성하고 `<M-a>`로 적용하며 실험해 봅니다. 자세한 내용은 [`:h MiniColors-colorscheme-methods`](../doc/mini-colors.qmd#minicolors-colorscheme-methods) 및 [`:h MiniColors-recipes`](../doc/mini-colors.qmd#minicolors-recipes)를 참조하세요.
- 결과가 만족스러우면 `<M-w>`로 컬러 스킴을 저장합니다. 만족스럽지 않다면 `<M-r>`로 초기 컬러 스킴으로 리셋합니다.
- 일부 하이라이트 그룹만 수정이 필요한 경우, 저장된 컬러 스킴 파일 내에서 수동으로 조정하세요.

## 설치 {#installation}

이 플러그인은 'mini.nvim' 라이브러리의 일부로 설치하거나(**권장**), 독립적인 Git 저장소로 설치할 수 있습니다.

두 가지 브랜치 중 하나를 골라 설치할 수 있습니다:

- `main` (기본값, **권장**): 플러그인의 최신 개발 버전입니다. 마지막 안정 릴리스 이후의 모든 변경 사항은 베타 테스트 단계(알파 테스트를 통과하고 어느 정도 안정됨을 의미)로 간주되어야 합니다.
- `stable`: `main` 브랜치에서 공개 베타 테스트를 거친 코드가 포함된 릴리스 시에만 업데이트됩니다.

다음은 몇 가지 일반적인 설치 방법ของ 코드 스니펫입니다 (하나만 사용하세요):

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
    | Main   | `add('nvim-mini/mini.colors')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.colors', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.colors', version = false },` |
    | Stable | `{ 'nvim-mini/mini.colors', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.colors'`                         |
    | Stable | `Plug 'nvim-mini/mini.colors', { 'branch': 'stable' }` |

</details>

**중요**: `require('mini.colors').setup()`을 호출할 필요는 없지만, 사용 편의성을 높이기 위해 호출할 수 있습니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{}
```

## 유사한 플러그인 {#similar-plugins}

- [rktjmp/lush.nvim](https://github.com/rktjmp/lush.nvim)
- [lifepillar/vim-colortemplate](https://github.com/lifepillar/vim-colortemplate)
- [tjdevries/colorbuddy.nvim](https://github.com/tjdevries/colorbuddy.nvim)
