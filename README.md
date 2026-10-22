# 📦 Olist 브라질 이커머스 데이터 분석 & 대시보드

브라질 온라인 마켓플레이스 **Olist** 의 실제 주문 데이터(약 10만 건)를 pandas · plotly 로 탐색적 데이터 분석(EDA)하고,
분석 결과를 **Streamlit 대시보드**로 만들어 배포한 프로젝트입니다.

- **대시보드 바로 가기**: https://olist-ecommerce-sinaboro.streamlit.app
  (Streamlit Community Cloud 무료 배포 — 한동안 접속이 없으면 잠들어 있다가, 접속 후 버튼을 누르면 1분 안에 다시 켜집니다)

## 구성

```
├── app.py                  ← Streamlit 대시보드 (배포되는 앱)
├── requirements.txt        ← 배포 서버가 설치할 패키지
├── .streamlit/config.toml  ← 대시보드 테마
├── data/                   ← 대시보드용 가공 데이터 (원본에서 필요한 열만 추려 압축, 약 2.4MB)
│   ├── orders.csv.gz
│   └── items.csv.gz
└── notebooks/              ← 분석 노트북 (실행 결과 포함)
    ├── 01_데이터이해_고객_매출.ipynb
    ├── 02_시간패턴_카테고리_배송리뷰.ipynb
    └── 03_대시보드_만들기와_GitHub_배포.ipynb
```

| 노트북 | 내용 |
|---|---|
| 01 | 9개 테이블의 연결 구조(키), 분석 대상 정의, 고객 수 · 재구매율, 지역, 결제 수단, 객단가, 월별 매출 |
| 02 | 일 · 요일 · 시간 패턴, 공정한 기간 비교, 카테고리 판매량 vs 매출, 파레토, 배송 기간 · 지연율, 배송 지연과 리뷰 점수, 지역별 배송 |
| 03 | 배포용 데이터 가공 → `app.py` 작성 → 자동 테스트 → GitHub push → Streamlit Community Cloud 배포 |

## 주요 인사이트

| 영역 | 발견 |
|---|---|
| 고객 | 실제 고객 96,096명 중 **재구매율 약 3%**, 고객의 42% 가 상파울루(SP) |
| 매출 | 같은 1~8월 기준 1년 새 매출 **+143%**, 성장은 객단가가 아니라 **주문 수** 증가 덕분 |
| 시간 | 2017-11-24 블랙프라이데이 하루 1,100건+, 평일 낮 시간대에 주문 집중 |
| 카테고리 | 판매 수량 1위 bed_bath_table, 매출 1위 health_beauty, 상위 10개 카테고리가 매출의 62% |
| 배송 · 리뷰 | 배송 지연 시 평균 리뷰 **4.28 → 2.55점**, 성수기 지연율 14~21%, 북부 지역 배송 약 25일 |

## 실행 방법

### 대시보드
```bash
pip install -r requirements.txt
streamlit run app.py
```

### 분석 노트북
1. Kaggle 「Brazilian E-Commerce Public Dataset by Olist」 의 CSV 9개를 내려받아 저장소 최상위의 `00_data/` 폴더에 넣습니다.
2. `pip install pandas plotly jupyter` 후 `notebooks/` 의 노트북을 01 → 02 → 03 순서로 실행합니다.
   (03 노트북은 `notebooks/olist_dashboard/` 에 대시보드 파일을 만듭니다. 저장소 최상위의 `app.py` · `data/` 가 그 결과물입니다.)

## 데이터 출처 · 라이선스

Olist, *Brazilian E-Commerce Public Dataset by Olist* (Kaggle), **CC BY-NC-SA 4.0** (비영리 · 출처 표시 · 동일 조건 공유).
`data/` 의 파일은 이 데이터에서 대시보드에 필요한 열만 가공 · 압축한 것입니다. 교육용 프로젝트입니다.
