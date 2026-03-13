# Claude 프로젝트 지침

## 언어
- 모든 답변은 **한국어**로 작성한다.
- 코드 주석도 한국어로 작성한다.
- 변수명·함수명은 영어(camelCase)를 유지하되, 설명은 한국어로 한다.

---

## 개발 방식: Test-Driven Development (TDD)

### 원칙
1. **Red** — 실패하는 테스트를 먼저 작성한다.
2. **Green** — 테스트를 통과하는 최소한의 코드를 작성한다.
3. **Refactor** — 테스트가 통과된 상태에서 코드를 개선한다.

### 규칙
- 새 기능을 구현하기 전에 반드시 테스트 케이스를 먼저 작성한다.
- 테스트 없이 기능 코드를 작성하지 않는다.
- 각 함수/모듈은 단독으로 테스트 가능하도록 설계한다.
- 테스트 파일 위치: 기능 파일과 동일한 디렉토리, `*.test.js` 또는 `*.spec.js` 형식.

### 현재 프로젝트 적용 방법
이 프로젝트는 단일 HTML 파일(빌드 도구 없음)이므로 테스트는 다음 방식으로 작성한다:
- 순수 로직 함수(필터, 정렬, ID 생성, 유효성 검사 등)는 별도 `*.test.js` 파일에 테스트 작성
- 브라우저 없이 실행 가능한 테스트는 Node.js 설치 없이도 동작하는 방식으로 작성
- UI 변경 시 영향받는 로직의 테스트를 먼저 업데이트한다.

---

## 프로젝트 컨텍스트

프로젝트 전체 현황은 [`PROJECT.md`](./PROJECT.md)를 참고한다.

### 핵심 정보 요약
- **GitHub**: https://github.com/stellajung-enuma/asset-manager
- **GitHub Pages**: https://stellajung-enuma.github.io/asset-manager/
- **로컬 경로**: `C:\Users\hanji\Documents\Claude 테스트\`
- **기술 스택**: 순수 HTML + CSS + JavaScript, LocalStorage
- **브랜치**: `master`

### 다음 작업 우선순위
1. 자산 유형 확장 (IT기기·가구·소모품 대분류 + 소분류)
2. QR 코드 생성 & 인쇄
3. 소프트웨어 라이선스 관리

---

## 코드 스타일

- 들여쓰기: 스페이스 2칸
- 문자열: 작은따옴표(`'`) 사용
- 함수 선언: `function` 키워드 사용 (화살표 함수는 콜백에서만)
- 변경 후 반드시 `git commit` + `git push` 하여 GitHub Pages에 반영한다.
