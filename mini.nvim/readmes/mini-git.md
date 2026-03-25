---
title: "mini.git"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-git_readme.png?raw=true" alt="mini.git" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### Git 통합

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-git.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-git)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-git.mp4?raw=true)

**참고**: 이 데모에서는 [mini.notify](https://nvim-mini.org/mini.nvim/readmes/mini-notify)의 커스텀 `vim.notify()`와 [mini.diff](https://nvim-mini.org/mini.nvim/readmes/mini-diff)의 Diff 줄 번호 하이라이팅을 사용합니다.

## 기능 {#features}

- [Git](https://git-scm.com/) 관련 데이터(루트 경로, 상태, HEAD 등)를 자동 추적합니다. 상태 표시줄(statusline)에서 편리하게 사용할 수 있도록 버퍼 로컬 변수를 제공합니다.

- 파일의 저장소 루트에서 `git` 호출을 실행하는 [`:Git`](../doc/mini-git.qmd#git) 명령을 제공합니다. 현재 인스턴스와의 긴밀한 통합(출력을 알림/버퍼로 표시, 커밋 메시지 편집에 사용 등)을 지원합니다.

- Git 이력을 검토하기 위한 헬퍼 함수:
    - [`MiniGit.show_range_history()`](../doc/mini-git.qmd#minigit.show_range_history)는 특정 줄 범위의 변화 과정을 보여줍니다.
    - [`MiniGit.show_diff_source()`](../doc/mini-git.qmd#minigit.show_diff_source)는 Diff 항목 시점의 파일 상태를 보여줍니다.
    - [`MiniGit.show_at_cursor()`](../doc/mini-git.qmd#minigit.show_at_cursor)는 컨텍스트에 따라 Git 관련 데이터를 보여줍니다.

수행하지 않는 작업:

- 전문적인 Git 클라이언트를 완전히 대체하지는 않습니다. 기준점: 해당 기능이 현재 Neovim의 상태(열려 있는 버퍼 등)에 의존하지 않는다면, 이 모듈의 범위를 벗어난 것입니다. 더 많은 기능을 원한다면 ['mini.diff'](https://nvim-mini.org/mini.nvim/readmes/mini-diff)나 전문 Git 클라이언트를 사용하세요.

더 자세한 정보는 도움말의 다음 부분을 참조하세요:

- [`:h :Git`](../doc/mini-git.qmd#git)
- [`:h MiniGit-examples`](../doc/mini-git.qmd#minigit-examples)
- [`:h MiniGit.enable()`](../doc/mini-git.qmd#minigit.enable)
- [`:h MiniGit.get_buf_data()`](../doc/mini-git.qmd#minigit.get_buf_data)

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
    | Main   | `add('nvim-mini/mini-git')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini-git', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini-git', version = false },` |
    | Stable | `{ 'nvim-mini/mini-git', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini-git'`                         |
    | Stable | `Plug 'nvim-mini/mini-git', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.git').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 일반 CLI 실행
  job = {
    -- Git 실행 파일 경로
    git_executable = 'git',

    -- 강제 종료 전 각 작업의 타임아웃 (ms)
    timeout = 30000,
  },

  -- [`:Git`](../doc/mini-git.qmd#git) 명령 옵션
  command = {
    -- 기본 화면 분할 방향
    split = 'auto',
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [tpope/vim-fugitive](https://github.com/tpope/vim-fugitive)
- [NeogitOrg/neogit](https://github.com/NeogitOrg/neogit)
- [lewis6991/gitsigns.nvim](https://github.com/lewis6991/gitsigns.nvim)
