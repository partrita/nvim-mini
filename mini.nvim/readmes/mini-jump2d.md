---
title: "mini.jump2d"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-jump2d_readme.png?raw=true" alt="mini.jump2d" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 반복적인 레이블 필터링을 통한 가시적 줄 내 점프

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-jump2d.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-jump2d)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-jump2d.mp4?raw=true)

## 기능 {#features}

- 동등하게 고려되는 가능한 점프 지점들을 하나만 남을 때까지 반복적으로 필터링하여 점프합니다. 필터링은 점프 지점에 표시되는 레이블 문자를 입력하여 수행됩니다.
- 커스터마이징 가능:
    - 합리적인 기본값과 함께 점프 지점을 계산하는 방식.
    - 반복 필터링 동안 점프 지점에 레이블을 붙이는 데 사용되는 문자들.
    - 시각적 효과: 몇 단계 앞까지 보여줄지, 지점이 있는 줄을 어둡게 처리할지 등.
    - 점프 과정 중 특정 이벤트에서 실행될 액션 후크(hooks).
    - 허용되는 창: 현재 창 및/또는 현재 창이 아닌 창.
    - 허용되는 줄: 빈 줄이나 접힌(folded) 줄 처리 여부, 커서 위/현재/아래 줄 처리 여부 등. 예를 들어, 현재 창의 커서 아래 줄에서만 지점을 찾도록 설정할 수 있습니다.
- 비주얼 및 연산자 대기(점 반복 지원) 모드에서 작동합니다.
- 미리 구성된 점프 지점 계산 방식 제공 (`MiniJump2d.builtin_opts()` 도움말 참조):
    - 줄의 시작 부분.
    - 단어의 시작 부분.
    - 사용자 입력으로부터 받은 단일 문자.
    - 사용자 입력으로부터 받은 가변 길이 쿼리.
- 멀티바이트 문자를 지원합니다.

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
    | Main   | `add('nvim-mini/mini.jump2d')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.jump2d', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.jump2d', version = false },` |
    | Stable | `{ 'nvim-mini/mini.jump2d', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.jump2d'`                         |
    | Stable | `Plug 'nvim-mini/mini.jump2d', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.jump2d').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 특정 줄에 대해 점프 지점(바이트 인덱스)을 생성하는 함수.
  -- 자세한 내용은 |MiniJump2d.start|를 참조하세요.
  -- `nil` (기본값)인 경우 - |MiniJump2d.default_spotter|를 사용합니다.
  spotter = nil,

  -- 점프 지점 레이블에 사용되는 문자들 (제공된 순서대로)
  labels = 'abcdefghijklmnopqrstuvwxyz',

  -- 시각적 효과 옵션
  view = {
    -- 하나 이상의 점프 지점이 있는 줄을 어둡게 처리할지 여부
    dim = false,

    -- 몇 단계 앞까지 보여줄지. 모든 단계를 보려면 큰 값을 설정하세요.
    n_steps_ahead = 0,
  },

  -- 어떤 줄을 사용하여 지점을 계산할지 결정
  allowed_lines = {
    blank = true, -- 빈 줄 (`true`여도 spotter로 전달되지는 않음)
    cursor_before = true, -- 커서 줄 이전의 줄들
    cursor_at = true, -- 커서 줄
    cursor_after = true, -- 커서 줄 이후의 줄들
    fold = true, -- 접힌 부분의 시작 (`true`여도 spotter로 전달되지는 않음)
  },

  -- 현재 탭페이지에서 가시적인 줄을 찾을 창들을 결정
  allowed_windows = {
    current = true,
    not_current = true,
  },

  -- 특정 이벤트에서 실행될 함수들
  hooks = {
    before_start = nil, -- 점프 시작 전
    after_jump = nil, -- 실제로 점프가 완료된 후
  },

  -- 모듈 매핑. 비활성화하려면 `''`(빈 문자열)을 사용하세요.
  mappings = {
    start_jumping = '<CR>',
  },

  -- 에러가 아닌 피드백 표시 여부
  -- 이는 사용자 입력이 필요할 때 유휴 시간 후 표시되는 정보 메시지에도 영향을 미칩니다.
  silent = false,
}
```

## 유사한 플러그인 {#similar-plugins}

- [phaazon/hop.nvim](https://github.com/phaazon/hop.nvim) (이 모듈의 주요 디자인 영감)
- [ggandor/lightspeed.nvim](https://github.com/ggandor/lightspeed.nvim)
- [ggandor/leap.nvim](https://github.com/ggandor/leap.nvim)
- [rlane/pounce.nvim](https://github.com/rlane/pounce.nvim)
