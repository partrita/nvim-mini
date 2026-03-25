---
title: "mini.cmdline"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-cmdline_readme.png?raw=true" alt="mini.cmdline" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 커맨드 라인(Command line) 개선

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-cmdline.qmd)를 참조하세요.

---

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-cmdline)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-cmdline.mp4?raw=true)

## 기능 {#features}

- 설정 가능한 지연 시간과 함께 자동 완성을 제공합니다. [`:h cmdline-completion`](https://neovim.io/doc/user/helptag.html?tag=cmdline-completion) 및 수동 [`:h 'wildchar'`](https://neovim.io/doc/user/helptag.html?tag='wildchar') 입력 경험을 개선합니다. Neovim>=0.11이 필요하며, Neovim>=0.12를 권장합니다.

- 입력하는 동안 단어를 자동 수정(Autocorrect)합니다. 기본적으로 명령어나 옵션처럼 고정된 후보군에서 가져와야 하는 단어들만 자동 수정됩니다.

- 입력하는 동안 명령어의 범위(range)를 미리 보여줍니다(Autopeek). 범위에 해당하는 줄과 설정 가능한 컨텍스트 줄을 플로팅 창으로 보여줍니다.

수행하지 않는 작업:

- 커맨드 라인 UI의 커스터마이징. Neovim>=0.12에서 [`:h vim._extui`](https://neovim.io/doc/user/helptag.html?tag=vim._extui)를 사용하세요.

- 자동 완성 후보의 커스터마이징. 후보는 [`:h cmdline-completion`](https://neovim.io/doc/user/helptag.html?tag=cmdline-completion)을 통해 계산됩니다.

## 설치 {#installation}

이 플러그인은 'mini.nvim' 라이브러리의 일부로 설치하거나(**권장**), 독립적인 Git 저장소로 설치할 수 있습니다.

베타 테스트 단계에서는 설치할 수 있는 브랜치가 하나만 있습니다:

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
    | Main   | `add('nvim-mini/mini.cmdline')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.cmdline', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.cmdline', version = false },` |
    | Stable | `{ 'nvim-mini/mini.cmdline', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.cmdline'`                         |
    | Stable | `Plug 'nvim-mini/mini.cmdline', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.cmdline').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 자동 완성: 입력하는 동안 `:h 'wildmenu'`를 표시합니다.
  autocomplete = {
    enable = true,

    -- 보완을 트리거할 지연 시간 (ms)
    -- 양수 값을 사용하려면 Neovim>=0.12를 권장합니다.
    delay = 0,

    -- 보완을 트리거할 때의 사용자 정의 규칙
    predicate = nil,

    -- 더 일관된 wildmenu 동작을 위해 화살표 키를 매핑할지 여부
    map_arrows = true,
  },

  -- 자동 수정: 존재하지 않는 단어(명령어, 옵션 등)를 조정합니다.
  autocorrect = {
    enable = true,

    -- 사용자 정의 자동 수정 규칙
    func = nil,
  },

  -- Autopeek: 플로팅 창에 명령어의 대상 범위를 표시합니다.
  autopeek = {
    enable = true,

    -- 범위 줄의 위아래로 표시할 컨텍스트 줄 수
    n_context = 1,

    -- 미리보기 창을 표시할 때의 사용자 정의 규칙
    predicate = nil,

    -- 창 옵션
    window = {
      -- 플로팅 창 설정
      config = {},

      -- statuscolumn을 렌더링하는 함수
      statuscolumn = nil,
    },
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [folke/noice.nvim](https://github.com/folke/noice.nvim)
- [nacro90/numb.nvim](https://github.com/nacro90/numb.nvim)
- 내장 [cmdline-autocompletion](https://neovim.io/doc/user/helptag.html?tag=cmdline-autocompletion) (Neovim>=0.12)
