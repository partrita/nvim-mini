---
title: "mini.move"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-move_readme.png?raw=true" alt="mini.move" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 선택 영역을 사방으로 자유롭게 이동

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-move.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-move)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-move.mp4?raw=true)

## 기능 {#features}

- 두 가지 모드에서 대상을 이동합니다:
    - 비주얼 모드: 텍스트를 선택한 후(문자 단위 `v`, 줄 단위 `V`, 블록 단위 `CTRL-V`) 상하좌우 네 방향으로 이동할 수 있도록 구성된 매핑을 누릅니다. 이동 후에도 비주얼 모드가 유지됩니다.
    - 노멀 모드: 현재 줄을 상하좌우 네 방향으로 이동하도록 구성된 매핑을 누릅니다.
    - 줄 단위 이동에 대한 특수 처리:
        - 수직 이동 시 `=`를 통해 자동으로 들여쓰기가 조정됩니다.
        - 수평 이동 시 `>` / `<`를 개선하여 들여쓰기/내어쓰기가 수행됩니다.
        - 선택 영역과 함께 커서가 이동합니다.
- 이동을 위한 매핑과 Lua 함수를 모두 제공합니다. [`:h MiniMove.move_selection()`](../doc/mini-move.qmd#minimove.move_selection) 및 [`:h MiniMove.move_line()`](../doc/mini-move.qmd#minimove.move_line)을 참조하세요.
- `v:count`를 지원합니다. 매핑 앞에 숫자를 입력하여 이동 횟수를 지정할 수 있습니다.
- 연속적인 모든 이동은 어떤 방향이든 상관없이 단 한 번의 `u` 입력으로 모두 취소할 수 있습니다.
- 수직 이동 시 선호하는 열(preferred column)을 준수합니다. 커서가 움직이는 방식과 동일하게 선택 영역을 수직으로 이동합니다 (대상이 되는 줄에 원본 열이 존재하지 않는 경우 등 엄격하게 수직이 아닐 수 있음).

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
    | Main   | `add('nvim-mini/mini.move')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.move', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.move', version = false },` |
    | Stable | `{ 'nvim-mini/mini.move', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.move'`                         |
    | Stable | `Plug 'nvim-mini/mini.move', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.move').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 모듈 매핑. 비활성화하려면 `''`(빈 문자열)을 사용하세요.
  mappings = {
    -- 비주얼 모드에서 비주얼 선택 영역 이동. 기본값은 Alt (Meta) + hjkl입니다.
    left = '<M-h>',
    right = '<M-l>',
    down = '<M-j>',
    up = '<M-k>',

    -- 노멀 모드에서 현재 줄 이동
    line_left = '<M-h>',
    line_right = '<M-l>',
    line_down = '<M-j>',
    line_up = '<M-k>',
  },

  -- 이동 동작을 제어하는 옵션
  options = {
    -- 줄 단위 수직 이동 중 선택 영역 들여쓰기 자동 조정
    reindent_linewise = true,
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [matze/vim-move](https://github.com/matze/vim-move)
- [booperlv/nvim-gomove](https://github.com/booperlv/nvim-gomove)
