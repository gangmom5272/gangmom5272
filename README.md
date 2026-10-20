# 김경민 (Gyeongmin Kim)

**Data Engineer**

---

### Projects

| 프로젝트 | 한 줄 소개 | 역할 | 성과 |
|---|---|---|---|
| **[ThisPatch](https://github.com/gangmom5272/thispatch)** | 스팀 리뷰 1억 7,100만 건을 분산 처리해 게임 개발사가 패치 반응을 진단하고 다음 패치를 기획할 수 있게 돕는 서비스 | 팀장 · 데이터 · 인프라 | |
| **[SAFY](https://github.com/gangmom5272/safy)** | 군중 밀집 위험을 실시간으로 파악하고 대응해 사고 예방에 도움을 주는 서비스 | 팀장 · 데이터 · AI | **우수상**<br/> |
| **[aemanbo](https://github.com/gangmom5272/aemanbo)** | 애니메이션과 원작 만화의 연결 지점을 찾아, 이어보기를 바로 시작할 수 있게 도와주는 서비스 | 팀장 · 백엔드 · 데이터셋 구축 | **최우수상**<br/> |

**ThisPatch** — 수집부터 서비스 DB 적재까지 데이터 파이프라인 전 구간과 온프레미스 클러스터를 담당

- 제공받은 클라우드 인스턴스가 포트 제약으로 노드 간 통신이 불가능해, 물리 머신 5대(Master 1 · Worker 4)로 **Hadoop / YARN / Spark 클러스터를 직접 구축** (HDFS 4.92TB, 복제 계수 3). 설치·운영 스크립트 24종 작성, systemd 데몬화
- Spring Batch 원격 파티셔닝 + RabbitMQ 분산 수집기로 **스팀 리뷰 1억 7,100만 건 / 게임 11.7만 개 / 공지 197만 건** 수집
- 처리량이 초당 425건에 그쳐 전량 수집에 4~9일이 걸릴 상황에서, 외부 응답·HDFS 쓰기·DB 커밋을 구간별로 측정했으나 한 페이지 8.3초가 설명되지 않음 → 코드 내부 계측으로 병목 3개를 특정해 **초당 2,540건(약 6배, 피크 3,090)**
- 5시간 40분 실행 후 실패가 반복되던 1.7억 행 Spark 집계를 **52분 완주**로 전환. 원인은 두 가지였고, (1) 1억 7,140만 행 중 **2행**이 수정시각 < 생성시각인데 집계기가 전체를 거부하는 구조, (2) 이벤트 로그 분석 결과 executor 64개 중 62개가 메모리 부족 종료 → 검증 실패 행을 이유별로 기록 후 제외(0.5% 초과 시 중단), 7개 칼럼만 디스크 보관·shuffle 파티션 240 고정·AQE 병합 해제
- AppID 18만 개 조인에 Broadcast Hash Join 적용 **17분 → 3.5분**. daily_stat 1,833만 행 전체 스캔을 AppID 인덱스로 해소
- 증분 수집 기준 시각 공백으로 **오류 없이 누락된 1,015개 게임**을 시연 준비 중 발견. 원인 특정 후 시연 대상 15개를 표적 재수집했고, 기준 시각 산정 방식 수정은 과제로 남김
- YARN이 `SUCCEEDED`로 표시한 작업도 드라이버 예외가 반영되지 않음을 확인하고, 성공 판정을 **"읽은 행 수 == DB 적재 행 수"**로 변경
- Spark 집계 결과를 서비스 DB 10개 표에 FK 순서로 적재. 드라이버 단일 트랜잭션 교체로 실패 시 이전 값이 보존되도록 설계
- NameNode 메타데이터 백업본만으로 복구 훈련을 수행해 23개 표의 행 수·스키마 일치 검증

**SAFY** — 팀 프로젝트의 `data/`(수집·정제 서버)와 `ai/`(분석 서버)를 담당

- 공공데이터 API 3종(재난문자·서울시 혼잡도·서울시 행사) 수집 파이프라인 설계. 외부 원본 모델과 내부 정규화 모델을 분리해 외부 스펙 변경이 내부로 번지지 않게 함
- 실패 경로를 5종으로 분리 (타임아웃 / HTTP / JSON 파싱 / 기관 오류코드 / 스키마 불일치)
- 혼잡도 지표 C·L을 직접 정의(8×8 격자)하고 제보 단위 위험도 공식을 설계
- YOLO 성능을 시나리오별로 분해해 고밀도 구간의 과소 탐지를 확인 → **P2PNet을 SAFY 환경에 맞게 미세 조정**
- 미세 조정용 **머리 좌표 데이터셋 4,395장 구축** (JHU-CROWD++ 4,344 + 사용 동의를 받은 팀 사진 51장 수동 라벨링, 머리 좌표 약 150만 개)
- 독립 홀드아웃 검증에서 고밀도 표본 1,154장 기준 **Count MAE 425.18 → 121.84**, C MAE 44.15 → 5.55 개선
- 다만 P2PNet은 질감이 복잡한 저밀도 장면에서 배경을 사람으로 세는 오탐이 커, 한쪽을 고르는 문제가 아니라고 판단 → 두 모델을 모든 정상 프레임에서 함께 실행하고 **오탐 게이트**로 결과를 분기하는 구조 설계
- 게이트 조건은 P2PNet이 출력하는 점 중 확률 0.5~0.6 구간이 전체의 **15% 이상**이면 저밀도 오탐으로 보고 YOLO11n 값만 사용, 미발동 시 두 혼잡도 중 큰 값으로 상향 보정. 공식 인원수는 어느 경우에도 YOLO11n이 담당
- 임계값 15%는 대형 오탐 23건과 정상 21건을 직접 분류해 튜닝 (**정확도 81.8% / 재현율 82.6%**). 표본이 44건으로 작아 운영 데이터 축적 후 재조정이 필요하다는 점을 코드 주석에 명시
- 운영 서버 실측 **평균 지연 57ms / P95 69ms / 17.4 FPS**, 546회 연속 요청 실패 0건
- 기술 검증 문서 31종, 테스트 83종 작성

**aemanbo**

- 수집 → 보강 → 병합 → 번역 → 정규화 → 분류 → 적재를 9개 스크립트로 단계 분리해 1,001건 × 39필드 데이터셋 구축
- 두 API의 식별 체계가 달라, 1,001건 중 이어보기 지점은 892건까지만 확보 (작품 메타데이터는 99~100%)
- LLM이 없는 작품을 생성하는 문제를 DB 실재 목록 내 선택으로 제한해 해결

---

### Tech

**Language**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white) ![Java](https://img.shields.io/badge/Java-437291?style=flat-square&logo=openjdk&logoColor=white)

**Data**

![Hadoop](https://img.shields.io/badge/Hadoop-66CCFF?style=flat-square&logo=apachehadoop&logoColor=black) ![Spark](https://img.shields.io/badge/Spark-E25A1C?style=flat-square&logo=apachespark&logoColor=white) ![Parquet](https://img.shields.io/badge/Parquet-50ABF1?style=flat-square&logo=apacheparquet&logoColor=white) ![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat-square&logo=rabbitmq&logoColor=white)

**Backend**

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![Django](https://img.shields.io/badge/Django-092E20?style=flat-square&logo=django&logoColor=white) ![Spring Batch](https://img.shields.io/badge/Spring%20Batch-6DB33F?style=flat-square&logo=springboot&logoColor=white) ![Pydantic](https://img.shields.io/badge/Pydantic-E92063?style=flat-square&logo=pydantic&logoColor=white) ![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white)

**Database**

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white) ![pgvector](https://img.shields.io/badge/pgvector-4169E1?style=flat-square)

**ML**

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![YOLO11n](https://img.shields.io/badge/YOLO11n-042AFF?style=flat-square&logo=ultralytics&logoColor=white) ![P2PNet](https://img.shields.io/badge/P2PNet-5B21B6?style=flat-square) ![OpenAI API](https://img.shields.io/badge/OpenAI%20API-412991?style=flat-square)

**Infra & CI**

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=flat-square&logo=jenkins&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white) ![AWS EC2](https://img.shields.io/badge/AWS%20EC2-FF9900?style=flat-square&logo=amazonec2&logoColor=white) ![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)

**Tools**

![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white) ![Jira](https://img.shields.io/badge/Jira-0052CC?style=flat-square&logo=jira&logoColor=white)


### Education

삼성 청년 SW 아카데미(SSAFY) 15기 · 2026.12 수료<br/>
한국외국어대학교 글로벌캠퍼스 프랑스학과 · 2026.02 졸업

---

### Contact

[![Gmail](https://img.shields.io/badge/gangmom5272@gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:gangmom5272@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/%EA%B2%BD%EB%AF%BC-%EA%B9%80-31774b426/)
