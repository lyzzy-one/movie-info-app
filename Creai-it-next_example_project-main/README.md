🎬 Movie Info App

개인 실습 프로젝트로, Next.js(App Router) + Redis 기반의 간단한 영화 정보 웹 애플리케이션입니다.
학회 세션 예제 코드를 바탕으로, 전체 구조를 직접 분석하고 서비스 형태로 재구성했습니다.

목표: Next.js의 폴더 기반 라우팅 구조와 API 라우트, Redis 데이터 캐싱 구조를 이해하고
프론트엔드에서의 데이터 흐름을 실제 서비스 형태로 설계하는 것

1) 영화 목록 페이지: /
API로부터 영화 목록을 불러와 카드 형태로 표시

제목/장르/년도 기반 실시간 검색 가능

2) 영화 상세 페이지: /movies/[id]

개별 영화의 상세 정보(제목, 장르, 평점, 줄거리) 표시

URL 동적 라우팅(app/movies/[id]/page.tsx) 기반으로 구성

3) API 라우트: /api/movies

GET 요청 시 영화 목록 또는 특정 영화 정보를 반환

Redis 연결 시, 데이터가 캐싱되어 빠르게 조회 가능

Redis가 없을 경우 기본 Mock 데이터(Fallback) 사용

4) 데이터 캐싱:

lib/redis.ts를 통해 Redis 클라이언트를 관리

scripts/init-movies.ts를 통해 초기 데이터 시드 가능

movie-info-app/
├── app/
│   ├── layout.tsx        # 전체 공통 레이아웃 (헤더, 네비게이션 등)
│   ├── globals.css       # 전역 스타일 시트
│   ├── page.tsx          # 메인 페이지 (영화 목록)
│   ├── movies/
│   │   └── [id]/page.tsx # 영화 상세 페이지 (동적 라우팅)
│   └── api/
│       └── movies/route.ts # 영화 데이터 API (Redis 연동)
│
├── lib/
│   └── redis.ts          # Redis 클라이언트 설정
│
├── scripts/
│   └── init-movies.ts    # Redis 초기 시드 스크립트
│
├── public/
│   └── placeholder.jpg   # 포스터 기본 이미지
│
├── package.json          # 프로젝트 의존성 및 스크립트 정의
└── tsconfig.json         # TypeScript 설정
