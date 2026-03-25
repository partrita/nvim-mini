---
title: "mini.comment"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-comment_readme.png?raw=true" alt="mini.comment" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 줄 주석 처리

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-comment.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-comment)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-comment.mp4?raw=true)

## 기능 {#features}

- 노멀 모드에서의 주석 처리는 `v:count`를 준수하며 점 반복(dot-repeat)이 가능합니다.
- 주석 구조는 'commentstring'에서 유추됩니다: 현재 버퍼 또는 로컬로 활성화된 tree-sitter 언어에서 가져옵니다. `options.custom_commentstring`을 통해 커스터마이징할 수 있습니다.
- 탭과 공백 들여쓰기를 모두 처리합니다 (단, 혼용된 경우는 제외).
- 주석 처리 전후에 사용자 정의 훅(hooks)을 실행할 수 있습니다.
- 세밀한 동작 조정을 위한 설정 옵션을 제공합니다.

참고:

- Tree-sitter를 인식하는 주석 처리를 사용하려면 'commentstring'의 전역 값이 `''`(빈 문자열)이어야 합니다. 이것이 기본값이므로, 수동으로 다른 값을 설정하지 않도록 주의하세요.

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

    | 브랜치 | 코드 스니펫                                                      |
    |--------|-------------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.comment')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.comment', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.comment', version = false },` |
    | Stable | `{ 'nvim-mini/mini.comment', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.comment'`                         |
    | Stable | `Plug 'nvim-mini/mini.comment', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.comment').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 모듈 동작을 제어하는 옵션
  options = {
    -- 커스텀 'commentstring'을 계산하는 함수 (선택 사항)
    custom_commentstring = nil,

    -- 주석 처리 시 빈 줄을 무시할지 여부
    ignore_blank_line = false,

    -- 동작 및 텍스트 오브젝트에서 줄 시작 부분을 무시할지 여부
    start_of_line = false,

    -- 주석 부분에 단일 공백 내부 패딩을 강제할지 여부
    pad_comment_parts = true,
  },

  -- 모듈 매핑. 비활성화하려면 `''`(빈 문자열)을 사용하세요.
  mappings = {
    -- 주석 토글 (예: `gcip` - 단락 내 주석 처리).
    -- 노멀 및 비주얼 모드 모두에 적용됩니다.
    comment = 'gc',

    -- 현재 줄 주석 토글
    comment_line = 'gcc',

    -- 비주얼 선택 영역 주석 토글
    comment_visual = 'gc',

    -- '주석(comment)' 텍스트 오브젝트 정의 (예: `dgc` - 전체 주석 블록 삭제).
    -- 매핑이 `comment_visual`과 다를 경우 비주얼 모드에서도 작동합니다.
    textobject = 'gc',
  },

  -- 특정 주석 처리 단계에서 실행될 훅(hook) 함수
  hooks = {
    -- 주석 처리 성공 전. 기본적으로 아무 작업도 하지 않습니다.
    pre = function() end,
    -- 주석 처리 성공 후. 기본적으로 아무 작업도 하지 않습니다.
    post = function() end,
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- Neovim>=0.10의 내장 주석 처리 기능, `:h commenting` 참조 ('mini.comment'를 참고하여 구현됨)
- [numToStr/Comment.nvim](https://github.com/numToStr/Comment.nvim)
- [tpope/vim-commentary](https://github.com/tpope/vim-commentary)
- [preservim/nerdcommenter](https://github.com/preservim/nerdcommenter)
- [b3nj5m1n/kommentary](https://github.com/b3nj5m1n/kommentary)
