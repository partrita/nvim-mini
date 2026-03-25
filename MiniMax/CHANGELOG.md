---
title: "MiniMax 변경 이력"
---

_'MiniMax'의 `main` 브랜치에서 생성됨_

## 2026-02-17 {#2026-02-17}

- 'mini.files' 설정을 `later` 대신 `now_if_args`를 사용하도록 업데이트했습니다. 그렇지 않으면 `nvim .`과 같이 Neovim을 시작할 때 `netrw`를 기본 탐색기로 덮어쓰지 못하는 문제가 있었습니다.

## 2026-02-15 {#2026-02-15}

- 'nvim-treesitter/nvim-treesitter-textobjects' 플러그인이 이제 `main` 브랜치를 기본값으로 사용하므로, 명시적인 브랜치 지정을 제거했습니다.

- 새로운 참조 설정을 추가했습니다:
    - `nvim-0.10` - Neovim>=0.10용
    - `nvim-0.12` - Neovim>=0.12용

## 2026-02-10 {#2026-02-10}

- 설정용 전역 변수를 `_G.Config` 대신 단순히 `Config`로 사용하도록 업데이트했습니다. 이는 더 간결하며 `MiniXxx` 변수들이 사용되는 방식과 더 일관성이 있습니다.

## 2026-01-29 {#2026-01-29}

- 'mini.completion' 설정을 `later` 대신 `now_if_args`를 사용하도록 업데이트했습니다. 그렇지 않으면 시작 시에 열린 파일들에 대해 적절한 omnifunc가 설정되지 않는 문제(`LspAttach` 이벤트가 이미 발생했기 때문)가 있었습니다.

- `now_if_args`가 필요한 'mini.nvim' 모듈들의 설정을 별도의 "Step one or two" 섹션으로 이동했습니다.

## 2026-01-13 {#2026-01-13}

- 'stevearc/conform.nvim' 설정을 개선했습니다:
    - 전용 포맷터가 없는 경우 LSP 서버의 포맷팅을 허용하도록 설정했습니다. 이는 더 유연한 동작을 제공합니다. 기존에는 `<Leader>lf` 매핑에서 강제되었습니다.
    - `<Leader>lf` 키맵에서 일반적인 `require('conform').format()`을 사용하도록 변경했습니다.

## 2026-01-08 {#2026-01-08}

- quickfix 리스트 탐색 키맵을 개선하고(구현을 더 짧고 견고하게 만듦), location 리스트 탐색용으로 `<Leader>eq`에 대응하는 `<Leader>eQ`를 추가했습니다.

## 2026-01-03 {#2026-01-03}

- 'mini.clue' 설정을 개선했습니다:
    - 더 간결한 설정을 위해 가능한 경우 배열 형태의 `mode`를 사용합니다.
    - 더 많은 내장 힌트를 보여주기 위해 `gen_clues.square_brackets()`를 사용합니다.
    - `s`를 트리거로 사용합니다. 현재는 'mini.surround' 액션에만 사용되지만, 향후 더 유용하게 쓰일 것입니다.

## 2025-12-20 {#2025-12-20}

- 'mini.cmdline'을 사용하기 시작했습니다.

## 2025-12-16 {#2025-12-16}

- 'nvim-treesitter/nvim-treesitter' 플러그인이 이제 `main` 브랜치를 기본값으로 사용하므로, 명시적인 브랜치 지정을 제거했습니다.

- 'mason-org/mason.nvim' 예제에서 `later` 대신 `now_if_args`를 사용하도록 업데이트했습니다. 그렇지 않으면 `nvim -- path/to/file`과 같이 Neovim을 시작할 때 Mason을 통해 설치된 LSP 서버를 즉시 사용할 수 없는 문제가 있었습니다.

## 2025-11-22 {#2025-11-22}

- `<Leader>fs` 매핑이 `:Pick lsp`에서 `"workspace_symbol"` 대신 `"workspace_symbol_live"` 범위를 사용하도록 업데이트했습니다.

## 2025-10-16 {#2025-10-16}

- `now_if_args` 시작 도우미를 다른 설정 파일에서 직접 사용할 수 있도록 `Config.now_if_args`로 'init.lua'에 이동했습니다.

- 'mini.misc'를 `now` 대신 `now_if_args`에서 활성화하도록 변경했습니다. 그렇지 않으면 `nvim -- path/to/file`과 같이 Neovim을 시작할 때 `setup_auto_root()` 및 `setup_restore_cursor()`가 초기 파일에서 작동하지 않는 문제가 있었습니다.

## 2025-10-13 {#2025-10-13}

- 최초 릴리스.
