# 기여하기

'mini.nvim'에 관심을 가져주시고 기여하고자 하셔서 감사합니다. 정말 큰 힘이 됩니다!

다음과 같은 방법으로 프로젝트에 기여하실 수 있습니다:

- **주변에 알리기**: 더 많은 사용자에게 프로젝트를 알리는 것은 큰 도움이 됩니다.
- **GitHub 이슈 생성**: 다음과 같은 유형의 이슈를 생성할 수 있습니다:
    - **버그 제보 (Bug report)**: 예상했던 결과와 실제 발생한 현상, 재현 가능한 단계를 설명해 주세요. 이슈를 만들기 전에 다음 사항을 확인해 주세요:
        - 의도된 동작(문서에 명시된 내용)이 아님을 확인해 주세요.
        - 이미 보고된 내용(열려 있거나 닫힌 이슈 포함)이 아닌지 확인해 주세요.
    - **기능 제안 (Feature request)**: 하나 이상의 모듈이 수행해야 할 기능을 간결하고 타당한 근거와 함께 설명해 주세요. 제안하기 전에, 이미 구현 계획이 없다고 명시된 기능(예: 'mini.comment'의 블록 주석)이 아닌지 확인해 주세요.
- **풀 리퀘스트 (PR) 생성**: 다음과 같은 유형이 가능합니다:
    - **코드 관련**: 버그 수정이나 기능 구현. **시작하기 전에 해당 내용이 프로젝트의 비전 및 목표와 일치하는지 확인해 주세요**. 가장 좋은 방법은 기존 이슈나 직접 만든 이슈에서 유지관리자로부터 긍정적인 피드백을 받는 것입니다. 최신 도움말 파일을 다시 생성했는지, 모든 테스트를 통과하는지 확인해 주세요 (나중 섹션 참조).
    - **문서 관련**: 'README.md', 코드 주석, 도움말 생성용 애노테이션 등의 오타/문구 수정. 이슈를 따로 만들지 않고 바로 PR을 보내셔도 좋습니다.
    - **'mini.base16' 및 'mini.hues' 모듈에 플러그인 통합 추가**.
