---
title: "MiniMax 설정"
---

_ 'MiniMax'의 `main` 브랜치에서 생성됨 _

## MiniMax 참조 설정

초기 설정 생성 중에 Neovim 버전에 따라 가장 적합한 설정이 선택됩니다.

사용 가능한 버전:

- [`nvim-0.10`](nvim-0.10) - Neovim>=0.10용
- [`nvim-0.11`](nvim-0.11) - Neovim>=0.11용
- [`nvim-0.12`](nvim-0.12) - Neovim>=0.12용 (현재 개발 중)

선택된 설정 간의 차이점:

- [`nvim-0.10`과 `nvim-0.11` 사이의 차이점](https://nvim-mini.org/MiniMax/configs/diffs/nvim-0.10_nvim-0.11)
- [`nvim-0.11`과 `nvim-0.12` 사이의 차이점](https://nvim-mini.org/MiniMax/configs/diffs/nvim-0.11_nvim-0.12)

### 구조

#### `init.lua`

시작 시 가장 먼저 실행되는 초기 파일입니다.

##### `nvim-pack-lock.json` (Neovim>=0.12용)

모든 설치된 플러그인에 대한 정보를 포함하는 `vim.pack` (내장 플러그인 관리자)용 락파일(lockfile)입니다. MiniMax에서 작동이 확인된 특정 리비전의 필수 플러그인을 초기 설정 중에 설치하기 위해 제공됩니다.

설치된 플러그인이 변경될 때마다(디스크에서의 상태 업데이트, 추적되는 `version` 변경, 삭제 등) 자동으로 업데이트됩니다. 수동으로 삭제하거나 편집하지 마세요.

락파일에 대한 자세한 내용은 [`:h vim.pack-lockfile`](https://neovim.io/doc/user/helptag.html?tag=vim.pack-lockfile)을, 플러그인 관리자 전반에 대해서는 [`:h vim.pack`](https://neovim.io/doc/user/helptag.html?tag=vim.pack)을 참조하세요.

#### `plugin/`

시작 시 알파벳 순서로 자동으로 실행되는 파일들입니다:

- `10_options.lua` - 내장 Neovim 동작.
- `20_keymaps.lua` - 사용자 정의 매핑, 주로 [`:h <Leader>`](https://neovim.io/doc/user/helptag.html?tag=<Leader>) 키 위주.
- `30_mini.lua` - MINI 설정.
- `40_plugins.lua` - MINI 외의 플러그인.

::: {.callout-note}
많은 설정에서 설정을 모듈화하기 위해 명시적인 `require()` 호출과 함께 'lua/' 디렉토리를 사용하는 것을 선호합니다. 사용해도 괜찮지만, 'lua' 네임스페이스를 차지한다는 단점이 있습니다. 모든 플러그인에서 공유되기 때문에 `require()` 중에 충돌이 발생할 수 있습니다. 보통 'lua/username'과 같이 전용 "사용자" 디렉토리 안에 설정 파일을 두어 해결합니다.

'plugin/' 방식은 이 문제가 없습니다. 또한 파일을 실행하기 위해 'init.lua' 내부에서 명시적인 `require()` 호출이 필요하지 않습니다.
:::

::: {.callout-tip}
이 방식에 대한 자세한 내용은 [`:h load-plugins`](https://neovim.io/doc/user/helptag.html?tag=load-plugins)를 참조하세요. 특히:
- 하위 디렉토리가 허용됩니다. 해당 파일들도 알파벳 순서로 소싱됩니다.
- Neovim이 `nvim -u path/to/file`과 같이 시작되어도 'plugin/' 파일들은 여전히 실행됩니다. `--noplugin`을 함께 전달하거나 [`:h $NVIM_APPNAME`](https://neovim.io/doc/user/helptag.html?tag=$NVIM_APPNAME) 방식을 사용하세요.
:::

#### `snippets/`

사용자 정의 스니펫. 데모용으로 단일 'global.json' 파일이 포함되어 있습니다 ('mini.snippets' 설정에서 사용됨).

#### `after/`

플러그인에 의해 추가된 동작을 덮어쓰기 위한 파일들입니다. 보통 'ftplugin/'과 같은 특수 하위 디렉토리에 위치합니다 ([`:h 'runtimepath'`](https://neovim.io/doc/user/helptag.html?tag='runtimepath') 참조). 이 디렉토리의 파일은 플러그인에서 제공하는 유사한 파일 다음에 적용됩니다.

교본용으로 제작되었으며, 'after/'를 사용하는 일반적인 방법의 예시가 포함되어 있습니다.

##### `after/ftplugin/`

파일 유형(filetype) 플러그인. [`:h 'filetype'`](https://neovim.io/doc/user/helptag.html?tag='filetype') 옵션이 설정될 때 소싱되는 파일들이 포함됩니다.

예를 들어, '\*.txt' 파일은 `text` 파일 유형을 가지므로, '\*.txt' 파일을 열 때 'ftplugin/text.lua'가 소싱됩니다. 여기에는 `text` 파일에만 존재해야 하는 동작을 정의합니다.

##### `after/lsp/` (Neovim>=0.11용)

LSP 서버를 설정하는 파일들입니다. Neovim 내장 기능인 [`:h vim.lsp.config()`](https://neovim.io/doc/user/helptag.html?tag=vim.lsp.config()) 및 [`:h vim.lsp.enable()`](https://neovim.io/doc/user/helptag.html?tag=vim.lsp.enable())에서 사용됩니다. 자세한 내용은 [`:h lsp-quickstart`](https://neovim.io/doc/user/helptag.html?tag=lsp-quickstart)를 참조하세요.

예를 들어, 'lsp/lua_ls.lua' 파일은 `vim.lsp.enable({ 'lua_ls' })` (즉, 동일한 이름으로) 호출 시 사용될 설정의 일부를 정의합니다.

##### `after/snippets/`

언어별 스니펫 정의가 포함된 파일들입니다. ['mini.snippets'](https://nvim-mini.org/mini.nvim/doc/mini-snippets.html)에서 사용됩니다. 'after/'에 위치하므로 플러그인(예: 'rafamadriz/friendly-snippets')에서 제공하는 모든 스니펫을 덮어씁니다.

예를 들어, 'snippets/lua.json'을 기반으로 Lua 파일 내부 Insert 모드에서 `l` + `<C-j>`를 입력하면 항상 `local $1 = $0` 스니펫이 삽입됩니다. 다른 스니펫 제공자에 이 스니펫이 있거나 충돌하는 스니펫이 있더라도 상관없습니다.
