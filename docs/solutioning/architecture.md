# [Solutioning] Warvote 시스템 아키텍처 및 데이터 설계

## 1. 기술 스택 (Tech Stack)

*   **Frontend:** Next.js (관리자/활동가 대시보드 - 반응형 웹)
*   **Backend:** FastAPI (Python) - 텍스트 분석 및 데이터 처리에 최적화
*   **Database:** 
    *   **PostgreSQL:** 사용자, 활동가, 유권자 데이터 및 관계 관리
    *   **Redis:** 실시간 단축 URL 클릭 로깅 및 캐싱
*   **Analysis:** KoNLPy(한국어 자연어 처리), Scrapy/Selenium (커뮤니티 모니터링)
*   **External API:** 문자 발송 API (알리고/비즈메시지 등), Google Maps API, YouTube Data API

## 2. 데이터베이스 스키마 설계 (Key Tables)

### [CRM 관련]
*   **Users Table:** 관리자 및 활동가 정보 (아이디, 등급, 소속 조직)
*   **Voters Table:** 유권자/지인 프로파일링 (이름, 연락처, 연령대, 거주지, 관심사, 지지성향, **추천인_ID**)
*   **Messages Table:** 발송 메시지 이력 및 템플릿
*   **Click_Logs Table:** 단축 URL 클릭 기록 (유권자_ID, 메시지_ID, 클릭시각, IP, 기기정보)

### [인텔리전스 관련]
*   **Monitoring_Keywords Table:** 추적 대상 키워드 및 채널 리스트
*   **Buzz_Items Table:** 수집된 게시물/영상 데이터 (플랫폼, 원문 링크, 작성시간, 조회수, 감성수치)
*   **Issue_Flows Table:** 이슈 발생 및 확산 경로 로그

## 3. 핵심 로직 설계: Personalized Short URL 엔진

1.  **발송 요청:** 관리자가 메시지 발송 시 유권자 그룹 선택.
2.  **토큰 생성:** `Base62` 인코딩을 사용하여 `유권자_ID`와 `활동가_ID`가 포함된 고유 해시 토큰 생성.
3.  **단축 URL 매핑:** `warvo.te/x1y2z3` 형태의 단축 URL 생성 후 Redis/DB 저장.
4.  **리다이렉션 & 트래킹:** 유권자가 클릭 시, 시스템은 로그를 기록하고 원본 콘텐츠(유튜브 등)로 리다이렉트.

## 4. 인텔리전스 모니터링 파이프라인

1.  **Collection:** 주요 커뮤니티(뽐뿌, 클리앙, 개드립, 맘카페 등) 및 유튜브 API를 통한 정기적 수집.
2.  **Analysis:** 
    *   긍부정 판단 (Sentiment Analysis)
    *   언론 기사와의 키워드 매칭 (기사화 여부 확인)
3.  **Visualization:** 시간 흐름에 따른 플랫폼별 언급량 추이 및 이슈 전파 맵 생성.
