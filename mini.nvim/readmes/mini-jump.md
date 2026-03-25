---
title: "mini.jump"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-jump_readme.png?raw=true" alt="mini.jump"  style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 다음/이전 단일 문자로 점프

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-jump.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-jump)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

초기 아이디어 및 구현은 [Adam Blažek](https://github.com/xigoi)에 의해 이루어졌습니다.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-jump.mp4?raw=true)

## 기능 {#features}

- `f`, `F`, `t`, `T` 기능을 확장하여 여러 줄에서 작동하도록 합니다.
- `f`, `F`, `t`, `T`를 다시 눌러 점프를 반복할 수 있습니다. 점프가 아닌 이유로 커서가 이동하거나 유휴 시간(설정 가능)이 지나면 점프 반복 상태가 초기화됩니다.
- 설정 가능한 지연 시간 후에 가능한 모든 대상 문자를 하이라이트하고, 설정 가능한 유휴 시간이 지나면 하이라이트를 중단합니다.
- 노멀, 비주얼, 연산자 대기(Neovim과 동일하게 점 반복 지원) 모드를 지원합니다.

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
    | Main   | `add('nvim-mini/mini.jump')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.jump', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.jump', version = false },` |
    | Stable | `{ 'nvim-mini/mini.jump', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.jump'`                         |
    | Stable | `Plug 'nvim-mini/mini.jump', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.jump').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 모듈 매핑. 비활성화하려면 `''`(빈 문자열)을 사용하세요.
  mappings = {
    forward = 'f',
    backward = 'F',
    forward_till = 't',
    backward_till = 'T',
    repeat_jump = ';',
  },

  -- 다양한 기능을 위한 지연 시간(ms). 비활성화하려면 아주 큰 값(예: 10^7)을 설정하세요.
  delay = {
    -- 점프 후 가능한 모든 점프 대상을 하이라이트할 때까지의 지연 시간
    highlight = 250,

    -- 점프 후 아무 작업이 없을 때(유휴 상태) 자동으로 중지할 때까지의 지연 시간
    idle_stop = 10000000,
  },

  -- 에러가 아닌 피드백 표시 여부
  -- 이는 사용자 입력이 필요할 때 유휴 시간 후 표시되는 정보 메시지에도 영향을 미칩니다.
  silent = false,
}
```

## 유사한 플러그인 {#similar-plugins}

- [rhysd/clever-f.vim](https://github.com/rhysd/clever-f.vim)
- [justinmk/vim-sneak](https://github.com/justinmk/vim-sneak)
