<div align="center">

# Planit

### **여행 일정과 날씨를 한 화면에서 관리하는 통합 여행 대시보드**

[![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-5-646CFF?style=flat-square&logo=vite)](https://vitejs.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3-06B6D4?style=flat-square&logo=tailwindcss)](https://tailwindcss.com/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104-009688?style=flat-square&logo=fastapi)](https://fastapi.tiangolo.com/)
[![MySQL](https://img.shields.io/badge/MySQL-8-4479A1?style=flat-square&logo=mysql&logoColor=white)](https://www.mysql.com/)

팀 GitHub: [NaYoung-ll/planit-projectmain](https://github.com/NaYoung-ll/planit-projectmain)

</div>

---

## 프로젝트 소개

**Planit**은 여행 일정 계획, 날씨 확인, 커뮤니티 후기 공유를 하나의 대시보드에서 관리할 수 있는 여행 플래너 웹 앱입니다.

- **프로젝트 기간**: 2025.09.29 ~ 2025.10.24 (3주)
- **팀 규모**: 6명
- **담당**: 프론트엔드 전체 뼈대 설계 + 프론트엔드 전반 가담 + 백엔드 API 연동/보완

> 본 저장소는 팀 프로젝트 Planit의 **개인 기여/구현 요약**입니다.

---

## What I Built (요약)

- **3단 레이아웃 설계**: React + Tailwind CSS 기반 대시보드 3단 그리드 레이아웃 구성 (사이드바/위젯 영역 포함 반응형)
- **CSS 마이그레이션**: 기존 CSS 12개를 Tailwind 유틸리티 기반으로 전환, 컬러/폰트 토큰으로 디자인 시스템 정리
- **공통 UI 컴포넌트 설계**: Button/Input/FormField/Card 등 재사용 가능한 6개 공통 컴포넌트 설계 및 구현
- **Custom Hooks 9개 설계**: useTrip(19개 함수), useAuth, useReview, useComment, useLike 등 비즈니스 로직 분리
- **여행 일정 CRUD**: 일정 생성/수정/삭제 화면, 도시/일자별 세부 일정 관리 UI, 체크리스트 CRUD 연동
- **커뮤니티**: 후기 작성/목록/상세 UI 구현, 이미지 업로드(FormData), 댓글/좋아요 기능 API 연동
- **날씨 위젯**: OpenWeather API 연동 위젯 구현, 상태별 UI(비/구름 등) 및 안내 배지/메시지 표시
- **미니 캘린더**: dayjs 기반 날짜/기간 선택 UI 구현, 일정 이벤트 표시 및 캘린더-일정 화면 연동
- **도시 검색**: 도시 검색 UI 구현(한/영 입력), 국가/도시 필터링 로직 적용 및 검색 API 연동
- **D-day 알림센터**: 알림 아이콘/리스트 구현, D-day 2일/1일 전 자동 알림 노출 + 클릭 시 상세 이동

---

## 핵심 기능

### 1) 3단 대시보드 레이아웃

- React + Tailwind CSS 기반 반응형 3단 그리드
- 좌측 사이드바(네비게이션) + 중앙 콘텐츠 + 우측 위젯(캘린더/날씨)
- Protected Route로 인증 기반 접근 제어

### 2) 여행 일정 관리 (CRUD)

- 3단계 생성 폼 (도시 선택 - 날짜 설정 - 일정 상세)
- 일자별 세부 일정 + 체크리스트 관리
- useTrip Hook 하나로 19개 API 함수 통합 관리

### 3) 커뮤니티 (후기/댓글/좋아요)

- 여행 후기 작성 시 이미지 업로드 (FormData)
- 댓글 CRUD + 좋아요 토글 기능
- 도시명 자동 매핑으로 후기 목록 보강

### 4) JWT 인증 + Axios 인터셉터

- JWT 기반 로그인/회원가입 플로우
- Axios 인터셉터로 모든 요청에 토큰 자동 주입
- 401 응답 시 자동 로그아웃 + 로그인 페이지 리다이렉트

### 5) 날씨 위젯 + 미니 캘린더

- OpenWeather API 실시간 날씨 데이터 연동
- 날씨 상태별 아이콘/배지 UI
- dayjs 기반 캘린더에서 일정 이벤트 표시 연동

---

## 아키텍처

```
                        Planit Frontend Architecture

    ┌──────────────┐     ┌──────────────────┐     ┌──────────────────────┐
    │   Browser    │     │   React Pages    │     │   Right Sidebar      │
    │              │────>│   (14개)          │     │   - Mini Calendar    │
    │              │     │                  │     │   - Weather Widget   │
    └──────────────┘     └────────┬─────────┘     └──────────────────────┘
                                  │
                                  ▼
                    ┌──────────────────────────┐
                    │    Custom Hooks (9개)     │
                    │  useTrip (19 functions)   │
                    │  useAuth, useReview ...   │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │    Axios Instance         │
                    │  Request: JWT 자동 주입    │
                    │  Response: 401 자동 처리   │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │    FastAPI Backend        │
                    │    (8 API Routers)        │
                    └────────────┬─────────────┘
                                 │
                    ┌────────────┼────────────┐
                    ▼            ▼            ▼
              ┌──────────┐ ┌──────────┐ ┌──────────────┐
              │  MySQL   │ │  bcrypt  │ │ OpenWeather  │
              │   DB     │ │  (Auth)  │ │    API       │
              └──────────┘ └──────────┘ └──────────────┘
```

### 데이터 흐름

```
User Action → React Page → Custom Hook → Axios (JWT Interceptor) → FastAPI → MySQL
```

---

## 기술 스택

| 분류             | 기술                               |
| ---------------- | ---------------------------------- |
| **Frontend**     | React 18, Vite 5                   |
| **Styling**      | Tailwind CSS 3                     |
| **HTTP Client**  | Axios (Interceptor)                |
| **Routing**      | React Router v6                    |
| **Date**         | dayjs                              |
| **Backend**      | FastAPI, Python                    |
| **Database**     | MySQL, SQLAlchemy (Async), Alembic |
| **Auth**         | JWT, bcrypt                        |
| **External API** | OpenWeather API                    |

---

## 프로젝트 구조

```
Planit/
├── src/
│   ├── components/          # 공통 UI 컴포넌트
│   │   ├── Layout.jsx       # 3단 레이아웃 (사이드바/네비/위젯)
│   │   ├── Button.jsx       # 공통 버튼
│   │   ├── Card.jsx         # 공통 카드
│   │   ├── Input.jsx        # 공통 인풋
│   │   ├── FormField.jsx    # 폼 필드 (라벨+인풋)
│   │   └── Protected.jsx    # 인증 보호 라우트
│   ├── hooks/               # Custom Hooks (9개)
│   │   ├── useTrip.jsx      # 여행 CRUD (19개 함수)
│   │   ├── useAuth.jsx      # 인증 (로그인/회원가입/프로필)
│   │   ├── useReview.jsx    # 리뷰 CRUD + 이미지 업로드
│   │   ├── useComment.jsx   # 댓글 CRUD
│   │   ├── useLike.jsx      # 좋아요 토글
│   │   ├── useWeather.jsx   # 날씨 API 연동
│   │   ├── useCity.jsx      # 도시 검색
│   │   ├── usePhoto.jsx     # 사진 관리
│   │   └── useEvent.jsx     # 일정 이벤트
│   ├── pages/               # 페이지 컴포넌트 (14개)
│   │   ├── Home.jsx         # 메인 (인기 여행지)
│   │   ├── Trips.jsx        # 여행 목록
│   │   ├── TripCreate.jsx   # 여행 생성 (3단계 폼)
│   │   ├── TripInfoEdit.jsx # 여행 상세 편집
│   │   ├── Community.jsx    # 커뮤니티 (리뷰/댓글/좋아요)
│   │   ├── Login.jsx        # 로그인
│   │   ├── Signup.jsx       # 회원가입
│   │   └── ...              # Profile, About 등
│   ├── services/
│   │   └── api.js           # Axios 인스턴스 (인터셉터)
│   ├── App.jsx              # 라우팅 설정
│   └── main.jsx             # 엔트리포인트
├── backend/
│   └── app/
│       ├── routers/         # API 라우터 (8개)
│       ├── db/              # 모델/스키마/CRUD (14개 모델)
│       ├── services/        # 비즈니스 로직 (7개)
│       └── main.py          # FastAPI 앱 설정
├── tailwind.config.js       # Tailwind 설정 (색상/폰트 토큰)
├── package.json
└── vite.config.js
```

---

## 실행 방법

### 프론트엔드

```bash
# 1. 저장소 클론
git clone https://github.com/NaYoung-ll/planit-projectmain.git
cd Planit

# 2. 의존성 설치
npm install

# 3. 개발 서버 실행
npm run dev

# 4. 접속
# http://localhost:5173
```

### 백엔드

```bash
# 1. 가상환경 생성 및 활성화
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 2. 의존성 설치
pip install -r requirements.txt

# 3. 서버 실행
uvicorn app.main:app --reload --port 8000

# 4. API 문서
# http://localhost:8000/docs
```

---

## 주요 성과

- **프론트엔드 14개 페이지 + 9개 Custom Hooks 설계**: 컴포넌트/훅 분리 아키텍처로 유지보수성 확보
- **CSS 12개 -> Tailwind 1개로 통합**: 유틸리티 기반 마이그레이션으로 스타일 충돌 제거
- **Axios 인터셉터 인증 자동화**: JWT 토큰 주입 + 401 자동 처리로 인증 플로우 안정화
- **백엔드 API 부족분 직접 구현**: 프론트-백엔드 병목 해소로 팀 프로젝트 일정 지연 방지

---

## 프로젝트 기간

**2025.09.29 ~ 2025.10.24 (3주)**

---

본 저장소는 포트폴리오 요약용 README입니다.
전체 프로젝트 코드는 [팀 GitHub](https://github.com/NaYoung-ll/planit-projectmain)에서 확인 가능합니다.
