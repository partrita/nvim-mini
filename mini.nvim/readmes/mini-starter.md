---
title: "mini.starter"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-starter_readme.png?raw=true" alt="mini.starter" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 빠르고 유연한 시작 화면

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-starter.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-starter)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-starter.mp4?raw=true)

## 기능 {#features}

- 모든 사용 가능한 액션은 항목(items) 내부에 정의됩니다. [`MiniStarter.sections`](../doc/mini-starter.qmd#ministarter.sections)에 사전 설정된 전체 섹션들이 준비되어 있습니다.
- 항목 배열을 제공하여 표시될 항목들을 설정할 수 있으며, 이는 내부적으로 항목 배열로 정규화됩니다. 제공된 항목이 정규화되는 방식은 [`MiniStarter.refresh()`](../doc/mini-starter.qmd#ministarter.refresh)를 참조하세요.
- 콘텐츠 후크(content hooks)를 제공하여 최종 외관을 수정할 수 있습니다. [`MiniStarter.gen_hook`](../doc/mini-starter.qmd#ministarter.gen_hook)에 사전 설정된 콘텐츠 후크 생성기들이 있습니다.
- 항목 선택은 두 가지 방식으로 가능합니다:
    - 접두사 쿼리를 입력하여 항목 이름과 매칭(대소문자 무시)해 필터링합니다. 표시되는 정보는 문자를 입력할 때마다 업데이트됩니다. 각 항목의 고유한 접두사는 하이라이트되어 표시됩니다.
    - 위/아래 화살표(또는 `<C-n>`/`<C-p>`, `<M-j>`/`<M-k>`)를 사용하여 이동한 뒤 Enter를 누릅니다.
- 여러 개의 Starter 버퍼를 동시에 열 수 있습니다.

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
    | Main   | `add('nvim-mini/mini.starter')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.starter', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.starter', version = false },` |
    | Stable | `{ 'nvim-mini/mini.starter', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.starter'`                         |
    | Stable | `Plug 'nvim-mini/mini.starter', { 'branch': 'stable' }` |

</details>

**중요**: 기능을 활성화하려면 `require('mini.starter').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- VimEnter 이벤트 시 Starter 버퍼를 열지 여부. Neovim이 
  -- 다른 것을 보여주려는 의도로 시작된 경우에는 열리지 않습니다.
  autoopen = true,

  -- 활성화된 항목이 단 하나일 때 해당 액션을 실행할지 여부
  evaluate_single = false,

  -- 표시될 항목들. 다음 요소들을 포함하는 배열이어야 합니다:
  -- - Item: <action>, <name>, <section> 키를 가진 테이블.
  -- - Function: 위 세 가지 카테고리 중 하나를 반환해야 함.
  -- - Array: 위 세 가지 타입(item, array, function)의 요소들.
  -- `nil`(기본값)인 경우 기본 항목들이 사용됩니다 (|mini.starter| 참조).
  items = nil,

  -- 항목들 앞에 표시될 헤더. `tostring`을 통해 단일 문자열로 변환됩니다 
  -- (여러 줄을 표시하려면 `\n` 사용). 함수인 경우 먼저 평가됩니다. 
  -- `nil`(기본값)인 경우 정중한 인사말이 사용됩니다.
  header = nil,

  -- 항목들 뒤에 표시될 푸터. `tostring`을 통해 단일 문자열로 변환됩니다 
  -- (여러 줄을 표시하려면 `\n` 사용). 함수인 경우 먼저 평가됩니다. 
  -- `nil`(기본값)인 경우 기본 사용법 도움말이 표시됩니다.
  footer = nil,

  -- 초기 콘텐츠에 순차적으로 적용될 함수들의 배열.
  -- 각 함수는 'Starter' 버퍼용 콘텐츠를 인자로 받아 반환해야 합니다 
  -- (|mini.starter| 및 |MiniStarter.content| 참조).
  content_hooks = nil,

  -- 쿼리를 업데이트할 문자들. 각 문자는 전역 매핑을 덮어쓰는 
  -- 특별한 버퍼 매핑을 갖게 됩니다. `:`를 추가하면 커맨드 모드로 
  -- 진입할 수 있게 되므로 주의하세요.
  query_updaters = 'abcdefghijklmnopqrstuvwxyz0123456789_-.',

  -- 에러가 아닌 피드백 표시를 비활성화할지 여부
  silent = false,
}
```

## 유사한 플러그인 {#similar-plugins}

- [mhinz/vim-startify](https://github.com/mhinz/vim-startify)
- [glepnir/dashboard-nvim](https://github.com/glepnir/dashboard-nvim)
- [goolord/alpha-nvim](https://github.com/goolord/alpha-nvim)
