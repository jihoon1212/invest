# Stock Regression Learning Project

주식 시장 데이터를 수집하고 기술적 지표를 생성한 뒤, 여러 회귀모델을 적용하여 분석 결과를 비교·시각화한 **Python 머신러닝 학습 프로젝트**입니다.

이 프로젝트는 Python 데이터 처리, 회귀분석, 모델 평가 및 Streamlit 대시보드 구현 과정을 학습하기 위해 제작했습니다.

---

## 1. 프로젝트 목적

이 프로젝트의 주요 목적은 다음과 같습니다.

* `yfinance`를 활용한 주식 시세 데이터 수집
* 주가·거래량 데이터를 이용한 파생변수 생성
* 여러 선형 회귀모델의 학습 및 성능 비교
* 실제값과 모델 추정값 시각화
* Streamlit 기반 분석 대시보드 구현
* 머신러닝 분석 과정을 하나의 프로그램으로 구성

---

## 2. 주요 기능

### 주식 데이터 수집

사용자가 입력한 종목 코드와 기간을 기준으로 다음 데이터를 수집합니다.

* 시가: `Open`
* 고가: `High`
* 저가: `Low`
* 종가: `Close`
* 거래량: `Volume`

미국 주식 종목 코드를 기준으로 사용할 수 있습니다.

예시:

* Apple: `AAPL`
* Microsoft: `MSFT`
* Google: `GOOGL`
* Tesla: `TSLA`
* Amazon: `AMZN`

### 기술적 지표 생성

수집한 데이터를 바탕으로 다음 변수를 생성합니다.

* 5일·20일·60일 이동평균
* RSI
* 볼린저 밴드
* 거래량 이동평균
* 일별 수익률
* 수익률 이동평균
* 변동성

### 회귀모델 비교

다음 모델을 선택하여 학습할 수 있습니다.

* Linear Regression
* Ridge Regression
* Lasso Regression
* ElasticNet

### 모델 평가

다음 지표를 이용하여 모델 결과를 평가합니다.

* MSE
* RMSE
* MAE
* MAPE
* R²
* Explained Variance

### 결과 시각화

* 실제값과 모델 추정값 비교
* 잔차 분석
* 회귀계수 절대값 기반 특성 중요도
* 평가 결과 CSV 저장
* 분석 결과 이미지 저장
* Streamlit 대시보드 제공

---

## 3. 기술 스택

* Python
* pandas
* NumPy
* scikit-learn
* yfinance
* Matplotlib
* Seaborn
* Plotly
* Streamlit

---

## 4. 프로젝트 구조

```text
invest/
├── data_loader.py
├── stock_regression.py
├── dashboard.py
├── requirements.txt
├── results/
└── README.md
```

### 주요 파일

| 파일                    | 설명                         |
| --------------------- | -------------------------- |
| `data_loader.py`      | yfinance 데이터 수집 및 전처리      |
| `stock_regression.py` | 파생변수 생성, 모델 학습, 평가 및 결과 저장 |
| `dashboard.py`        | Streamlit 기반 분석 대시보드       |
| `requirements.txt`    | 프로젝트 실행에 필요한 라이브러리 목록      |
| `results/`            | 평가 결과와 그래프 저장 폴더           |

---

## 5. 설치 방법

저장소를 복제합니다.

```bash
git clone https://github.com/jihoon1212/invest.git
cd invest
```

가상환경을 생성하고 활성화합니다.

```bash
python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

필요한 라이브러리를 설치합니다.

```bash
pip install -r requirements.txt
```

---

## 6. 실행 방법

### 명령줄에서 모델 실행

```bash
python stock_regression.py --symbol AAPL
```

Ridge 모델 실행 예시:

```bash
python stock_regression.py \
  --symbol AAPL \
  --model ridge \
  --alpha 1.0 \
  --test-size 0.2 \
  --save-plots
```

Windows PowerShell에서는 한 줄로 실행할 수 있습니다.

```bash
python stock_regression.py --symbol AAPL --model ridge --alpha 1.0 --test-size 0.2 --save-plots
```

### Streamlit 대시보드 실행

```bash
streamlit run dashboard.py
```

대시보드에서 다음 항목을 선택할 수 있습니다.

* 분석 종목
* 데이터 수집 기간
* 회귀모델
* 정규화 강도
* 테스트 데이터 비율

---

## 7. 현재 모델의 해석과 한계

현재 모델은 당일 가격과 기술적 지표를 입력변수로 사용하여 종가를 추정합니다.

따라서 이 프로젝트는 엄밀한 의미의 **미래 주가 예측 모델이라기보다, 주식 데이터를 이용한 회귀분석 학습 예제**에 가깝습니다.

다음과 같은 한계가 있습니다.

* 다음 거래일의 가격을 직접 예측하도록 설계되지 않음
* 기술적 지표에 당일 종가 정보가 포함됨
* 시계열 교차검증과 워크포워드 검증을 적용하지 않음
* 거래비용과 세금 등을 고려한 백테스트가 없음
* 기업 재무정보와 거시경제 변수를 반영하지 않음
* 과거 데이터의 성능이 미래 투자 성과를 보장하지 않음

특성 중요도는 인과관계를 의미하지 않으며, 선형모델의 표준화된 입력변수에 대한 회귀계수 절대값을 나타냅니다.

---

## 8. 학습한 내용

이 프로젝트를 통해 다음 내용을 실습했습니다.

* 외부 금융 데이터 수집
* pandas를 활용한 시계열 데이터 처리
* 이동평균·RSI·볼린저 밴드 계산
* 학습 데이터와 테스트 데이터의 시간순 분리
* 특성 스케일링
* 선형 회귀 및 규제 회귀모델 비교
* 회귀모델 평가 지표 계산
* 분석 결과 시각화
* Streamlit 기반 데이터 대시보드 구현
* 명령줄 인자를 활용한 프로그램 실행

---

## 9. 향후 개선 방향

* 다음 거래일 종가 또는 수익률을 타깃으로 변경
* 단순 가격 예측 대신 상승·하락 분류모델 비교
* 시계열 교차검증 및 워크포워드 검증 적용
* 단순 기준모델과 성능 비교
* 백테스트와 거래비용 반영
* 모델·스케일러 저장 및 재사용
* 테스트 코드와 입력값 검증 추가
* 분석 결과와 실행 화면 이미지 추가

---

## Disclaimer

본 프로젝트는 데이터 분석과 머신러닝 학습을 위한 개인 프로젝트입니다.

프로젝트에서 제공하는 분석 결과는 투자 권유 또는 금융 자문이 아니며, 실제 투자에 활용하여 발생한 손실에 대해 책임지지 않습니다.
