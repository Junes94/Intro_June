## 김개발 포트폴리오 (정적 웹사이트)

간단한 정적 웹 포트폴리오입니다. `HTML + CSS + JavaScript`만으로 구현되어 별도 빌드 과정이나 서버 없이도 동작합니다. 생명과학 전공자도 쉽게 이해하고 수정할 수 있도록 구조와 작동 원리를 친절히 설명합니다.

### 미리보기/실행
- 방법 1: 파일 탐색기에서 `index.html` 더블클릭 (로컬 파일로 열기)
- 방법 2: VS Code 확장 프로그램 “Live Server”로 `index.html` 실행
- 방법 3: 간단 배포 후 브라우저에서 접속 (GitHub Pages, Netlify, Vercel 등)

### 폴더 구조
```
vibe_exercise/
├─ index.html   # 페이지 뼈대(구조/콘텐츠)
├─ style.css    # 스타일(색, 폰트, 레이아웃, 반응형)
└─ script.js    # 상호작용(메뉴, 스크롤, 애니메이션, 폼 유효성)
```

### 주요 섹션과 기능 개요
- 헤더/네비게이션: 상단 고정, 모바일 햄버거 메뉴, 현재 섹션 하이라이트
- 홈(Hero): 이름, 다국어 타이핑 효과(영/한), 강조 버튼, 간단 프로필 아이콘
- 소개(About): 경력 요약, 통계 카드(년수/프로젝트/만족도)
- 기술(Skills): 스킬 바(progress bar) 애니메이션(IntersectionObserver)
- 경력(Experience): 타임라인 UI(좌/우 교차 배치, 반응형 시 세로)
- 프로젝트(Projects): 카드형 목록(호버 상승, 기술 태그, 링크 버튼)
- 연락처(Contact): 정보 카드 + 문의 폼(프론트 단 유효성 검사)
- 푸터(Footer): 저작권 표시

### 기술 스택
- HTML5 시맨틱 섹션 구조
- CSS3: 그리드/플렉스, 그라디언트, 그림자, 반응형 미디어쿼리
- JavaScript(바닐라): 메뉴 토글, 스무스 스크롤, 타이핑/스크롤 애니메이션, 폼 검사

### 파일별 설명
- `index.html`
  - 네비게이션(`.nav-menu`, `.hamburger`)과 각 섹션(`#home`, `#about`, `#skills`, `#experience`, `#projects`, `#contact`)으로 구성
  - 홈 섹션의 타이핑 대상 요소: `.typing-text` + `data-texts` 속성에 문구 배열(JSON 문자열)
  - 마지막에 `script.js` 로드

- `style.css`
  - 전체 타이포/색/레이아웃 정의
  - 헤더 고정, 링크 호버 밑줄 애니메이션, Hero 그라디언트 배경, 텍스트 그라디언트
  - 스킬 바 애니메이션(`.skill-progress.animate`)과 다양한 섹션 카드/타임라인 스타일
  - 반응형: 768px, 480px 기준으로 그리드 → 단일 컬럼 전환, 모바일 메뉴 슬라이드

- `script.js`
  - DOM 로드 후 실행. 핵심 로직:
    - 모바일 메뉴 토글(`.hamburger`, `.nav-menu.active`)
    - 네비 링크 클릭 시 헤더 높이 보정한 스무스 스크롤
    - 스크롤 시 헤더 배경/그림자 변화
    - 스킬 바: IntersectionObserver로 뷰포트 진입 시 `data-width`만큼 채우기(+ CSS 애니메이션)
    - 현재 스크롤 위치에 따라 활성 네비 링크 업데이트
    - 연락처 폼 유효성 검사(필수값, 이메일 형식). 현재는 서버 전송 없이 알림만 표시
    - 타이핑 효과: 단일(`typeWriter`) + 다중 순환(`multiTypeWriter`)
    - 스크롤 등장 애니메이션(타임라인/프로젝트/스킬 섹션 요소에 opacity/translate 적용)
    - ESC/외부 클릭/리사이즈 시 모바일 메뉴 닫기, 초기 페이드인, 스크롤 핸들러 최적화(throttle)

### 커스터마이징 가이드
- 이름/문구 변경: `index.html`의 Hero `.hero-title`, `.hero-name`, 소개/경력/프로젝트 텍스트 수정
- 타이핑 문구 교체: `index.html`의 `.typing-text`의 `data-texts` JSON 배열 편집
- 스킬 퍼센트 수정: `index.html`에서 각 `.skill-progress`의 `data-width="90%"` 등 변경
- 색상/테마 변경: `style.css`의 기본 색(`[#3498db]`, `[#2c3e50]` 등)과 그라디언트 조정
- 프로젝트 카드 추가: `#projects` 내 `.projects-grid`에 `.project-card` 블록 복제/수정
- 연락처 정보/링크 교체: `#contact`의 이메일/전화/소셜 링크 텍스트, href 수정

### 접근성/사용성 체크리스트
- 링크 텍스트는 명확하게: “프로젝트 보기”, “GitHub” 등 의미 있는 라벨 유지
- 대비 비율 확인: 배경 그라디언트 위의 텍스트 가독성 검사
- 키보드 사용성: ESC로 메뉴 닫힘 지원, 포커스 스타일 필요 시 CSS 추가 고려
- 시맨틱 구조: 섹션 `id`와 제목 계층 유지. 이미지에는 대체 텍스트(현재 이모지 placeholder)

### 성능 메모
- 스크롤·리사이즈 핸들러에 throttle 적용(기본 16ms)
- IntersectionObserver로 필요 시에만 스킬 애니메이션 실행
- 외부 의존성 없음(폰트 제외): 초기 로드가 가벼움

### 한계/주의사항
- 폼 제출은 데모 수준(알림 후 reset). 실제 전송은 백엔드 또는 서비스(SendGrid/Formspree 등) 연동 필요
- 애니메이션이 많은 구간에서 저사양 기기 성능 저하 가능 → transition 시간/요소 수 조절

### 로컬 개발 팁
```bash
# VS Code Live Server 사용 시 (권장)
# index.html을 열고, 우클릭 → Open with Live Server
```

윈도우에서는 파일을 더블클릭해도 열리지만, 파일 프로토콜에서는 일부 브라우저 기능 차이가 있을 수 있어 Live Server가 더 안정적입니다.

### 배포(정적 호스팅)
- GitHub Pages: 레포지토리에 push → Pages 활성화(브랜치: main, 폴더: root)
- Netlify/Vercel: 레포 연결 후 루트 디렉터리 그대로 배포(빌드 스텝 없음)

### 브라우저 호환성
- 최신 크롬/엣지/파이어폭스/사파리에서 동작. `backdrop-filter` 등 일부 효과는 구형 브라우저에서 제한될 수 있음

### 라이선스
- 개인 포트폴리오용. 별도 라이선스 명시 없으며, 상업적 재사용 시 원저자 표시를 권장합니다.

### 변경 이력(요약)
- 초기 버전: 네비/타이핑/스킬바/타임라인/프로젝트/폼/애니메이션 포함
