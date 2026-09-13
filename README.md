# 김경민 (Gyeongmin Kim)

**Data Engineer**

---

### 소개

**해온 일**
- 공공데이터 API 수집·정제 파이프라인 설계 (재난문자, 서울시 도시데이터)
- 외부 소스 2종 통합해 1,001건 데이터셋 구축
- 인파 혼잡도 지표 정의 및 모델 성능 측정·비교 검증
- FastAPI / Django 기반 백엔드 개발

**관심 분야**
- 서로 다른 소스의 데이터를 하나의 기준으로 맞추는 일
- 파이프라인이 깨지는 지점을 미리 나눠두는 설계

---

### Projects

| 프로젝트 | 한 줄 | 역할 | 성과 |
|---|---|---|---|
| **SAFY** <br/>재난·인파 안전 서비스 | 공공데이터 수집 파이프라인 + 인파 혼잡도 분석 | 팀장 · 데이터 · AI<br/>6명 팀 / 커밋 32 of 118 | **발표회 2위**<br/>(반 대표 선발 후 진출) |
| **[aemanbo](https://github.com/gangmom5272/aemanbo)** <br/>애니↔만화 이어보기 매핑 | 외부 소스 2종을 통합해 데이터셋 구축 | 백엔드 · 데이터셋<br/>2명 팀 / 커밋 36 of 42 | **프로젝트 1위**<br/>1,001건 × 39필드 구축 |

**SAFY** — 재난문자·서울시 도시데이터를 수집·정제하고, 영상에서 인파 혼잡도를 계산하는 서비스

- 외부 API 원본 모델과 내부 정규화 모델을 분리해, 외부 스펙 변경이 내부로 번지지 않게 설계
- 실패 경로를 5종으로 분리 (타임아웃 / HTTP / JSON 파싱 / 기관 오류코드 / 스키마 불일치)
- 혼잡도 지표를 직접 정의 (8×8 격자 64칸, 전체 C / 국소 2×2 L) 후 계산 근거를 이미지로 렌더링
- 전체 MAE 1.17을 시나리오별로 분해해 국소 밀집 구간만 2.33으로 튀는 것을 확인 → 고밀도 전용 모델 2종 비교 검증

**aemanbo** — 애니메이션을 다 본 사람에게 원작 만화를 몇 권 몇 화부터 이어 보면 되는지 알려주는 서비스

- 수집 → 보강 → 병합 → 번역 → 정규화 → 분류 → 적재를 9개 스크립트로 단계 분리
- 두 API의 식별 체계가 달라 생긴 매핑 실패를 필드별 완성도로 측정 (작품 메타 99~100% vs 이어보기 78.3%)
- LLM이 없는 작품을 생성하는 문제를 DB 실재 목록 내 선택으로 제한해 해결

---

### Tech

**프로젝트에 적용**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Django](https://img.shields.io/badge/Django-092E20?style=flat-square&logo=django&logoColor=white)
![Pydantic](https://img.shields.io/badge/Pydantic-E92063?style=flat-square&logo=pydantic&logoColor=white)
![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![GitLab CI](https://img.shields.io/badge/GitLab%20CI-FC6D26?style=flat-square&logo=gitlab&logoColor=white)
![Jira](https://img.shields.io/badge/Jira-0052CC?style=flat-square&logo=jira&logoColor=white)

**학습 중**

![Hadoop](https://img.shields.io/badge/Hadoop-66CCFF?style=flat-square&logo=apachehadoop&logoColor=black)
![Spark](https://img.shields.io/badge/Spark-E25A1C?style=flat-square&logo=apachespark&logoColor=white)
![Java](https://img.shields.io/badge/Java-437291?style=flat-square&logo=openjdk&logoColor=white)

**다뤄본 경험**
Vue 3 · React · OpenAI API · Nginx · YOLO11n

---

### Education

삼성 청년 SW 아카데미(SSAFY) 15기 · 2026.12 수료<br/>
한국외국어대학교 글로벌캠퍼스 프랑스학과 · 2026.02 졸업

---

### Contact

[![Gmail](https://img.shields.io/badge/gangmom5272@gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:gangmom5272@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/%EA%B2%BD%EB%AF%BC-%EA%B9%80-31774b426/)
