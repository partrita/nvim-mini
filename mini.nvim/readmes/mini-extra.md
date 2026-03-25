---
title: "mini.extra"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-extra_readme.png?raw=true" alt="mini.extra" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 'mini.nvim'의 추가 기능들

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-extra.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-extra)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-extra.mp4?raw=true)

## 기능 {#features}

다른 'mini.nvim' 모듈에 직접 포함시키기에는 필수적이지 않지만 유용한 추가 기능들을 제공합니다.

기능:

- ['mini.pick'](https://nvim-mini.org/mini.nvim/readmes/mini-pick)을 위한 다양한 피커(pickers):
    - 내장 진단 ([`MiniExtra.pickers.diagnostic()`](../doc/mini-extra.qmd#miniextra.pickers.diagnostic)).
    - 파일 탐색기 ([`MiniExtra.pickers.explorer()`](../doc/mini-extra.qmd#miniextra.pickers.explorer)).
    - Git 브랜치/커밋/파일/헝크 ([`MiniExtra.pickers.git_hunks()`](../doc/mini-extra.qmd#miniextra.pickers.git_hunks) 등).
    - 명령어/검색/입력 이력 ([`MiniExtra.pickers.history()`](../doc/mini-extra.qmd#miniextra.pickers.history)).
    - LSP 참조/심볼 등 ([`MiniExtra.pickers.lsp()`](../doc/mini-extra.qmd#miniextra.pickers.lsp)).
    - Tree-sitter 노드 ([`MiniExtra.pickers.treesitter()`](../doc/mini-extra.qmd#miniextra.pickers.treesitter)).
    - **이 외에도 훨씬 많습니다.**
  자세한 내용은 [`:h MiniExtra.pickers`](../doc/mini-extra.qmd#miniextra.pickers)를 참조하세요.

- ['mini.ai'](https://nvim-mini.org/mini.nvim/readmes/mini-ai)를 위한 다양한 텍스트 오브젝트 사양. [`:h MiniExtra.gen_ai_spec`](../doc/mini-extra.qmd#miniextra.gen_ai_spec)을 참조하세요.

- ['mini.hipatterns'](https://nvim-mini.org/mini.nvim/readmes/mini-hipatterns)를 위한 다양한 하이라이터(highlighters). [`:h MiniExtra.gen_highlighter`](../doc/mini-extra.qmd#miniextra.gen_highlighter)를 참조하세요.

참고:

- 이 모듈은 특정 기능에 필요한 'mini.nvim' 모듈만을 요구합니다: 피커에는 'mini.pick'이 하나만 필요하는 등.

더 자세한 정보는 도움말의 다음 부분을 참조하세요:

- [`:h MiniExtra.pickers`](../doc/mini-extra.qmd#miniextra.pickers)
- [`:h MiniExtra.gen_ai_spec`](../doc/mini-extra.qmd#miniextra.gen_ai_spec)
- [`:h MiniExtra.gen_highlighter`](../doc/mini-extra.qmd#miniextra.gen_highlighter)

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
    | Main   | `add('nvim-mini/mini.extra')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.extra', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.extra', version = false },` |
    | Stable | `{ 'nvim-mini/mini.extra', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.extra'`                         |
    | Stable | `Plug 'nvim-mini/mini.extra', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.extra').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{}
```

## 유사한 플러그인 {#similar-plugins}

- [nvim-telescope/telescope.nvim](https://github.com/nvim-telescope/telescope.nvim)
- [ibhagwan/fzf-lua](https://github.com/ibhagwan/fzf-lua)
