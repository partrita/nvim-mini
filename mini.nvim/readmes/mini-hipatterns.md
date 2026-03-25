---
title: "mini.hipatterns"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-hipatterns_readme.png?raw=true" alt="mini.hipatterns" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 텍스트 내 패턴 하이라이트

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-hipatterns.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-hipatterns)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-hipatterns.mp4?raw=true)

## 기능 {#features}

- 설정 가능한 패턴과 하이라이트 그룹(문자열 또는 콜러블)을 사용하여 텍스트를 하이라이트합니다.

- 하이라이트는 설정 가능한 디바운스(debounce) 지연 시간과 함께 비동기적으로 업데이트됩니다.

- 버퍼 내의 일치 항목을 가져오는 함수를 제공합니다.

일반적인 사용 사례 예시는 [`:h MiniHipatterns-examples`](../doc/mini-hipatterns.qmd#minihipatterns-examples)를 참조하세요.

참고:

- 기본적으로는 아무런 하이라이터도 정의되어 있지 않습니다. 시각적인 효과를 보려면 `config.highlighters`에 추가해야 합니다.

## 사용 예시 {#example-usage}

```lua
local hipatterns = require('mini.hipatterns')
hipatterns.setup({
  highlighters = {
    -- 독립된 'FIXME', 'HACK', 'TODO', 'NOTE' 하이라이트
    fixme = { pattern = '%f[%w]()FIXME()%f[%W]', group = 'MiniHipatternsFixme' },
    hack  = { pattern = '%f[%w]()HACK()%f[%W]',  group = 'MiniHipatternsHack'  },
    todo  = { pattern = '%f[%w]()TODO()%f[%W]',  group = 'MiniHipatternsTodo'  },
    note  = { pattern = '%f[%w]()NOTE()%f[%W]',  group = 'MiniHipatternsNote'  },

    -- 16진수 색상 문자열(`#rrggbb`)을 해당 색상으로 하이라이트
    hex_color = hipatterns.gen_highlighter.hex_color(),
  },
})
```

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

    | 브랜치 | 코드 스니펫                                                         |
    |--------|----------------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.hipatterns')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.hipatterns', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                        |
    |--------|-----------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.hipatterns', version = false },` |
    | Stable | `{ 'nvim-mini/mini.hipatterns', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                               |
    |--------|------------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.hipatterns'`                         |
    | Stable | `Plug 'nvim-mini/mini.hipatterns', { 'branch': 'stable' }` |

</details>

**중요**: 모든 일반 버퍼에서 하이라이트를 자동으로 활성화하려면 비어 있지 않은 `highlighters`와 함께 `require('mini.hipatterns').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 하이라이터 테이블 (자세한 내용은 |MiniHipatterns.config| 참조).
  -- 기본적으로는 아무것도 정의되어 있지 않습니다. 시각적 효과를 위해 수동으로 추가하세요.
  highlighters = {},

  -- 비동기 하이라이트 프로세스를 정의하는 지연 시간 (ms)
  delay = {
    -- 텍스트가 변경될 때마다 업데이트하기 전 대기 시간
    text_change = 200,

    -- 창 스크롤 후 업데이트하기 전 대기 시간
    scroll = 50,
  },

}
```

## 유사한 플러그인 {#similar-plugins}

- [folke/todo-comments.nvim](https://github.com/folke/todo-comments.nvim)
- [folke/paint.nvim](https://github.com/folke/paint.nvim)
- [NvChad/nvim-colorizer.lua](https://github.com/NvChad/nvim-colorizer.lua)
- [uga-rosa/ccc.nvim](https://github.com/uga-rosa/ccc.nvim)
