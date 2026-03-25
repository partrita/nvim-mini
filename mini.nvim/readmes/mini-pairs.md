---
title: "mini.pairs"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-pairs_readme.png?raw=true" alt="mini.pairs" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 최소한의 빠른 자동 쌍(Autopairs) 생성

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-pairs.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-pairs)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-pairs.mp4?raw=true)

## 기능 {#features}

- 커서 주변 환경(커서 왼쪽과 오른쪽 문자)에 따라 두 개의 "쌍이 되는" 문자를 처리하는 기능을 제공합니다.
- [`MiniPairs.map()`](../doc/mini-pairs.qmd#minipairs.map) 또는 [`MiniPairs.setup()`](../doc/mini-pairs.qmd#minipairs.setup)(전역 매핑용), [`MiniPairs.map_buf()`](../doc/mini-pairs.qmd#minipairs.map_buf)(버퍼 매핑용)를 사용하여 적절한 매핑을 만들어 사용하는 것을 권장합니다.
- 쌍은 특수 `<BS>`(설정된 모든 모드) 및 `<CR>`(입력 모드 전용) 매핑에 대해 자동으로 등록됩니다. 쌍 내부에서 키를 누르면 쌍 전체를 삭제하거나, 쌍 내부에 빈 줄을 추가합니다. 참고: 기존 매핑을 덮어쓰지 않는 경우에만 이러한 매핑이 자동으로 생성됩니다.

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

    | 브랜치 | 코드 스니펫                                                    |
    |--------|-----------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.pairs')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.pairs', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                   |
    |--------|------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.pairs', version = false },` |
    | Stable | `{ 'nvim-mini/mini.pairs', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                          |
    |--------|-------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.pairs'`                         |
    | Stable | `Plug 'nvim-mini/mini.pairs', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.pairs').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 이 `config`의 매핑이 생성될 모드
  modes = { insert = true, command = false, terminal = false },

  -- 전역 매핑. 각 우항(right hand side)은 쌍 정보여야 하며, 
  -- 최소한 다음 필드들을 포함하는 테이블이어야 합니다 (|MiniPairs.map| 참조):
  -- - <action> - 'open', 'close', 'closeopen' 중 하나.
  -- - <pair> - 사용할 쌍을 나타내는 두 글자 문자열.
  -- 기본적으로 `\` 뒤에는 쌍이 삽입되지 않으며, 따옴표는 <CR>에 의해 인식되지 않고, 
  -- `'`는 글자 뒤에 쌍을 삽입하지 않습니다.
  -- 테이블의 일부만 수정할 수 있습니다 (나머지는 이 기본값을 사용합니다).
  mappings = {
    ['('] = { action = 'open', pair = '()', neigh_pattern = '^[^\\]' },
    ['['] = { action = 'open', pair = '[]', neigh_pattern = '^[^\\]' },
    ['{'] = { action = 'open', pair = '{}', neigh_pattern = '^[^\\]' },

    [')'] = { action = 'close', pair = '()', neigh_pattern = '^[^\\]' },
    [']'] = { action = 'close', pair = '[]', neigh_pattern = '^[^\\]' },
    ['}'] = { action = 'close', pair = '{}', neigh_pattern = '^[^\\]' },

    ['"'] = { action = 'closeopen', pair = '""', neigh_pattern = '^[^\\]',   register = { cr = false } },
    ["'"] = { action = 'closeopen', pair = "''", neigh_pattern = '^[^%a\\]', register = { cr = false } },
    ['`'] = { action = 'closeopen', pair = '``', neigh_pattern = '^[^\\]',   register = { cr = false } },
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [windwp/nvim-autopairs](https://github.com/windwp/nvim-autopairs)
- [jiangmiao/auto-pairs](https://github.com/jiangmiao/auto-pairs)
