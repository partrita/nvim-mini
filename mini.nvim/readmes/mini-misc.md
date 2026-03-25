---
title: "mini.misc"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-misc_readme.png?raw=true" alt="mini.misc" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 유용한 기타 기능들

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-misc.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-misc)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-misc.mp4?raw=true)

## 기능 {#features}

- `bench_time()`은 함수를 여러 번 실행하여 걸린 시간을 측정합니다.
- `log_add()` / `log_show()` 및 기타 헬퍼 함수들은 특수한 인메모리 로그 배열을 작업하는 데 사용됩니다. Lua 코드를 디버깅할 때 `print()` 대신 유용하게 사용할 수 있습니다.
- `put()`과 `put_text()`는 각각 커맨드 라인과 현재 버퍼에 Lua 객체를 출력합니다.
- `resize_window()`는 현재 창을 편집 가능한 너비로 조정합니다.
- `safely()`는 특정 조건에서 함수를 실행하고 에러 발생 시 경고를 표시합니다. 'init.lua'를 간단한 지연 로딩(lazy loading)과 함께 안전하게 구성하는 데 유용합니다.
- `setup_auto_root()`는 현재 디렉터리를 자동으로 변경하도록 설정합니다.
- `setup_termbg_sync()`는 터미널 배경 동기화를 설정합니다 (현재 Neovim 인스턴스 주변에 생길 수 있는 "프레임"을 제거).
- `setup_restore_cursor()`는 파일을 다시 열 때 커서 위치를 자동으로 복원하도록 설정합니다.
- `stat_summary()`는 숫자 배열의 요약 통계를 계산합니다.
- `tbl_head()`와 `tbl_tail()`은 테이블의 첫 번째와 마지막 요소를 반환합니다.
- `zoom()`은 현재 버퍼를 플로팅 창을 통해 전체 화면으로 확대합니다.
- 그 외 다양한 기능을 제공합니다.

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
    | Main   | `add('nvim-mini/mini.misc')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.misc', checkout = 'stable' })` |

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
    | Main   | `{ 'nvim-mini/mini.misc', version = false },` |
    | Stable | `{ 'nvim-mini/mini.misc', version = '*' },`   |

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
    | Main   | `Plug 'nvim-mini/mini.misc'`                         |
    | Stable | `Plug 'nvim-mini/mini.misc', { 'branch': 'stable' }` |

</details>

**중요**: `require('mini.misc').setup()`을 반드시 호출할 필요는 없으나, 사용 편의성을 높이기 위해 호출할 수 있습니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 전역 변수로 만들 필드들의 배열 (독립적인 변수로 사용됨)
  make_global = { 'put', 'put_text' },
}
```

## 유사한 플러그인 {#similar-plugins}

- [nvim-lua/plenary.nvim](https://github.com/nvim-lua/plenary.nvim)
