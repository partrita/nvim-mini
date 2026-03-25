# nvim-mini.org

이 저장소는 **MINI** (**M**odular **I**ndependent **N**eovim **I**mprovements)의 공식 웹사이트인 [nvim-mini.org](https://nvim-mini.org)의 소스 코드를 포함하고 있습니다.

## 개요

이 웹사이트는 [Quarto](https://quarto.org/)를 사용하여 구축되었으며 다음과 같은 구성 요소의 중앙 허브 역할을 합니다:

- [**mini.nvim**](https://github.com/echasnovski/mini.nvim): 독립적인 Neovim 모듈들의 컬렉션.
- [**MiniMax**](https://github.com/echasnovski/MiniMax): 최소한이면서도 최대한 유용한 Neovim 설정.
- **블로그**: MINI 생태계에 관한 공지사항 및 업데이트.

## 구조

- `index.qmd`: 랜딩 페이지.
- `mini.nvim/`: `mini.nvim` 저장소에서 미러링된 문서 및 리소스.
- `MiniMax/`: `MiniMax` 저장소에서 미러링된 문서 및 리소스.
- `blog/`: Quarto 블로그 포스트.
- `_scripts/`: 문서 동기화 및 처리를 위한 Lua 및 쉘 스크립트.
- `assets/`: 이미지 및 기타 정적 에셋.
- `theme/`: Quarto 테마 및 문법 정의.

## 개발

`mini.nvim/` 및 `MiniMax/`의 콘텐츠는 `_scripts/`에 있는 스크립트를 사용하여 각 저장소에서 자동으로 동기화됩니다.

### 콘텐츠 동기화

업스트림 저장소에서 최신 문서를 가져와 동기화하려면 다음 명령을 실행하세요:

```bash
# mini.nvim과 MiniMax 모두 동기화
make sync
```

각 구성 요소를 개별적으로 동기화할 수도 있습니다:

```bash
# mini.nvim만 동기화
make mini.nvim

# MiniMax만 동기화
make MiniMax
```

### 웹사이트 빌드

웹사이트는 Quarto를 사용하여 빌드됩니다. 로컬에서 사이트를 미리 보거나 렌더링하려면 [Quarto가 설치](https://quarto.org/docs/get-started/)되어 있어야 합니다.

```bash
# 로컬에서 웹사이트 미리보기
quarto preview

# 웹사이트 렌더링 (docs/ 디렉터리에 출력)
quarto render
```

## 기여하기

웹사이트에 대한 기여는 언제나 환영합니다! 문서에 문제가 있거나 개선 사항이 있다면 이슈를 열거나 풀 리퀘스트를 제출해 주세요.

참고로 `mini.nvim` 및 `MiniMax` 관련 문서는 각 해당 저장소에 직접 기여해야 합니다.

## 라이선스

이 저장소의 콘텐츠는 [MIT 라이선스](LICENSE)를 따릅니다.
