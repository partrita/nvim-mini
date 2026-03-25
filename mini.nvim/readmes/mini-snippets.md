---
title: "mini.snippets"
---

<p align="center"> <img src="https://github.com/nvim-mini/assets/blob/main/logo-2/logo-snippets_readme.png?raw=true" alt="mini.snippets" style="max-width:100%;border:solid 2px"/> </p>
<p align="center">_'mini.nvim'의 `main` 브랜치에서 생성됨_</p>


### 스니펫(Snippet) 관리 및 확장

더 자세한 내용은 [기능](#features) 및 [상세 문서](../doc/mini-snippets.qmd)를 참조하세요.

---

::: {.callout-note}
이 프로젝트는 이전에 개인 계정인 `echasnovski`에서 관리되었습니다. 장기적인 프로젝트 안정성을 개선하기 위해 전용 조직으로 이전되었습니다. 자세한 내용은 [여기](https://github.com/nvim-mini/mini.nvim/discussions/1970)를 참조하세요.
:::

⦿ 이 모듈은 [mini.nvim](https://nvim-mini.org/mini.nvim) 라이브러리의 일부입니다. 이 모듈을 언급할 때는 [이 링크](https://nvim-mini.org/mini.nvim/readmes/mini-snippets)를 사용해 주세요.

⦿ 모든 기여(이슈, 풀 리퀘스트, 토론 등)는 'mini.nvim' 저장소에서 진행됩니다.

⦿ 일반적인 디자인 원칙, 비활성화/설정 레시피 등은 [전체 라이브러리 문서](https://nvim-mini.org/mini.nvim/doc/mini-nvim)를 참조하세요.

⦿ 이 모듈을 사용하는 전체 설정 예제는 [MiniMax](https://nvim-mini.org/MiniMax)를 참조하세요.

---

이 프로젝트의 성장을 돕고 싶지만 어디서부터 시작해야 할지 모르겠다면, ['mini.nvim'의 기여 가이드](https://nvim-mini.org/mini.nvim/CONTRIBUTING)를 확인하거나 'mini.nvim' 프로젝트 및 해당 독립 저장소에 Github 스타를 남겨주세요.

## 데모

![](https://github.com/nvim-mini/assets/blob/main/demo/demo-snippets.mp4?raw=true)

## 기능 {#features}

- 명시적으로 추가하거나 유연하고 성능이 우수한 내장 로더(loaders) 세트를 사용하여 스니펫 컬렉션을 관리합니다. [`:h MiniSnippets.gen_loader`](../doc/mini-snippets.qmd#minisnippets.gen_loader)를 참조하세요.

- 구성된 스니펫은 현재의 로컬 컨텍스트에 따라 매 확장(expand) 전에 효율적으로 결정됩니다. 예를 들어, 마크다운 코드 블록과 같이 서로 다른 로컬 Tree-sitter 언어에서 서로 다른 스니펫을 사용할 수 있습니다. [`:h MiniSnippets.default_prepare()`](../doc/mini-snippets.qmd#minisnippets.default_prepare)를 참조하세요.

- 현재 입력된 텍스트를 기반으로 삽입할 스니펫을 매칭합니다. 정확한 일치와 퍼지 매칭을 모두 지원합니다. [`:h MiniSnippets.default_match()`](../doc/mini-snippets.qmd#minisnippets.default_match)를 참조하세요.

- 여러 개의 스니펫이 매칭된 경우 `vim.ui.select()`를 통해 선택할 수 있습니다. [`:h MiniSnippets.default_select()`](../doc/mini-snippets.qmd#minisnippets.default_select)를 참조하세요.

- 특화된 인프로세스(in-process) LSP 서버를 시작하여 (자동)완성 엔진(예: [mini.completion](https://nvim-mini.org/mini.nvim/readmes/mini-completion)) 내부에 로드된 스니펫을 표시할 수 있습니다. [`:h MiniSnippets.start_lsp_server()`](../doc/mini-snippets.qmd#minisnippets.start_lsp_server)를 참조하세요.

- 스니펫 세션 동안 다음과 같이 설정 가능한 방식으로 삽입, 점프 및 편집을 수행합니다:
    - 점프 및 중단을 위한 설정 가능한 매핑.
    - 탐색을 용이하게 하기 위해 탭스톱(tabstops) 간의 점프가 순환(wrap around)됩니다.
    - 세션이 자동으로 중단되는 규칙을 이해하기 쉽습니다.
    - 상대적 들여쓰기를 유지하면서 연결된 탭스톱의 텍스트를 동기화합니다.
    - 동적인 탭스톱 상태 시각화 (현재/방문함/방문하지 않음 등).
    - 빈 탭스톱의 인라인 시각화 (Neovim>=0.10 필요).
    - 주석 내부에서 작동하며 새 줄에서도 주석 리더(leader)를 유지합니다.
    - 중첩된 세션을 지원합니다 (활성 세션이 있는 동안 다른 스니펫 확장 가능).

    [`:h MiniSnippets.default_insert()`](../doc/mini-snippets.qmd#minisnippets.default_insert)를 참조하세요.

- 스니펫 본문을 분석하기 쉬운 데이터 구조로 파싱하는 기능을 노출합니다. [`:h MiniSnippets.parse()`](../doc/mini-snippets.qmd#minisnippets.parse)를 참조하세요.

참고:

- 기본적으로 어떠한 스니펫 컬렉션도 설정하지 않습니다. 매칭할 스니펫을 가지려면 `config.snippets`를 명시적으로 채워야 합니다.
- 내장된 스니펫 컬렉션은 포함되어 있지 않습니다. 사용자가 직접 스니펫을 추가하거나 전용 플러그인을 사용하여 추가해야 합니다.
- 기본 스니펫 세션에서 변수/탭스톱 변환(transformations)은 지원하지 않습니다. 이는 간결하게 구현하기 어려운 ECMAScript 정규 표현식 파서가 필요하기 때문입니다.

더 자세한 정보는 다음을 참조하세요:

- [개요](#overview)
- [`:h MiniSnippets-glossary`](../doc/mini-snippets.qmd#minisnippets-glossary)
- [`:h MiniSnippets-examples`](../doc/mini-snippets.qmd#minisnippets-examples)
- [`:h MiniSnippets-in-other-plugins`](../doc/mini-snippets.qmd#minisnippets-in-other-plugins) (플러그인 제작자용)

## 의존성 {#dependencies}

이 모듈은 스니펫 컬렉션을 포함하지 않습니다. 수동으로 생성하거나 [rafamadriz/friendly-snippets](https://github.com/rafamadriz/friendly-snippets)와 같은 전용 플러그인을 설치하세요.

## 빠른 시작 {#quickstart}

- 다음과 같은 설정을 사용하세요:

    ```lua
    local gen_loader = require('mini.snippets').gen_loader
    require('mini.snippets').setup({
      snippets = {
        -- 전역 스니펫이 포함된 사용자 정의 파일을 먼저 로드합니다 (윈도우 환경에 맞게 조정 필요)
        gen_loader.from_file('~/.config/nvim/snippets/global.json'),

        -- 'runtimepath' 디렉터리의 "snippets/" 하위 디렉터리에서 파일을 읽어
        -- 현재 언어에 기반한 스니펫을 로드합니다.
        gen_loader.from_lang(),
      },
    })
    ```

    이 설정은 모든 버퍼에 나타나는 커스텀 "전역" 스니펫 파일 하나와 로컬 언어에 따라 로드되는 스니펫들을 가질 수 있게 해줍니다 ([`:h MiniSnippets.gen_loader.from_lang()`](../doc/mini-snippets.qmd#minisnippets.gen_loader.from_lang) 참조).

    언어 스니펫을 수동으로 생성하거나 (예: `$XDG_CONFIG_HOME/nvim/snippets/lua.json` 파일을 생성하고 채움), 전용 스니펫 컬렉션 플러그인 (예: [rafamadriz/friendly-snippets](https://github.com/rafamadriz/friendly-snippets))을 설치하여 추가하세요.

    **참고**: 모든 내장 로더는 기본적으로 출력을 캐싱합니다. 즉, 파일을 처음 읽은 뒤에는 파일을 변경해도 현재 Neovim 세션 동안에는 반영되지 않습니다. 필요한 경우 캐시를 초기화하는 방법은 [`:h MiniSnippets.gen_loader`](../doc/mini-snippets.qmd#minisnippets.gen_loader)를 참조하세요.

- 특정 언어가 지정된 파일(예: 설정의 'init.lua')에서 Neovim을 열고 `<C-j>`를 누릅니다.

디자인과 확장을 이해하는 가장 좋은 방법은 직접 사용해 보는 것입니다. 다음은 간단한 데모를 위한 추가 단계입니다:

- 설정 디렉터리에 'snippets/global.json' 파일을 생성하고 다음 내용을 입력합니다:

    ```json
    {
      "Basic":        { "prefix": "ba", "body": "T1=$1 T2=$2 T0=$0"         },
      "Placeholders": { "prefix": "pl", "body": "T1=${1:aa}\nT2=${2:<$1>}"  },
      "Choices":      { "prefix": "ch", "body": "T1=${1|a,b|} T2=${2|c,d|}" },
      "Linked":       { "prefix": "li", "body": "T1=$1\n\tT1=$1"            },
      "Variables":    { "prefix": "va", "body": "Runtime: $VIMRUNTIME\n"    },
      "Complex":      {
        "prefix": "co",
        "body": [ "T1=${1:$RANDOM}", "T3=${3:$1_${2:$1}}", "T2=$2" ]
      }
    }
    ```
- Neovim을 엽니다. 각 스니펫 접두사(prefix)를 입력하고 `<C-j>`를 누릅니다 (이미 활성화된 세션이 있더라도 가능합니다). 거기서부터 탐색해 보세요.

## 개요 {#overview}

스니펫은 자주 사용되는 텍스트를 위한 템플릿입니다. 전형적인 워크플로우는 스니펫의 (설정 가능한) 접두사를 입력하고 이를 스니펫 세션으로 확장(expand)하는 것입니다. 그러면 사전 정의된 텍스트가 추가되고 사용자가 특정 위치에서 상호작용하며 변경/추가할 수 있게 됩니다.

이 개요는 매핑 및 확장에 대해 기본 설정을 가정합니다. 자세한 내용은 [`:h MiniSnippets.config`](../doc/mini-snippets.qmd#minisnippets.config) 및 [`:h MiniSnippets-examples`](../doc/mini-snippets.qmd#minisnippets-examples)를 참조하세요.

### 스니펫 구조

스니펫은 세 부분으로 구성됩니다:

- `Prefix` (접두사) - 현재 텍스트와 매칭하는 데 사용되는 식별자.
- `Body` (본문) - 적절한 문법으로 실제로 삽입되는 콘텐츠.
- `Desc` (설명) - 사람이 읽을 수 있는 형식의 설명.

예시: `{ prefix = 'tis', body = 'This is snippet', desc = 'Snip' }`
`tis`를 입력하고 확장 매핑(기본값 `<C-j>`)을 누르면 "tis"가 제거되고 "This is snippet"이 추가되며 커서가 입력 모드로 끝에 위치합니다.

### 문법 (Syntax)

짧은 접두사 입력 후 텍스트만 삽입하는 것으로도 충분히 강력합니다. 더 유연한 기능을 위해 스니펫 본문을 특별한 방식으로 형식화할 수 있습니다. 이 모듈은 [LSP 사양](https://microsoft.github.io/language-server-protocol/specifications/lsp/3.18/specification/#snippet_syntax)에 정의된 문법을 지원합니다 (약간의 차이는 있습니다).

기본 문법 기능의 빠른 개요:

- 탭스톱(Tabstops)은 해당 위치에서 대화형 편집을 하기 위한 스니펫 부분입니다. `$1`, `$2` 등으로 표시됩니다.

  탭스톱 간의 이동을 "점핑(jumping)"이라고 하며, 탭스톱 식별자의 숫자 순서대로 특수 키를 눌러 수행합니다: 다음 탭스톱과 이전 탭스톱으로 점프하려면 각각 `<C-l>`과 `<C-h>`를 사용합니다.

  특별한 탭스톱인 `$0`을 "최종 탭스톱(final tabstop)"이라고 합니다: 이는 스니펫 세션이 언제 자동으로 종료될지 결정하는 데 사용되며, 점핑 과정에서 마지막에 방문하게 됩니다.

  예시: `T1=$1 T2=$2 T0=$0`은 세 개의 탭스톱을 가진 `T1= T2= T0=`으로 확장됩니다.

- 탭스톱은 자리 표시자(Placeholder)를 가질 수 있습니다: 탭스톱이 아직 편집되지 않았을 때 사용되는 텍스트입니다. 편집하지 않으면 이 텍스트가 유지됩니다. 자리 표시자 자체도 문법을 따르므로 내부에 또 다른 탭스톱이나 자리 표시자를 포함할 수 있습니다 (중첩 가능). 자리 표시자가 있는 탭스톱은 `${1:placeholder}`로 표시됩니다 (`$1`은 `${1:}`과 같습니다).

  예시: `T1=${1:text} T2=${2:<$1>}`은 `T1=text T2=<text>`로 확장됩니다. 첫 번째 자리 표시자에서 `x`를 입력하면 `T1=x T2=<x>`가 됩니다. 한 번 점프한 뒤 `y`를 입력하면 `T1=x T2=y`가 됩니다.

- 동일한 식별자를 가진 탭스톱이 여러 개 있을 수 있습니다. 이들은 연결(linked)되어 텍스트 편집 중에 동기화되어 업데이트됩니다. 서로 다른 자리 표시자를 가질 수도 있지만, 첫 번째(왼쪽에서 오른쪽으로) 탭스톱의 자리 표시자와 동일하게 강제됩니다.

  예시: `T1=${1:text} T1=$1`은 `T1=text T1=text`로 확장됩니다. 첫 번째 자리 표시자에서 `x`를 입력하면 `T1=x T1=x`가 됩니다.

- 탭스톱은 선택지(Choices)를 가질 수 있습니다: 탭스톱 텍스트에 대한 제안입니다. `${1|a,b,c|}`로 표시됩니다. 탭스톱으로 점프한 후 선택지가 표시됩니다 (`:h ins-completion`과 유사한 인터페이스 사용). 첫 번째 선택지가 자리 표시자로 사용됩니다.

  예시: `T1=${1|left,right|}`은 `T1=left`로 확장됩니다.

- 변수(Variables)를 사용하여 사용자 상호작용 없이 자동으로 텍스트를 삽입할 수 있습니다. 탭스톱과 마찬가지로 각 변수는 정의되지 않았을 때 사용될 자리 표시자를 가질 수 있습니다. 에디터 상태를 설명하는 특별한 변수 세트가 제공됩니다.

  예시: `V1=$TM_FILENAME V2=${NOTDEFINED:placeholder}`는 `V1=현재-파일-기준이름 V2=placeholder`로 확장됩니다.

LSP 사양과는 몇 가지 차이점이 있습니다: 변수 변환(transformations) 미지원, 더 넓은 범위의 지원되는 특수 변수 등. 자세한 내용은 [`:h MiniSnippets-syntax-specification`](../doc/mini-snippets.qmd#minisnippets-syntax-specification)을 참조하세요.

프로그램 방식으로 스니펫 본문을 데이터 구조로 파싱하려면 [`:h MiniSnippets.parse()`](../doc/mini-snippets.qmd#minisnippets.parse) 함수를 사용할 수 있습니다.

### 확장 (Expand)

스니펫을 사용하는 것은 "확장(expanding)"이라고 불리는 과정을 통해 이루어집니다:

- 스니펫 접두사 또는 인식 가능한 일부를 입력합니다.
- `<C-j>`를 눌러 확장합니다. 다음 단계들이 수행됩니다:
    - 현재 컨텍스트(버퍼 + 로컬 언어)에서 사용 가능한 스니펫을 준비합니다. 이를 통해 설정 시에 컨텍스트마다 다른 스니펫을 반환하는 일반적인 함수 로더를 가질 수 있습니다.
    - 커서 왼쪽의 텍스트와 가용한 접두사를 매칭합니다. 먼저 정확한 매칭을 시도하고 실패하면 퍼지 매칭을 시도합니다.
    - 여러 개가 매칭되면 `vim.ui.select()`를 사용하여 하나를 선택합니다.
    - 단일 매칭된 스니펫을 삽입합니다. 스니펫에 탭스톱이 포함되어 있으면 스니펫 세션을 시작합니다.

더 자세한 정보는 도움말의 다음 섹션들을 참조하세요:

- [`:h MiniSnippets.default_prepare()`](../doc/mini-snippets.qmd#minisnippets.default_prepare)
- [`:h MiniSnippets.default_match()`](../doc/mini-snippets.qmd#minisnippets.default_match)
- [`:h MiniSnippets.default_select()`](../doc/mini-snippets.qmd#minisnippets.default_select)
- [`:h MiniSnippets.default_insert()`](../doc/mini-snippets.qmd#minisnippets.default_insert)

스니펫 세션은 탭스톱 위치에서 대화형 편집을 가능하게 합니다:

- 모든 탭스톱 위치는 탭스톱 "상태"(현재/방문함/방문하지않음/최종 여부 및 이미 편집되었는지 여부)에 따라 시각화됩니다.

  빈 탭스톱은 인라인 가상 텍스트(`•` / `∎`는 각각 일반/최종 탭스톱용)로 시각화됩니다. 세션이 중단되면 사라집니다.

- 첫 번째 탭스톱에서 세션을 시작합니다. 자리 표시자를 대체할 텍스트를 입력합니다. 현재 탭스톱의 작업이 끝나면 `<C-l>`로 다음 탭스톱으로 점프합니다. 이를 반복합니다. 이전 탭스톱을 수정하고 싶으면 `<C-h>`로 뒤로 점프합니다. 점프는 끝에서 다시 시작 지점으로 순환됩니다 (최종 탭스톱 다음은 첫 번째 탭스톱).

- 탭스톱에 선택지가 있는 경우, `<C-n>` / `<C-p>`를 사용하여 다음 / 이전 항목을 선택합니다.

- 활성 세션이 있는 동안 또 다른 스니펫 세션을 시작할 수 있습니다. 이는 중첩된 세션을 생성합니다: 현재 세션을 일시 중단하고 새 세션을 시작합니다. 새로 생성된 세션이 종료되면 일시 중단된 세션이 재개됩니다.

- `<C-c>`를 눌러 수동으로 세션을 중단하거나 자동으로 중단되게 합니다: 최종 탭스톱이 현재 상태일 때 텍스트 수정을 하거나 노멀 모드로 나가면 됩니다. 스니펫에 최종 탭스톱이 명시적으로 정의되어 있지 않으면 스니펫 끝에 자동으로 추가됩니다.

스니펫 세션에 대한 자세한 내용은 [`:h MiniSnippets-session`](../doc/mini-snippets.qmd#minisnippets-session)을 참조하세요.

완성 엔진(LSP 완성을 지원하는 [mini.completion](https://nvim-mini.org/mini.nvim/readmes/mini-completion) 또는 `:h vim.lsp.completion` 등)을 통해 스니펫을 선택하고 삽입하려면 `require('mini.snippets').setup()` 호출 후 [`:h MiniSnippets.start_lsp_server()`](../doc/mini-snippets.qmd#minisnippets.start_lsp_server)를 호출하세요. 이는 'mini.snippets'로 로드된 스니펫을 매칭하고 제공하는 LSP 서버를 설정합니다. 완성 엔진으로 매칭하려면 `start_lsp_server({ match = false })`를 사용하세요.

### 관리 (Management)

**중요**: 'mini.snippets'는 기본적으로 어떠한 스니펫도 불러오지 않으므로, [`:h MiniSnippets.setup()`](../doc/mini-snippets.qmd#minisnippets.setup) 내부에서 [`:h MiniSnippets.config`](../doc/mini-snippets.qmd#minisnippets.config)를 따라 명시적으로 수행해야 합니다.

권장되는 스니펫 관리 방식은 스니펫 데이터가 포함된 전용 파일을 생성하고 `config.snippets`에서 함수 로더를 통해 로드하는 것입니다. 기본적인 (하지만 강력한) 스니펫 관리 설정은 [빠른 시작](#quickstart)을 참조하세요.

지원되는 파일의 일반적인 아이디어는 일반적인 스니펫 컬렉션들에 대해 즉각적인 사용 경험을 제공하는 것입니다. 대표적으로 [rafamadriz/friendly-snippets](https://github.com/rafamadriz/friendly-snippets)가 있습니다.

지원되는 파일 형식은 다음과 같습니다:

- 확장자:
    - JSON 객체로 읽기/디코드됨: `*.json`, `*.code-snippets`
    - Lua 파일로 실행하여 반환값 사용: `*.lua`

- 콘텐츠 형식:
    - 사전형(Dict-like): JSON의 객체, Lua의 반환된 테이블. 순서 보장 없음.
    - 배열형(Array-like): JSON의 배열, Lua의 반환된 배열 테이블. 순서 유지.

단일 스니펫이 포함된 파일 콘텐츠 예시:

- Lua 사전형:   `return { name = { prefix = 't', body = 'Text' } }`
- Lua 배열형:  `return { { prefix = 't', body = 'Text', desc = 'name' } }`
- JSON 사전형:  `{ "name": { "prefix": "t", "body": "Text" } }`
- JSON 배열형: `[ { "prefix": "t", "body": "Text", "desc": "name" } ]`

일반적인 조언:

- 'runtimepath'의 어느 경로라도 "snippets" 하위 디렉터리에 파일을 두세요 (예: `$XDG_CONFIG_HOME/nvim/snippets/global.json`). 이는 [`:h MiniSnippets.gen_loader.from_runtime()`](../doc/mini-snippets.qmd#minisnippets.gen_loader.from_runtime) 및 [빠른 시작](#quickstart)과 호환됩니다.
- 더 넓은 크로스 플랫폼 설정을 원한다면 사전형 콘텐츠가 포함된 `*.json` 파일을 권장합니다. 그 외의 경우 배열형 콘텐츠가 포함된 `*.lua` 파일을 사용하세요.

참고:

- VSCode 스타일의 "package.json" 파일은 내장 지원하지 않습니다. 내장 또는 사용자 정의 로더를 통해 [`:h MiniSnippets.setup()`](../doc/mini-snippets.qmd#minisnippets.setup)에서 구조를 수동으로 정의하세요.
- 스니펫 데이터의 `scope` 필드는 내장 지원하지 않습니다. 스니펫을 미리 작은 파일들로 분리해 두고 필요할 때 로드하는 방식이 권장됩니다.

지원되는 스니펫 문법은 [`:h MiniSnippets-syntax-specification`](../doc/mini-snippets.qmd#minisnippets-syntax-specification) 또는 [문법](#syntax) 섹션을 참조하세요.

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

    | 브랜치 | 코드 스니펫                                                       |
    |--------|--------------------------------------------------------------------|
    | Main   | `add('nvim-mini/mini.snippets')`                                   |
    | Stable | `add({ source = 'nvim-mini/mini.snippets', checkout = 'stable' })` |

</details>

<details>
<summary><a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                  |
    |--------|-----------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.nvim', version = false },` |
    | Stable | `{ 'nvim-mini/mini.nvim', version = '*' },`   |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                      |
    |--------|---------------------------------------------------|
    | Main   | `{ 'nvim-mini/mini.snippets', version = false },` |
    | Stable | `{ 'nvim-mini/mini.snippets', version = '*' },`   |

</details>

<details>
<summary><a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a> 사용 시</summary>

- 'mini.nvim' 라이브러리:

    | 브랜치 | 코드 스니펫                                         |
    |--------|------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.nvim'`                         |
    | Stable | `Plug 'nvim-mini/mini.nvim', { 'branch': 'stable' }` |

- 단독 플러그인:

    | 브랜치 | 코드 스니펫                                             |
    |--------|----------------------------------------------------------|
    | Main   | `Plug 'nvim-mini/mini.snippets'`                         |
    | Stable | `Plug 'nvim-mini/mini.snippets', { 'branch': 'stable' }` |

</details>

**중요**: 매칭할 스니펫을 가지려면 비어 있지 않은 `snippets` 항목과 함께 `require('mini.snippets').setup()`을 호출해야 합니다.

**참고**: 윈도우 환경에서는 파일 경로가 너무 길어 발생하는 문제(`error: unable to create file <some file name>: Filename too long`)가 있을 수 있습니다. 다음 중 하나를 시도해 보세요:

- 해당 git 전역 설정 값을 활성화합니다: `git config --system core.longpaths true`. 그 후 다시 설치를 시도하세요.
- 더 짧은 경로의 다른 위치에 플러그인을 설치합니다.

## 기본 설정 {#default-config}

```lua
-- `setup()` 안에 이 내용을 복사할 필요는 없습니다. 자동으로 사용됩니다.
{
  -- 스니펫 및 로더 배열 (자세한 내용은 |MiniSnippets.config| 참조).
  -- 기본적으로 아무것도 정의되어 있지 않습니다. 매칭할 스니펫을 수동으로 추가하세요.
  snippets = {},

  -- 모듈 매핑. 비활성화하려면 `''`(빈 문자열)을 사용하세요.
  mappings = {
    -- 커서 위치에서 스니펫 확장. 입력 모드에서 전역적으로 생성됩니다.
    expand = '<C-j>',

    -- 기본 `expand.insert` 세션과 상호작용합니다.
    -- 활성 세션 동안에만 생성됩니다.
    jump_next = '<C-l>',
    jump_prev = '<C-h>',
    stop = '<C-c>',
  },

  -- 스니펫 확장을 설명하는 함수들. `nil`인 경우 기본값은 
  -- `MiniSnippets.default_<field>()`입니다.
  expand = {
    -- 컨텍스트에서 원시 설정 스니펫들을 결정
    prepare = nil,
    -- 커서 위치에서 결정된 스니펫 매칭
    match = nil,
    -- 매칭된 스니펫 중 하나를 선택할 수 있음
    select = nil,
    -- 선택된 스니펫 삽입
    insert = nil,
  },
}
```

## 유사한 플러그인 {#similar-plugins}

- [L3MON4D3/LuaSnip](https://github.com/L3MON4D3/LuaSnip)
- Neovim>=0.10의 내장 스니펫 확장, `:h vim.snippet` 참조 (스니펫 확장 기능만 제공하고 관리는 하지 않음).
- [rafamadriz/friendly-snippets](https://github.com/rafamadriz/friendly-snippets) (엄선된 스니펫 파일 컬렉션)
- [abeldekat/cmp-mini-snippets](https://github.com/abeldekat/cmp-mini-snippets) ('mini.snippets'를 통합하는 [hrsh7th/nvim-cmp](https://github.com/hrsh7th/nvim-cmp)용 소스)
