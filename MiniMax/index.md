---
title: "MiniMax"
---

<p align="center"> <img src="logo.png" alt="mini.nvim" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'MiniMax'의 `main` 브랜치에서 생성됨_</p>


## MINI를 최대한 활용한 Neovim

MiniMax는 Neovim 설정 생성기입니다. [스크립트를 실행](#setting-up)하고 나면, 당신의 설정은:

- 일관되고 강력하며 유연한 구성을 위해 주로 'mini.nvim' 모듈을 기반으로 합니다.
- 즉시 사용할 수 있는 안정적이고 정제된, 기능이 풍부한 Neovim 환경을 제공합니다.
- 추가 개발이 가능한 최소한의 구조를 가집니다.
- 읽기 쉽게 작성된 상세한 주석이 포함되어 있습니다.

[참조 설정](configs)을 둘러보세요. 생성 과정에서 Neovim 버전에 따라 가장 적합한 설정이 선택됩니다.

변경 이력은 [변경 이력](CHANGELOG.md)을 참조하세요.

이 프로젝트가 유용하다고 생각된다면 Github 스타를 남겨주세요.

### 미리보기

<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-minimax_1.png?raw=true"> <img alt="설정 과정" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-minimax_1.png?raw=true" style="width: 45%"/> </a>
<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-minimax_2.png?raw=true"> <img alt="피커(Picker)" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-minimax_2.png?raw=true" style="width: 45%"/> </a>

<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-minimax_3.png?raw=true"> <img alt="힌트(Clues)" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-minimax_3.png?raw=true" style="width: 45%"/> </a>
<a href="https://github.com/nvim-mini/assets/blob/main/demo/demo-minimax_4.png?raw=true"> <img alt="파일 탐색기" src="https://github.com/nvim-mini/assets/blob/main/demo/demo-minimax_4.png?raw=true" style="width: 45%"/> </a>

### 지향하지 않는 것

MiniMax는 "Neovim 배포판(distribution)"이 아닙니다. 즉, 자동 설정 업데이트가 없습니다. 설정이 완료된 후에는 당신이 직접 개선하고 업데이트해야 하며, 이 방식이 훨씬 더 안정적입니다. MiniMax 자체가 어떻게 업데이트되는지는 [업데이트](#updating) 및 [변경 이력](CHANGELOG.md)을 통해 확인할 수 있으며, 이에 맞춰 자신의 설정을 조정할 수 있습니다.

또한 모든 Neovim 기능과 플러그인의 설치 및 사용법을 다루는 종합 가이드가 아닙니다. 설정의 대부분은 안정성과 기능 사이의 균형을 맞추기 위해 신중하게 선택되었습니다.

### 요구 사항

#### 소프트웨어

- [Neovim](https://neovim.io/) 실행 파일. 이름은 `nvim`으로 가정합니다.
- [Git](https://git-scm.com/) 실행 파일. 이름은 `git`으로 가정합니다.
- 운영체제: Neovim이 지원하는 모든 OS.
- 플러그인 다운로드를 위한 인터넷 연결.
- (선택 사항, 권장) [`ripgrep`](https://github.com/BurntSushi/ripgrep#installation).
- (선택 사항, 권장) [트루 컬러(true colors)](https://github.com/termstandard/colors#truecolor-support-in-output-devices) 및 [Nerd Font 아이콘](https://www.nerdfonts.com/)을 지원하는 터미널 에뮬레이터(또는 GUI). 전체 Nerd Font가 필요하지는 않으며, [`NerdFontsSymbolsOnly`](https://github.com/ryanoasis/nerd-fonts/releases/latest)를 폴백으로 사용하는 것만으로도 충분합니다.
- (선택 사항, 권장) [`nvim-treesitter/nvim-treesitter` 플러그인의 `main` 브랜치](https://github.com/nvim-treesitter/nvim-treesitter/tree/main?tab=readme-ov-file#requirements)를 위한 시스템 요구 사항.

#### 지식

다음에 대한 기초적인 이해가 필요합니다:

- CLI(커맨드 라인) 사용: 터미널 열기, 파일 시스템 탐색, 명령 실행, 종료.

- Neovim 사용: 열기, 모드 기반 편집, 도움말 읽기, 종료. Neovim 내부에서 [`:h help.txt`](https://neovim.io/doc/user/helptag.html?tag=help.txt) (또는 링크 클릭)를 입력하고 `<Enter>`를 누르면 기본 사항을 익히는 데 도움이 됩니다.

    개인적인 추천 사항 (전문 수록은 아니지만 내용을 숙지하세요): [`:h notation`](https://neovim.io/doc/user/helptag.html?tag=notation), [`:h key-notation`](https://neovim.io/doc/user/helptag.html?tag=key-notation), [`:h vim-modes`](https://neovim.io/doc/user/helptag.html?tag=vim-modes), [`:h mode-switching`](https://neovim.io/doc/user/helptag.html?tag=mode-switching), [`:h windows-intro`](https://neovim.io/doc/user/helptag.html?tag=windows-intro),  [`:h vimtutor`](https://neovim.io/doc/user/helptag.html?tag=vimtutor)

- Neovim 내부에서 도움말 파일 읽기: 도움말 태그(tags), 키 표기법(key notations), 탐색 방식.

  ::: {.callout-tip}
  이미 MiniMax 설정을 사용 중이라면, `<Space>` + `f` + `h`를 눌러 모든 도움말 태그를 퍼지 검색할 수 있습니다.
  :::

- [Lua 언어](https://learnxinyminutes.com/lua/) 읽기: 변수, 테이블, 함수 호출, 반복문. [`:h lua-concepts`](https://neovim.io/doc/user/helptag.html?tag=lua-concepts) 및 [`:h lua-guide`](https://neovim.io/doc/user/helptag.html?tag=lua-guide)도 함께 확인하세요.

#### 동기 부여

- 문서를 읽고 연습할 준비가 되어 있다면 정말 큰 도움이 될 것입니다. Neovim이나 MINI가 처음이라면 내용이 많게 느껴질 수 있습니다. 하지만 배우고 연습할수록 쉬워집니다. 이런 과정 없이는 Neovim과 MiniMax를 충분히 즐기기 어려울 수 있습니다.

### 설정 방법 {#setting-up}

이 방법은 임시로 'nvim-minimax' 설정을 구성하며 기존 설정에는 영향을 주지 않습니다. 상시 설정으로 사용하려면 `NVIM_APPNAME=nvim-minimax` 부분을 모두 제거하세요.

```bash
# 다운로드
git clone --filter=blob:none https://github.com/nvim-mini/MiniMax ./MiniMax

# 설정 구성 (설정 파일을 복사하고 Git 저장소를 초기화할 수 있음)
NVIM_APPNAME=nvim-minimax nvim -l ./MiniMax/setup.lua

# Neovim 시작
NVIM_APPNAME=nvim-minimax nvim

# Neovim>=0.12에서는 `y`를 눌러 나열된 모든 플러그인 설치를 승인하세요.
# 플러그인 설치가 완료될 때까지 기다리세요 (새로운 알림이 더 이상 나타나지 않아야 함).

# 새로운 설정을 즐기세요!
# 설정 파일을 읽는 것부터 시작해 보세요. `<Space>`+`e`+`i`를 입력하면 'init.lua'가 열립니다.
```

참고:

- MiniMax 프로젝트는 GitHub UI 등을 통해 수동으로 다운로드할 수도 있습니다.

- `NVIM_APPNAME=nvim-minimax`를 사용하면 설정 디렉토리는 유닉스 계열에서는 '\~/.config/nvim-minimax', 윈도우에서는 '\~/AppData/Local/nvim-minimax'가 됩니다.

    상시 설정 디렉토리는 유닉스 계열에서는 '\~/.config/nvim', 윈도우에서는 '\~/AppData/Local/nvim'입니다.

- 설정 도중 파일이 백업되었다는 메시지가 나오면, 대상 설정 디렉토리에 MiniMax의 파일들과 충돌하는 파일이 이미 존재함을 의미합니다. 기존 파일은 `MiniMax-backup` 디렉토리로 이동되었습니다. 필요에 따라 복원하고 백업 디렉토리를 삭제하세요.

- [MiniMax](configs) 디렉토리를 직접 탐색하여 자신에게 가장 잘 맞는 참조 설정이나 그 일부분을 찾을 수 있습니다. 관련 설정 예제('init.lua'부터 시작)를 읽어보고 흥미로운 부분을 기존 설정에 적용해 보세요.

### 업데이트 {#updating}

MiniMax는 이미 설정된 구성에 대해 완전 자동 업데이트를 제공하지 않습니다. [참조 설정](configs)과 [변경 이력](CHANGELOG.md)을 수동으로 확인하여 변경 사항을 살펴보는 것이 권장되는 방식입니다.

자동 업데이트에 가장 가까운 방법은 다음과 같습니다:

```bash
# MiniMax 자체 업데이트 가져오기
git -C ./MiniMax pull

# 설정 스크립트 다시 실행. 상시 설정인 경우 `NVIM_APPNAME=nvim-minimax` 제거
NVIM_APPNAME=nvim-minimax nvim -l ./MiniMax/setup.lua

# 백업된 파일에 대한 메시지가 나타날 수 있습니다:
# 1. 충돌하는 파일이 있는 'MiniMax-backup' 디렉토리를 확인합니다.
# 2. 필요한 파일을 복구합니다.
# 3. 백업 디렉토리를 삭제합니다.
```

### 유사한 프로젝트

- [nvim-lua/kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim)

- 더 자동화된 방식 ("Neovim 배포판"):
    - [LazyVim/LazyVim](https://github.com/LazyVim/LazyVim)
    - [NvChad/NvChad](https://github.com/NvChad/NvChad)
    - [AstroNvim/AstroNvim](https://github.com/AstroNvim/AstroNvim)

---

© Evgeni Chasnovski, [MIT](https://choosealicense.com/licenses/mit/)
