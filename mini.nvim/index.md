---
title: "mini.nvim"
---

<p align="center"> <img src="logo.png" alt="mini.nvim" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 올인원 플러그인

최소한의 노력으로 [Neovim](https://github.com/neovim/neovim) (버전 0.9 이상) 환경을 개선하는 40개 이상의 독립적인 Lua 모듈 모음입니다. 모든 모듈은 동일한 설정 방식과 일반적인 설계 원칙을 공유합니다.

이 프로젝트를 Neovim 플러그인 중의 "맥가이버 칼"이라고 생각하세요: 가장 일반적인 작업에 적합한 다양하고 독립적인 도구(모듈)를 가지고 있습니다. 각 모듈은 시작 및 사용 오버헤드 없이 별도로 사용할 수 있습니다.

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면:

- 'mini.nvim' 및/또는 다른 [MINI 프로젝트](https://nvim-mini.org)에 Github 스타를 남겨주세요.
- [기여 가이드](CONTRIBUTING.md)를 확인하세요.

현재 개발 버전을 포함한 변경 이력은 [변경 이력](CHANGELOG.md)을 참조하세요.

'mini.nvim' 기반의 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

::: {.callout-note}
이 프로젝트는 이전에 `echasnovski/mini.nvim`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

## 목차

- [설치](#installation)
- [모듈](#modules)
- [일반 원칙](#general-principles)
- [플러그인 컬러 스킴](#plugin-color-schemes)
- [계획된 모듈](#planned-modules)

## 설치 {#installation}

두 가지 브랜치 중 하나를 골라 설치할 수 있습니다:

- `main` (기본값, **권장**): 플러그인의 최신 개발 버전입니다. 마지막 안정 릴리스 이후의 모든 변경 사항은 베타 테스트 단계(알파 테스트를 통과하고 어느 정도 안정됨을 의미)로 간주되어야 합니다.
- `stable`: `main` 브랜치에서 공개 베타 테스트를 거친 코드가 포함된 릴리스 시에만 업데이트됩니다.

다음은 몇 가지 일반적인 설치 방법의 코드 스니펫입니다:

- `git clone`을 사용한 수동 설치 ([mini.deps](https://nvim-mini.org/mini.nvim/readmes/mini-deps)와 호환됨):

```lua
-- 'init.lua' 상단에 배치하세요
local path_package = vim.fn.stdpath('data') .. '/site'
local mini_path = path_package .. '/pack/deps/start/mini.nvim'
if not vim.loop.fs_stat(mini_path) then
  vim.cmd('echo "Installing `mini.nvim`" | redraw')
  local clone_cmd = {
    'git', 'clone', '--filter=blob:none',
    -- 'stable' 브랜치를 사용하려면 다음 줄의 주석을 해제하세요
    -- '--branch', 'stable',
    'https://github.com/nvim-mini/mini.nvim', mini_path
  }
  vim.fn.system(clone_cmd)
  vim.cmd('packadd mini.nvim | helptags ALL')
  vim.cmd('echo "Installed `mini.nvim`" | redraw')
end
```

- [folke/lazy.nvim](https://github.com/folke/lazy.nvim) 사용 시:

| 브랜치 | 코드 스니펫                                  |
|--------|-----------------------------------------------|
| Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
| Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- [junegunn/vim-plug](https://github.com/junegunn/vim-plug) 사용 시:

| 브랜치 | 코드 스니펫                                         |
|--------|------------------------------------------------------|
| Main   | `Plug 'nvim-mini/mini.nvim'`                         |
| Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 모든 모듈은 독립적인 Git 저장소로도 배포됩니다. 자세한 내용은 각 모듈의 정보를 확인하세요.

**중요**: 기능을 활성화하려면 모듈의 `setup()`을 호출해야 합니다 (필요한 경우).

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 모듈 {#modules}

'mini.nvim'은 많은 모듈을 포함하고 있어 처음에는 조금 당황스러울 수 있습니다. 모든 모듈은 필요할 때마다 하나씩 독립적으로 사용할 수 있습니다.

더 쉬운 탐색을 위해, 여기서는 모듈의 주요 기능을 기반으로 그룹화하여 제시합니다 (일부 모듈은 여러 그룹에 속할 수 있습니다). 더 자세한 목록은 [여기](doc/mini-nvim.qmd)를 참조하세요.

### 텍스트 편집

이 모듈들은 텍스트 편집 경험을 개선합니다. 'mini.ai', 'mini.operators', 'mini.surround'부터 시작해 보세요.

| 모듈             | 설명                                  | 개요                               | 상세 문서                                  |
|-----------------|---------------------------------------|--------------------------------------|------------------------------------------|
| mini.ai         | `a`/`i` 텍스트 오브젝트 확장 및 생성 | [README](readmes/mini-ai.md)         | [문서](doc/mini-ai.qmd)         |
| mini.align      | 대화형으로 텍스트 정렬                | [README](readmes/mini-align.md)      | [문서](doc/mini-align.qmd)      |
| mini.bracketed  | `[` / `]`를 사용한 다음/이전 이동     | [README](readmes/mini-bracketed.md)  | [문서](doc/mini-bracketed.md)  |
| mini.comment    | 주석 처리                             | [README](readmes/mini-comment.md)    | [문서](doc/mini-comment.qmd)    |
| mini.move       | 선택 영역 이동                        | [README](readmes/mini-move.md)       | [문서](doc/mini-move.qmd)       |
| mini.operators  | 텍스트 조작 연산자                    | [README](readmes/mini-operators.md)  | [문서](doc/mini-operators.qmd)  |
| mini.pairs      | 자동 쌍(autopairs)                    | [README](readmes/mini-pairs.md)      | [문서](doc/mini-pairs.qmd)      |
| mini.splitjoin  | 단일/다중 라인 인접 변환              | [README](readmes/mini-splitjoin.md)  | [문서](doc/mini-splitjoin.qmd)  |
| mini.surround   | 주변 텍스트 감싸기/삭제/변경          | [README](readmes/mini-surround.md)   | [문서](doc/mini-surround.qmd)   |

### 일반적인 UI

이 모듈들은 Neovim의 일반적인 UI 요소를 개선합니다.

| 모듈             | 설명                                  | 개요                               | 상세 문서                                  |
|-----------------|---------------------------------------|--------------------------------------|------------------------------------------|
| mini.basics     | 일반적인 Neovim 기본 설정             | [README](readmes/mini-basics.md)     | [문서](doc/mini-basics.qmd)     |
| mini.clue       | 매핑 힌트 표시                        | [README](readmes/mini-clue.md)       | [문서](doc/mini-clue.qmd)       |
| mini.cursorword | 커서 아래 단어 강조                   | [README](readmes/mini-cursorword.md) | [문서](doc/mini-cursorword.qmd) |
| mini.extra      | 추가 기능 모음                        | [README](readmes/mini-extra.md)      | [문서](doc/mini-extra.qmd)      |
| mini.hipatterns | 텍스트 하이라이트 패턴                | [README](readmes/mini-hipatterns.md) | [문서](doc/mini-hipatterns.qmd) |
| mini.indentscope| 인덴트 범위 시각화                    | [README](readmes/mini-indentscope.md)| [문서](doc/mini-indentscope.qmd)|
| mini.map        | 코드 미니맵                           | [README](readmes/mini-map.md)        | [문서](doc/mini-map.qmd)        |
| mini.notify     | 알림 관리                             | [README](readmes/mini-notify.md)     | [문서](doc/mini-notify.qmd)     |
| mini.statusline | 상태표시줄(statusline)                | [README](readmes/mini-statusline.md) | [문서](doc/mini-statusline.qmd) |
| mini.tabline    | 탭표시줄(tabline)                      | [README](readmes/mini-tabline.md)    | [문서](doc/mini-tabline.qmd)    |
| mini.trailspace | 후행 공백 시각화 및 제거              | [README](readmes/mini-trailspace.md) | [문서](doc/mini-trailspace.qmd) |

### 워크플로우

이 모듈들은 작업을 더 효율적으로 만들어 줍니다.

| 모듈             | 설명                                  | 개요                               | 상세 문서                                  |
|-----------------|---------------------------------------|--------------------------------------|------------------------------------------|
| mini.bufremove  | 버퍼 삭제 (레이아웃 유지)             | [README](readmes/mini-bufremove.md)  | [문서](doc/mini-bufremove.qmd)  |
| mini.completion | 자동 완성 및 시그니처 헬프            | [README](readmes/mini-completion.md) | [문서](doc/mini-completion.qmd) |
| mini.deps       | 플러그인 매니저                       | [README](readmes/mini-deps.md)       | [문서](doc/mini-deps.qmd)       |
| mini.diff       | Diff 표시 및 관리                     | [README](readmes/mini-diff.md)       | [문서](doc/mini-diff.qmd)       |
| mini.files      | 파일 탐색기                           | [README](readmes/mini-files.md)      | [문서](doc/mini-files.qmd)      |
| mini.fuzzy      | 퍼지 매칭                             | [README](readmes/mini-fuzzy.md)      | [문서](doc/mini-fuzzy.qmd)      |
| mini.git        | Git 통합                              | [README](readmes/mini-git.md)        | [문서](doc/mini-git.qmd)        |
| mini.icons      | 아이콘 제공                           | [README](readmes/mini-icons.md)      | [문서](doc/mini-icons.qmd)      |
| mini.jump       | 텍스트 내 빠른 이동                   | [README](readmes/mini-jump.md)       | [문서](doc/mini-jump.qmd)       |
| mini.jump2d     | 2D 영역 내 빠른 점프                  | [README](readmes/mini-jump2d.md)     | [문서](doc/mini-jump2d.qmd)     |
| mini.misc       | 잡다한 유틸리티                       | [README](readmes/mini-misc.md)       | [문서](doc/mini-misc.qmd)       |
| mini.pick       | 피커(Picker)                          | [README](readmes/mini-pick.md)       | [문서](doc/mini-pick.qmd)       |
| mini.sessions   | 세션 관리                             | [README](readmes/mini-sessions.md)   | [문서](doc/mini-sessions.qmd)   |
| mini.snippets   | 스니펫 관리                           | [README](readmes/mini-snippets.md)   | [문서](doc/mini-snippets.qmd)   |
| mini.visits     | 파일 방문 기록 및 추적                | [README](readmes/mini-visits.md)     | [문서](doc/mini-visits.qmd)     |

### 외관 및 테마

이 모듈들은 Neovim의 외관을 개선합니다.

| 모듈             | 설명                                  | 개요                               | 상세 문서                                  |
|-----------------|---------------------------------------|--------------------------------------|------------------------------------------|
| mini.animate    | 애니메이션 효과                       | [README](readmes/mini-animate.md)    | [문서](doc/mini-animate.qmd)    |
| mini.base16     | Base16 테마 생성                      | [README](readmes/mini-base16.md)     | [문서](doc/mini-base16.qmd)     |
| mini.colors     | 색상 팔레트 관리                      | [README](readmes/mini-colors.md)     | [문서](doc/mini-colors.qmd)     |
| mini.hues       | 임의의 색상 기반 컬러 스킴            | [README](readmes/mini-hues.md)       | [문서](doc/mini-hues.qmd)       |

### 개발 도구

이 모듈들은 플러그인 개발자나 파워 유저를 위한 도구입니다.

| 모듈             | 설명                                  | 개요                               | 상세 문서                                  |
|-----------------|---------------------------------------|--------------------------------------|------------------------------------------|
| mini.doc        | Neovim 도움말 파일 생성               | [README](readmes/mini-doc.md)        | [문서](doc/mini-doc.qmd)        |
| mini.test       | 플러그인 테스트 프레임워크            | [README](readmes/mini-test.md)       | [문서](doc/mini-test.qmd)       |

## 일반 원칙 {#general-principles}

- **독립성**: 각 모듈은 별도의 하위 플러그인처럼 작동하며 독립적으로 사용할 수 있습니다.
- **최소주의**: 꼭 필요한 기능만을 포함하여 가볍고 빠르게 유지합니다.
- **일관성**: 유사한 설정 방식과 설계 철학을 따릅니다.

상세한 내용은 [공통 원칙 문서](doc/mini-nvim.qmd#general-principles)를 참조하세요.

## 플러그인 컬러 스킴 {#plugin-color-schemes}

일부 모듈은 컬러 스킴에 따라 다르게 보일 수 있습니다. 'mini.nvim'은 다음과 같은 전용 컬러 스킴을 제공합니다:

- **minisummer**: 밝고 활기찬 테마.
- **miniwinter**: 차분하고 가독성 좋은 어두운 테마.

[상세 문서](doc/mini-colors.qmd)에서 이 테마들을 어떻게 사용하고 커스터마이징하는지 확인하세요.

## 계획된 모듈 {#planned-modules}

미래에 추가될 수 있는 모듈 목록입니다. 아이디어나 제안은 언제나 환영합니다!
- `mini.tabs`: 탭 페이지 관리를 위한 더 나은 UI.
- `mini.project`: 지능적인 프로젝트 루트 감지 및 전환.

---

© Evgeni Chasnovski, [MIT](https://choosealicense.com/licenses/mit/)
