# 김경민 (Gyeongmin Kim)

**Data Engineer**

---

### Projects

| 프로젝트 | 한 줄 소개 | 역할 | 성과 |
|---|---|---|---|
| **SAFY** | 군중 밀집 위험을 실시간으로 파악하고 대응해 사고 예방에 도움을 주는 서비스 | 팀장 · 데이터 · AI | **2위** |
| **[aemanbo](https://github.com/gangmom5272/aemanbo)** | 애니메이션과 원작 만화의 연결 지점을 찾아, 이어보기를 바로 시작할 수 있게 도와주는 서비스 | 팀장 · 백엔드 · 데이터셋 구축 | **1위** |

**SAFY**

- 외부 API 원본 모델과 내부 정규화 모델을 분리해, 외부 스펙 변경이 내부로 번지지 않게 설계
- 실패 경로를 5종으로 분리 (타임아웃 / HTTP / JSON 파싱 / 기관 오류코드 / 스키마 불일치)
- 혼잡도 지표를 직접 정의 (8×8 격자 64칸, 전체 C / 국소 2×2 L) 후 계산 근거를 이미지로 렌더링
- 전체 MAE 1.17을 시나리오별로 분해해 국소 밀집 구간만 2.33으로 튀는 것을 확인 → 고밀도 전용 모델 P2PNet·DM-Count 비교 검증

**aemanbo**

- 수집 → 보강 → 병합 → 번역 → 정규화 → 분류 → 적재를 9개 스크립트로 단계 분리해 1,001건 × 39필드 데이터셋 구축
- 두 API의 식별 체계가 달라, 1,001건 중 이어보기 지점은 892건까지만 확보 (작품 메타데이터는 99~100%)
- LLM이 없는 작품을 생성하는 문제를 DB 실재 목록 내 선택으로 제한해 해결

---

### Tech

**Language**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)

**Backend**

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![Django](https://img.shields.io/badge/Django-092E20?style=flat-square&logo=django&logoColor=white) ![Pydantic](https://img.shields.io/badge/Pydantic-E92063?style=flat-square&logo=pydantic&logoColor=white) ![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white)

**Database**

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white) ![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)

**ML**

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![YOLO11n](https://img.shields.io/badge/YOLO11n-042AFF?style=flat-square&logo=ultralytics&logoColor=white) ![OpenAI API](https://img.shields.io/badge/OpenAI%20API-412991?style=flat-square)

**Infra & CI**

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=flat-square&logo=jenkins&logoColor=white) ![GitLab CI](https://img.shields.io/badge/GitLab%20CI-FC6D26?style=flat-square&logo=gitlab&logoColor=white)

**Tools**

![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white) ![Jira](https://img.shields.io/badge/Jira-0052CC?style=flat-square&logo=jira&logoColor=white)

**Learning**

![Hadoop](https://img.shields.io/badge/Hadoop-66CCFF?style=flat-square&logo=apachehadoop&logoColor=black) ![Spark](https://img.shields.io/badge/Spark-E25A1C?style=flat-square&logo=apachespark&logoColor=white) ![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black) ![Java](https://img.shields.io/badge/Java-437291?style=flat-square&logo=openjdk&logoColor=white)

### Education

삼성 청년 SW 아카데미(SSAFY) 15기 · 2026.12 수료<br/>
한국외국어대학교 글로벌캠퍼스 프랑스학과 · 2026.02 졸업

---

### Contact

[![Gmail](https://img.shields.io/badge/gangmom5272@gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:gangmom5272@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/%EA%B2%BD%EB%AF%BC-%EA%B9%80-31774b426/)