- **다른 컬러 스킴에 명시적 지원 추가**: 모든 'mini.nvim' 모듈은 기본적으로 모든 컬러 스킴을 지원합니다 (하이라이트 그룹을 내장 하이라이트 그룹에 링크하는 방식). 하지만 특정 컬러 스킴에서는 어울리지 않을 수 있습니다. 다양한 컬러 스킴에서 'mini.nvim'을 명시적으로 지원하도록 업데이트하는 것을 적극 권장합니다. 이 파일 뒷부분에 하이라이트 그룹 목록이 있습니다.
- **[토론(Discussions)](https://github.com/nvim-mini/mini.nvim/discussions) 참여**.

정중하고 예의 바른 모든 기여를 언제나 환영합니다! 읽어주셔서 감사합니다!

## 커밋 메시지

- 변경 사항의 본질을 충분히 전달하면서도 가능한 한 간결하게 작성하세요. 1년 뒤에 커밋 이력을 보더라도 쉽게 이해할 수 있을지 생각해 보세요.

- 단일 커밋은 한 개의 모듈만 변경하거나, 모든 모듈에 영향을 주는(예: 전역 규칙 적용) 내용이어야 합니다. 두 개 이상의 모듈에 대한 변경 사항은 모듈별 커밋으로 나누어야 합니다.

- [Conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) 스타일을 따르세요:
    - 메시지 구조:

        ```
        <type>[optional scope][!]: <description>

        [optional body]

        [optional footer(s)]
        ```

    - `<type>`은 **필수**이며 다음 중 하나여야 합니다:
        - `ci` - 자동화(GitHub actions, 스크립트 등) 관련 변경.
        - `docs` - 사용자용 문서(help, README, CONTRIBUTING 등) 변경.
        - `feat` - 새로운 사용자 기능 추가.
        - `fix` - 사용자 이슈 해결.
        - `refactor` - 사용자에게 영향을 주지 않는 코드나 문서의 변경.
        - `style` - 관습적인 변경(포맷팅, 문구 수정 등) 및 그 효과.
        - `test` - 테스트 관련 변경.
      나중에 squash될 임시 커밋의 경우 `fixup` 타입을 사용하세요.
    - `[optional scope]`가 있다면 괄호 `()` 안에 작성하세요. 단일 모듈을 변경하는 경우 모듈 이름을 scope로 사용하는 것은 **필수**입니다. 모든 모듈에 관계된 경우 `ALL`을 사용하세요.
    - 하위 호환성이 깨지는 변경(Breaking change)은 `:` 앞에 `!`를 붙여 표시하세요.
    - `<description>`은 명령형 현재 시제로 작성하세요 ("change" 사용, "changed"나 "changes" 금지). 첫 줄은 72자 이내여야 하며, 대문자로 시작하지 않고 마침표 등의 문장 부호로 끝내지 마세요.
    - `[optional body]`가 있다면 평이한 문장으로 상세 내용과 동기를 작성하세요. 한 줄은 최대 80자여야 합니다.
    - `[optional footer(s)]`가 있다면 Git이나 GitHub 명령어를 포함할 수 있습니다. 이슈나 PR을 해결하는 경우 별도의 줄에 "Resolve #xxx"를 작성하세요.

- 모듈 이름 없이 함수 및 필드 이름을 사용하세요 (예: `MiniSurround.add()` 대신 `add()`).

예시:

```
feat(deps): add folds in update confirmation buffer
```

```
fix(jump): make operator not delete one character if target is not found

One main goal is to do that in a dot-repeatable way, because this is very
likely to be repeated after an unfortunate first try.

Resolve #688
```

```
refactor(bracketed): do not source 'vim.treesitter' on `require()`

Although less explicit, this considerably reduces startup footprint of
'mini.bracketed' in isolation.
```

```
feat(hues)!: update verbatim text to be distinctive
```

```
test(ALL): update screenshots to work on Nightly
```

### 자동 커밋 메시지 검사 (Linting)

- 이미 작성된 커밋 메시지를 검사하려면 `scripts/lintcommit-ci.sh <git-log-range>`를 실행하세요. 최신 커밋 하나를 검사하려면 `scripts/lintcommit-ci.sh HEAD~..HEAD`를 사용합니다.
- 커밋 전에 메시지를 검사하려면 [`pre-commit`](https://pre-commit.com/#install)을 설치하고 `pre-commit install --hook-type commit-msg`를 실행하세요. (ROOT 디렉토리에서 실행, `nvim` 실행 필요)

## 도움말 파일 생성

도움말 생성용 애노테이션을 업데이트했다면 파일을 재생성해 주세요. 프로젝트 루트에서 다음 중 하나를 실행하면 됩니다:

- 커맨드 라인에서 `make documentation` 실행.
- Neovim 내부에서 `:luafile scripts/minidoc.lua` 또는 `:lua require('mini.doc').generate()` 실행.

## 테스트

코드 변경 시 기존 테스트를 깨뜨리지 않는지 확인해 주세요. 기능을 추가하거나 버그를 수정한 경우 새 테스트 케이스를 추가해야 합니다.

- 커맨드 라인에서:
    - `make test`를 실행하여 모든 테스트 실행.
    - `make test_xxx`를 실행하여 `tests/test_xxx.lua` 파일만 실행 (예: `make test_ai`).
    - 여러 Neovim 버전(`nvim_07`, `nvim_08` 등)에 대해 테스트하려면 `NVIM_EXEC="nvim_07 nvim_08 nvim_09 nvim_010" make test`와 같이 실행하세요.
- Neovim 내부에서 `:lua require('mini.test').setup(); MiniTest.run()`을 실행하여 모든 테스트를, 또는 `:lua require('mini.test').setup(); MiniTest.run_file()`을 실행하여 현재 버퍼의 테스트만 실행할 수 있습니다.

더 자세한 입문서는 [TESTING.md](TESTING.md)를 참조하세요.

**참고**:

- 외부 의존성(git, LSP 서버 등)이 필요한 경우 모킹(Mocking)을 사용하여 테스트하세요. 'mini.pick', 'mini.completion' 등의 테스트 코드를 참고할 수 있습니다.
- 일부 테스트(주로 시간 지연 관련)는 불안정(flaky)할 수 있습니다. 테스트에 실패했으나 관련 코드 변경이 없다면 해당 테스트를 여러 번 다시 실행해 보세요. [TESTING.md의 'Retry' 섹션](TESTING.md#Retry)을 참조하세요.
- 견고한 테스트 작성을 위한 조언:
    - 비동기/느린 실행 테스트 시 `sleep()` 도우미를 사용하고, OS별 지연 시간 상수를 활용하세요.
    - 윈도우의 경로 구분자(`\`)를 고려하여 코딩하거나 테스트 파일을 작성하세요.

## 포맷팅

이 프로젝트는 Lua 코드 포맷팅을 위해 [StyLua](https://github.com/JohnnyMorganz/StyLua) 버전 2.1.0을 사용합니다. 변경 사항을 반영하기 전에:

- [StyLua v2.1.0 설치](https://github.com/JohnnyMorganz/StyLua#installation).
- 루트 디렉토리에서 `stylua .`를 실행하거나, `pre-commit`을 설치하여 자동 포맷팅 되도록 하세요.

## 하이라이트 그룹 목록

'mini.nvim' 모듈에서 정의하는 모든 하이라이트 그룹 목록입나다. 용도는 'doc' 디렉토리의 문서를 참조하세요.

- 'mini.animate':
    - `MiniAnimateCursor`
    - `MiniAnimateNormalFloat`

- 'mini.clue':
    - `MiniClueBorder`
    - `MiniClueDescGroup`
    - `MiniClueDescSingle`
    - `MiniClueNextKey`
    - `MiniClueNextKeyWithPostkeys`
    - `MiniClueSeparator`
    - `MiniClueTitle`

- 'mini.cmdline':
    - `MiniCmdlinePeekBorder`
    - `MiniCmdlinePeekLineNr`
    - `MiniCmdlinePeekNormal`
    - `MiniCmdlinePeekSep`
    - `MiniCmdlinePeekSign`
    - `MiniCmdlinePeekTitle`

- 'mini.completion':
    - `MiniCompletionActiveParameter`
    - `MiniCompletionDeprecated`
    - `MiniCompletionInfoBorderOutdated`

- 'mini.cursorword':
    - `MiniCursorword`
    - `MiniCursorwordCurrent`

- 'mini.deps':
    - `MiniDepsChangeAdded`
    - `MiniDepsChangeRemoved`
    - `MiniDepsHint`
    - `MiniDepsInfo`
    - `MiniDepsMsgBreaking`
    - `MiniDepsPlaceholder`
    - `MiniDepsTitle`
    - `MiniDepsTitleError`
    - `MiniDepsTitleSame`
    - `MiniDepsTitleUpdate`

- 'mini.diff':
    - `MiniDiffSignAdd`
    - `MiniDiffSignChange`
    - `MiniDiffSignDelete`
    - `MiniDiffOverAdd`
    - `MiniDiffOverChange`
    - `MiniDiffOverChangeBuf`
    - `MiniDiffOverContext`
    - `MiniDiffOverContextBuf`
    - `MiniDiffOverDelete`

- 'mini.files':
    - `MiniFilesBorder`
    - `MiniFilesBorderModified`
    - `MiniFilesCursorLine`
    - `MiniFilesDirectory`
    - `MiniFilesFile`
    - `MiniFilesNormal`
    - `MiniFilesTitle`
    - `MiniFilesTitleFocused`

- 'mini.hipatterns':
    - `MiniHipatternsFixme`
    - `MiniHipatternsHack`
    - `MiniHipatternsNote`
    - `MiniHipatternsTodo`

- 'mini.icons':
    - `MiniIconsAzure`
    - `MiniIconsBlue`
    - `MiniIconsCyan`
    - `MiniIconsGreen`
    - `MiniIconsGrey`
    - `MiniIconsOrange`
    - `MiniIconsPurple`
    - `MiniIconsRed`
    - `MiniIconsYellow`

- 'mini.indentscope':
    - `MiniIndentscopeSymbol`
    - `MiniIndentscopeSymbolOff`

- 'mini.jump':
    - `MiniJump`

- 'mini.jump2d':
    - `MiniJump2dDim`
    - `MiniJump2dSpot`
    - `MiniJump2dSpotAhead`
    - `MiniJump2dSpotUnique`

- 'mini.map':
    - `MiniMapNormal`
    - `MiniMapSymbolCount`
    - `MiniMapSymbolLine`
    - `MiniMapSymbolView`

- 'mini.notify':
    - `MiniNotifyBorder`
    - `MiniNotifyLspProgress`
    - `MiniNotifyNormal`
    - `MiniNotifyTitle`

- 'mini.operators':
    - `MiniOperatorsExchangeFrom`

- 'mini.pick':
    - `MiniPickBorder`
    - `MiniPickBorderBusy`
    - `MiniPickBorderText`
    - `MiniPickCursor`
    - `MiniPickIconDirectory`
    - `MiniPickIconFile`
    - `MiniPickHeader`
    - `MiniPickMatchCurrent`
    - `MiniPickMatchMarked`
    - `MiniPickMatchRanges`
    - `MiniPickNormal`
    - `MiniPickPreviewLine`
    - `MiniPickPreviewRegion`
    - `MiniPickPrompt`
    - `MiniPickPromptCaret`
    - `MiniPickPromptPrefix`

- 'mini.snippets':
    - `MiniSnippetsCurrent`
    - `MiniSnippetsCurrentReplace`
    - `MiniSnippetsFinal`
    - `MiniSnippetsUnvisited`
    - `MiniSnippetsVisited`

- 'mini.starter':
    - `MiniStarterCurrent`
    - `MiniStarterFooter`
    - `MiniStarterHeader`
    - `MiniStarterInactive`
    - `MiniStarterItem`
    - `MiniStarterItemBullet`
    - `MiniStarterItemPrefix`
    - `MiniStarterSection`
    - `MiniStarterQuery`

- 'mini.statusline':
    - `MiniStatuslineDevinfo`
    - `MiniStatuslineFileinfo`
    - `MiniStatuslineFilename`
    - `MiniStatuslineInactive`
    - `MiniStatuslineModeCommand`
    - `MiniStatuslineModeInsert`
    - `MiniStatuslineModeNormal`
    - `MiniStatuslineModeOther`
    - `MiniStatuslineModeReplace`
    - `MiniStatuslineModeVisual`

- 'mini.surround':
    - `MiniSurround`

- 'mini.tabline':
    - `MiniTablineCurrent`
    - `MiniTablineFill`
    - `MiniTablineHidden`
    - `MiniTablineModifiedCurrent`
    - `MiniTablineModifiedHidden`
    - `MiniTablineModifiedVisible`
    - `MiniTablineTabpagesection`
    - `MiniTablineTrunc`
    - `MiniTablineVisible`

- 'mini.test':
    - `MiniTestEmphasis`
    - `MiniTestFail`
    - `MiniTestPass`

- 'mini.trailspace':
    - `MiniTrailspace`
