_'mini.nvim'의 `main` 브랜치에서 생성됨_

과거 및 현재 개발 버전의 변경 이력입니다. 모듈별(또는 전체 모듈) 및 유형별 사용자 관련 기능을 나열합니다.

다음과 같은 변경 유형이 있습니다:

- `Evolve` - 새로운 기능을 추가하면서 기존 기능을 변경합니다.
- `Refine` - 새로운 기능 추가 없이 기존 기능을 변경합니다. 이는 보통 "중대한 변경(breaking change)"으로 설명되지만, 여기서는 기존 기능에 대한 사용자의 기대를 바꿀 수 있다는 의미로 사용됩니다.
- `Expand` - 기존 기능에 영향을 주지 않고 새로운 기능을 추가합니다. 본질적으로 새로운 기능입니다.

# 버전 0.18.0-dev {#v0.18.0}

## mini.base16 {#v0.18.0-mini.base16}

### Expand {#v0.18.0-mini.base16-expand}

- 새로운 플러그인 통합 추가:
    - 'folke/snacks.nvim'

## mini.clue {#v0.18.0-mini.clue}

### Expand {#v0.18.0-mini.clue-expand}

- `vim.keymap.set`의 `modes` 파라미터와의 일관성을 위해 힌트와 트리거에 모드 배열을 허용합니다. (By @pkazmier, PR #2202)

## mini.extra {#v0.18.0-mini.extra}

### Expand {#v0.18.0-mini.extra-expand}

- `pickers.manpages` 피커를 추가했습니다.

## mini.hues {#v0.18.0-mini.hues}

### Expand {#v0.18.0-mini.hues-expand}

- 새로운 플러그인 통합 추가:
    - 'folke/snacks.nvim'

## mini.jump {#v0.18.0-mini.jump}

### Evolve {#v0.18.0-mini.jump-evolve}

- dot-repeat가 순수 Neovim에서와 같이 동작하도록 하여 일반적인 점프를 덜 방해하도록 개선했습니다. 이는 `dte` -> `fx` -> `.`를 실행했을 때 `dfx`가 아닌 `dte`가 다시 수행되도록 합니다. (By @abeldekat, PR #2284)

## mini.misc {#v0.18.0-mini.misc}

### Evolve {#v0.18.0-mini.misc-evolve}

- `setup_termbg_sync()`가 터미널 에뮬레이터의 배경색을 리셋하기 위해 OSC 111 제어 시퀀스를 사용하도록 업데이트했습니다. 이는 플랫폼(예: `tmux`) 간에 더 견고한 동작을 제공합니다.
    기존의 "초기 배경색을 명시적으로 설정하여 리셋"하는 동작은 새로운 `opts.explicit_reset` 옵션을 `true`로 설정하여 사용할 수 있습니다.

### Expand {#v0.18.0-mini.misc-expand}

- 함수를 실행하고 발생 가능한 에러를 경고로 보고하는 `safely()`를 추가했습니다. 특정 조건(이벤트, 지연 등)까지 실행을 연기할 수도 있습니다.
    이는 향후 `MiniDeps.now()`와 `MiniDeps.later()`를 대체할 예정입니다.

## mini.pairs {#v0.18.0-mini.pairs}

### Refine {#v0.18.0-mini.pairs-refine}

- 기본 매핑의 주변 패턴이 멀티바이트 문자와 더 잘 작동하도록 업데이트했습니다. 의미는 동일하며 형식이 더 유연하게 조정되었습니다.

## mini.pick {#v0.18.0-mini.pick}

### Expand {#v0.18.0-mini.pick-expand}

- `source.preview`가 피커의 메인 창에 다른 버퍼를 직접 설정할 수 있도록 허용합니다. 여전히 제공된 `buf_id` 버퍼를 조정하는 것이 권장되지만, 이것이 불가능할 경우를 위한 워크아웃이 마련되었습니다.

### Refine {#v0.18.0-mini.pick-refine}

- 피커가 활성 상태일 때 `config.delay.async` 밀리초마다 강제로 화면을 다시 그리는 것을 중단했습니다. 이는 불필요한 CPU 사용량과 코드/테스트 복잡성을 가중시켰습니다.
    이로 인해 비동기 하이라이트(예: `vim.treesitter.start()` 이후)가 있는 프리뷰는 추가적인 처리가 필요할 수 있습니다. 이미 내장된 몇 가지 명시적 `:redraw`가 있지만, 충분하지 않다면 필요한 곳에서 직접 redraw를 실행해 주세요.

## mini.surround {#v0.18.0-mini.surround}

### Expand {#v0.18.0-mini.surround-expand}

- `find` 및 `find_left` 액션을 위한 Visual 모드 및 Operator-pending 모드 매핑을 추가했습니다.

## mini.test {#v0.18.0-mini.test}

### Refine {#v0.18.0-mini.test-refine}

- `expect.error` 및 `expect.no_error`가 테스트할 함수를 위한 추가 인자를 받지 않도록 업데이트했습니다. 다음 'mini.nvim' 릴리스 전까지는 작동하겠지만 그 이후에는 작동하지 않을 예정입니다.
    익명 함수를 사용하여 명시적으로 인자를 전달하세요: `expect.error(f, "", 1, 2)` -> `expect.error(function() f(1, 2) end, "")`

- 모든 내장 리포터(`gen_reporter.buffer`, `gen_reporter.stdout`)가 모든 실패(fails)를 먼저 보여주고 그 다음에 모든 노트(notes)를 보여주도록 업데이트했습니다. 이는 노트가 많을 때 실패한 케이스를 더 쉽게 찾을 수 있게 해줍니다.

### Expand {#v0.18.0-mini.test-expand}

- 모든 `MiniTest.expect` 기대치가 기본 "Failed expectation for ..." 대신 실패 원인을 커스터마이징할 수 있도록 업데이트했습니다. 또한 마지막 인자로 `opts`를 일관되게 도입했습니다.

- `MiniTest.expect.equality`가 실패한 동등성 비교의 상세 원인을 보여주도록 업데이트했습니다. 두 문자열에서 어느 문자가 다른지, 또는 두 테이블에서 어느 키의 값이 다른지 등을 보여줍니다.

---
(이하 생략 - 과거 버전의 변경 이력은 [기존 CHANGELOG.md](https://github.com/nvim-mini/mini.nvim/blob/main/CHANGELOG.md)를 참조하세요)
