---
title: "mini.bracketed"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-bracketed_readme.png?raw=true" alt="mini.bracketed" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 대괄호를 사용하여 앞뒤로 이동

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-bracketed.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-bracketed)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-bracketed.mp4?raw=true)

## 기능 {#features}

- 특정 대상으로 이동하기 위해 설정 가능한 Lua 함수들을 제공합니다. 각 함수는 다음으로 커스터마이징할 수 있습니다:
    - 방향: "forward", "backward", "first" (첫 번째부터 순방향), "last" (마지막부터 역방향) 중 하나.
    - 이동 횟수.
    - 끝에 도달했을 때 순환(wrap) 여부 (마지막 항목에서 다음으로 넘어가면 첫 번째로 이동).
    - 기타 대상별 옵션들.

- 대괄호를 사용한 매핑을 제공합니다. 설정 가능한 대상 접미사(suffix)를 사용하여 생성되며, 선택적으로 비활성화할 수 있습니다.

    각 매핑은 |[count]|를 지원합니다. 매핑은 노멀 모드에서 생성되지만, 현재 버퍼 내에서 커서를 이동하는 대상의 경우 비주얼 모드와 연산자 대기(Operator-pending, 점 반복 포함) 모드도 지원합니다.

    하나의 대상에 대해 `소문자-접미사`와 `대문자-접미사`를 사용하여 다음과 같은 매핑이 생성됩니다:
    - `[` + `대문자-접미사` : 첫 번째로 이동.
    - `[` + `소문자-접미사` : 이전으로 이동.
    - `]` + `소문자-접미사` : 다음으로 이동.
    - `]` + `대문자-접미사` : 마지막으로 이동.

- 지원되는 대상 (자세한 내용은 해당 Lua 함수 도움말 참조):

    | 대상                                            | 매핑            | Lua 함수                 |
    |---------------------------------------------------|---------------------|------------------------------|
    | 버퍼 (Buffer)                                     | `[B` `[b` `]b` `]B` | [`MiniBracketed.buffer()`](../doc/mini-bracketed.qmd#minibracketed.buffer)     |
    | 주석 블록 (Comment block)                         | `[C` `[c` `]c` `]C` | [`MiniBracketed.comment()`](../doc/mini-bracketed.qmd#minibracketed.comment)    |
    | 충돌 마커 (Conflict marker)                       | `[X` `[x` `]x` `]X` | [`MiniBracketed.conflict()`](../doc/mini-bracketed.qmd#minibracketed.conflict)   |
    | 진단 (Diagnostic)                                 | `[D` `[d` `]d` `]D` | [`MiniBracketed.diagnostic()`](../doc/mini-bracketed.qmd#minibracketed.diagnostic) |
    | 디스크 상의 파일 (File)                           | `[F` `[f` `]f` `]F` | [`MiniBracketed.file()`](../doc/mini-bracketed.qmd#minibracketed.file)       |
    | 들여쓰기 변경 (Indent change)                     | `[I` `[i` `]i` `]I` | [`MiniBracketed.indent()`](../doc/mini-bracketed.qmd#minibracketed.indent)     |
    | 현재 버퍼 내 점프 목록 (Jump)                     | `[J` `[j` `]j` `]J` | [`MiniBracketed.jump()`](../doc/mini-bracketed.qmd#minibracketed.jump)       |
    | 위치 목록 내 위치 (Location)                      | `[L` `[l` `]l` `]L` | [`MiniBracketed.location()`](../doc/mini-bracketed.qmd#minibracketed.location)   |
    | 최근 파일 (Old files)                             | `[O` `[o` `]o` `]O` | [`MiniBracketed.oldfile()`](../doc/mini-bracketed.qmd#minibracketed.oldfile)    |
    | Quickfix 목록 항목 (Quickfix)                     | `[Q` `[q` `]q` `]Q` | [`MiniBracketed.quickfix()`](../doc/mini-bracketed.qmd#minibracketed.quickfix)   |
    | Tree-sitter 노드 및 부모 (Tree-sitter)            | `[T` `[t` `]t` `]T` | [`MiniBracketed.treesitter()`](../doc/mini-bracketed.qmd#minibracketed.treesitter) |
    | 선형 이력 내 실행 취소 상태 (Undo states)         | `[U` `[u` `]u` `]U` | [`MiniBracketed.undo()`](../doc/mini-bracketed.qmd#minibracketed.undo)       |
    | 현재 탭의 창 (Window)                             | `[W` `[w` `]w` `]W` | [`MiniBracketed.window()`](../doc/mini-bracketed.qmd#minibracketed.window)     |
    | 최신 붙여넣기 영역을 대체하는 복사 선택 영역 (Yank) | `[Y` `[y` `]y` `]Y` | [`MiniBracketed.yank()`](../doc/mini-bracketed.qmd#minibracketed.yank)       |

참고:

- `undo` 대상은 `u` 및 `<C-R>` 키를 리매핑하여 각각 실행 취소 및 다시 실행 후의 상태를 등록합니다. 기존 설정과 충돌하는 경우 `undo` 대상을 비활성화하거나 [`MiniBracketed.setup()`](../doc/mini-bracketed.qmd#minibracketed.setup) 호출 후에 리매핑을 수행하세요. `undo` 대상을 직접 사용하려면 실행 취소/다시 실행 키가 동작 후 [`MiniBracketed.register_undo_state()`](../doc/mini-bracketed.qmd#minibracketed.register_undo_state)를 호출하도록 리매핑해야 합니다.

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

    | 브랜치 | 코드 스니펫                                                        |
    |--------|---------------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.bracketed')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.bracketed', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                       |
    |--------|----------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.bracketed', version = false },` |
    | Stable | `{ 'nvim-mini/mini.bracketed', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                              |
    |--------|-----------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.bracketed'`                         |
    | Stable | `Plug 'nvim-mini/mini.bracketed', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.bracketed').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 최상위 요소는 대상의 동작을 설명하는 테이블입니다:
  --
  -- - <suffix> - 단일 문자 접미사. 매핑에서 `[` / `]` 뒤에 사용됩니다.
  --   예를 들어, `b`인 경우 `[B`, `[b`, `]b`, `]B` 매핑을 생성합니다.
  --   매핑을 생성하지 않으려면 빈 문자열 `''`을 입력하세요.
  --
  -- - <options> - 대상 옵션을 덮어쓰는 테이블입니다.
  --
  -- 자세한 내용은 [`:h MiniBracketed.config`](../doc/mini-bracketed.qmd#minibracketed.config)를 참조하세요.

  buffer     = { suffix = 'b', options = {} },
  comment    = { suffix = 'c', options = {} },
  conflict   = { suffix = 'x', options = {} },
  diagnostic = { suffix = 'd', options = {} },
  file       = { suffix = 'f', options = {} },
  indent     = { suffix = 'i', options = {} },
  jump       = { suffix = 'j', options = {} },
  location   = { suffix = 'l', options = {} },
  oldfile    = { suffix = 'o', options = {} },
  quickfix   = { suffix = 'q', options = {} },
  treesitter = { suffix = 't', options = {} },
  undo       = { suffix = 'u', options = {} },
  window     = { suffix = 'w', options = {} },
  yank       = { suffix = 'y', options = {} },
}
```

## 유사한 플러그인 {#similar-plugins}

- [tpope/vim-unimpaired](https://github.com/tpope/vim-unimpaired)
