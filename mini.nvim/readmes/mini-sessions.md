---
title: "mini.sessions"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-sessions_readme.png?raw=true" alt="mini.sessions" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 세션 관리 (읽기, 쓰기, 삭제)

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-sessions.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-sessions)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-sessions.mp4?raw=true)

## 기능 {#features}

- `:mksession`을 기반으로 작동합니다 (`'sessionoptions'`가 완전히 준수됩니다).
- 전역 세션(설정된 디렉터리에서 가져옴)과 로컬 세션(현재 디렉터리에서 가져옴)을 모두 지원합니다.
- 새로운 세션이 자동으로 생성되지 않습니다. 수동으로 [`MiniSessions.write()`](../doc/mini-sessions.qmd#minisessions.write)를 사용하세요.
- Neovim이 다른 것을 실행하려는 의도 없이 호출된 경우, 기본 세션(로컬 세션이 감지되면 로컬, 그렇지 않으면 마지막으로 작성된 전역 세션)을 자동으로 읽어옵니다(Autoread).
- Neovim을 종료하기 전에 현재 읽어온 세션을 자동으로 작성합니다(Autowrite).
- 모든 액션의 강제 실행 여부(severity level)를 설정할 수 있습니다.

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

    | 브랜치 | 코드 스니펫                                                       |
    |--------|--------------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.sessions')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.sessions', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                      |
    |--------|---------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.sessions', version = false },` |
    | Stable | `{ 'nvim-mini/mini.sessions', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                             |
    |--------|----------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.sessions'`                         |
    | Stable | `Plug 'nvim-mini/mini.sessions', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.sessions').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- Neovim이 파일 인자 없이 열렸을 때 기본 세션을 읽어올지 여부
  autoread = false,

  -- 현재 읽어온 세션을 떠나기 전에 자동으로 작성할지 여부
  autowrite = true,

  -- 전역 세션이 저장되는 디렉터리 (비활성화하려면 `''` 사용)
  directory = --<|stdpath()|에서 가져온 사용자 데이터 디렉터리의 "session" 하위 디렉터리>,

  -- 로컬 세션을 위한 파일명 (비활성화하려면 `''` 사용)
  file = 'Session.vim',

  -- 잠재적으로 유해할 수 있는 액션을 강제 실행할지 여부 (함수에 따라 의미가 다름)
  force = { read = false, write = true, delete = false },

  -- 액션을 위한 후크(hook) 함수들. 기본값 `nil`은 '아무것도 하지 않음'을 의미합니다.
  hooks = {
    -- 성공적인 액션 전
    pre = { read = nil, write = nil, delete = nil },
    -- 성공적인 액션 후
    post = { read = nil, write = nil, delete = nil },
  },

  -- 액션 완료 후 세션 경로를 출력할지 여부
  verbose = { read = false, write = true, delete = true },
}
```

## 유사한 플러그인 {#similar-plugins}

- [mhinz/vim-startify](https://github.com/mhinz/vim-startify)
- [Shatur/neovim-session-manager](https://github.com/Shatur/neovim-session-manager)
