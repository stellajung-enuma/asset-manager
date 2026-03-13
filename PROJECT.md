# IT 자산관리 시스템 — 프로젝트 정리

## 저장소 정보

| 항목 | 내용 |
|------|------|
| **GitHub 저장소** | https://github.com/stellajung-enuma/asset-manager |
| **Clone URL** | https://github.com/stellajung-enuma/asset-manager.git |
| **GitHub Pages URL** | https://stellajung-enuma.github.io/asset-manager/ |
| **브랜치** | `master` |
| **로컬 경로** | `C:\Users\hanji\Documents\Claude 테스트\` |

---

## 기술 스택

- **프론트엔드**: 순수 HTML + CSS + JavaScript (빌드 도구 없음)
- **데이터 저장**: LocalStorage (브라우저 내 영속)
- **외부 의존성**: 없음 — 오프라인에서도 동작
- **로컬 서버**: PowerShell HttpListener (`serve.ps1`)

> Node.js/npm이 설치되어 있지 않아 단일 HTML 파일로 구현함

---

## 파일 구조

```
Claude 테스트/
├── index.html          # 메인 앱 (전체 UI + 로직 포함)
├── serve.ps1           # 로컬 개발 서버 (PowerShell)
├── .gitignore
├── PROJECT.md          # 이 파일
└── .claude/
    ├── launch.json     # preview_start 서버 설정
    └── plans/
        └── concurrent-crafting-hennessy.md  # 구현 계획서
```

---

## 구현된 기능

### 대시보드
- 전체 / 사용중 / 미사용 / 수리중 통계 카드
- 유형별(노트북/태블릿) CSS 막대 차트
- 상태별 CSS 막대 차트
- 최근 등록 자산 5개 미리보기

### 자산 목록
- **전체 / 노트북 / 태블릿** 탭 분리
- 검색: 모델명, 브랜드, 시리얼번호, 담당자, 부서
- 필터: 유형, 상태
- 컬럼: 자산번호, 유형, 브랜드, 모델명, 시리얼번호, 상태, 담당자, 부서, 구매일

### 자산 CRUD
- 추가 / 수정 모달 (유형, 상태, 브랜드, 모델명, 시리얼번호, 담당자, 부서, 구매일, 가격, 메모)
- 삭제 확인 다이얼로그
- 시리얼번호 중복 검사
- Toast 알림

### 샘플 데이터 (첫 실행 시 자동 로드)
- 노트북 5개: Samsung Galaxy Book3 Pro, LG 그램 16, Apple MacBook Pro 14", Dell XPS 15, Samsung Galaxy Book3
- 태블릿 5개: Apple iPad Pro 12.9", Samsung Galaxy Tab S9, Apple iPad Air 5th, Microsoft Surface Pro 9, Samsung Galaxy Tab S8+

---

## 자산 데이터 모델

```js
{
  id: "ASSET-001",           // 자동 생성 (ASSET-NNN 형식)
  type: "노트북" | "태블릿",
  brand: "Samsung",
  model: "Galaxy Book3 Pro",
  serial: "SN-2023-NB-001",
  status: "사용중" | "미사용" | "수리중",
  assignee: "홍길동",
  department: "개발팀",
  purchaseDate: "2023-03-15",
  price: 1800000,
  memo: "충전기 포함",
  createdAt: "2023-03-15"
}
```

---

## 로컬 실행 방법

### 방법 1 — 파일 직접 열기 (가장 간단)
```
index.html 파일을 브라우저에서 더블클릭
```

### 방법 2 — 로컬 서버 실행
```powershell
powershell -ExecutionPolicy Bypass -File serve.ps1
# → http://localhost:5500 에서 접속
```

### 방법 3 — Claude Code preview_start
`.claude/launch.json` 설정 완료 (`autoPort: true`)
```
preview_start "asset-manager"
```

---

## Git 커밋 히스토리

| 커밋 | 설명 |
|------|------|
| `870a21e` | Revert to original version (노트북/태블릿 only) ← **현재** |
| `87078e2` | Add category expansion, QR codes, and software license management |
| `83da704` | Add IT asset management web app (최초 버전) |

> `87078e2` 커밋에 카테고리 확장 + QR코드 + 소프트웨어 라이선스 기능이 구현되어 있음
> 사용자 피드백으로 현재는 revert된 상태

---

## 다음 작업 계획 (우선순위 순)

1. **② 자산 유형 확장** — PC, 태블릿, 책상, 의자, 수납장, 책장 등 IT 사무실 전 실물 자산으로 확장 (대분류/소분류 구조)
2. **① QR 코드 생성 & 인쇄** — 각 자산에 QR 코드 부착용 출력 기능
3. **③ 소프트웨어 라이선스 관리** — 라이선스 키, 좌석 수, 만료일, 만료 임박 경고

---

## 참고 사항

- `serve.ps1`은 `$env:PORT` 환경변수로 포트를 받도록 설정 (`autoPort` 지원)
- LocalStorage 키: `it_assets_v1`
- GitHub Pages 배포: `master` 브랜치 루트 기준 (`index.html`)
