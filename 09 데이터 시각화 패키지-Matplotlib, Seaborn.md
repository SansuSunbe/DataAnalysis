# 9. 데이터 시각화 패키지-Matplotlib, Seaborn

# 데이터 시각화

### 데이터를 그래프로 표현하여 패턴과 인사이트를 쉽게 이해할 수 있도록 돕는 도구
텍스트 데이터만으로는 숨겨진 관계를 찾기 어렵지만 “그래프를 활용하면 데이터의 구조를 쉽게 파악”가능

## 특징

1. 데이터를 시각적으로 표현하여 패턴과 인사이트 도출
2. 텍스트 데이터보다 이해가 빠르고 직관적
3. 다양한 분석 및 보고서 작성에 필수적
4. 데이터 크기가 커질 수록 시각화의 중요성이 커짐

# Matplotlib

### 파이썬에서 제공하는 2D 및 3D 시각화 도구
고도로 커스터마이징 가능
다양한 그래프 생성 가능
기본적이고 낮은 수준의 시각화 제공

## Matplotlib의 구성 요소

### pyplot 모듈

- Matplotlib의 핵심 모듈로, 간단한 인터페이스를 통해 기본적인 그래프 쉽게 생성 가능
- MATLAB 스타일의 명령어 기반으로 설계, 직관적 사용 가능
- 데이터를 시각화 하는 요소(선, 점 등)

### Figure

- 그래프가 그려지는 전체 캔버스
- 시각화 전체를 나타내는 컨테이너

### Axes

- 데이터가 시각화되는 실제 그래프 영역

## 그래프 생성 예시

```python
# 캔버스 생성
import matplotlib.pyplot as plt

# 전체영역
figure = plt.figure()
# 실제 그래프를 그리는 영역
axes = figure.add_subplot(1, 1, 1)

# 전체 영역
figure = plt.figure()

# 1행 2열 1번째 subplot
axes1 = figure.add_subplot(121)
axes2 = figure.add_subplot(122)

# 그래프 생성
plt.show()
```

## 막대 그래프 생성 예시

### Bar()

- 막대 그래프
- 범주형 데이터를 시각화 할 때 사용

```python
# Bar()
# 막대그래프 - 범주형 데이터를 시각화 할 때 사용
import matplotlib.pyplot as plt

x = ['봄', '여름', '가을', '겨울']
y = [250, 100, 230, 150]

plt.bar(x, y, color = 'skyblue')
plt.title("계절별 통계")
plt.xlabel("계절")
plt.ylabel("값")
plt.show()
```

### scatter()

- 산점도 그래프
- 두 변수 간의 관계를 나타낼 때 사용

```python
# scatter()
# 산점도 그래프 - 두 변수 간의 관계를 나타낼 때 사용
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [2, 4, 1, 8, 7]
plt.scatter(x, y, s = 100, c = 'red', label = '데이터 포인트')
plt.title("산점도")
plt.xlabel("X 축")
plt.ylabel("Y 축")
plt.legend()
plt.show()
```

### pie()

- 원형 그래프
- 데이터의 비율을 나타낼 때 사용

```python
# pie()
# 원형 그래프 - 데이터의 비율을 나타낼 때 사용
# autopct : 비율 표시
# explode : 조각 분리
import matplotlib.pyplot as plt

labels = ['봄', '여름', '가을', '겨울']
sizes = [50, 30, 12, 28]
explode = [0, 0.1, 0, 0] # 여름 조각 분리

plt.pie(sizes, labels = labels, autopct = '%.1f%%', explode = explode)
plt.title("계절 별 비율")
plt.show()
```

# 다중 플롯

### 한 그래프 안에 여러 데이터 시리즈를 겹쳐 표현하는 방법,
하나의 axes에 여러 선형 그래프, 막대 그래프 등을 겹쳐서 표시하는 그래프를 의미
다양한 데이터 간의 관계를 한 눈에 비교 가능

## 활용 예시

- 여러 제품의 판매량 비교
- 여러 지역의 기온 변화 비교

## 예시

```python
import matplotlib.pyplot as plt

# 데이터 생성
months = ['1월', '2월', '3월', '4월', '5월']
sales_A = [100, 150, 200, 250, 300]
sales_B = [80, 130, 170, 200, 270]

# 다중 플롯 생성
plt.plot(months, sales_A, label = "제품 A", color = "blue", marker = "o")
plt.plot(months, sales_B, label = "제품 B", color = "orange", linestyle = "--", marker = "s")

# 그래프 제목 및 설정
plt.title("제품 A와 제품 B의 월별 판매량")
plt.xlabel("월")
plt.ylabel("판매량")
plt.legend() # 범례 추가
plt.show()
```

# 서브 플롯

### 한 화면에 여러 개의 그래프를 분리하여 배치, 
plt.subplot(rows, cols, index)나 plt.subplots()로 서브 플롯 생성
각 플롯은 별도의 데이터와 설정을 가질 수 있음

## 활용 예시

- 각 제품의 판매 데이터를 개별 그래프로 표시
- 각 지역의 날씨 데이터를 별도로 표시

## 예시

```python
import matplotlib.pyplot as plt
# 데이터 생성
months = ['1월', '2월', '3월', '4월', '5월']
sales_A = [100, 150, 200, 250, 300]
sales_B = [80, 130, 170, 200, 270]

# 서브 플롯 생성(2행 1열)
plt.subplot(2, 1, 1) # 첫 번째 그래프
plt.plot(months, sales_A, color = "blue", marker = "o")
plt.title("제품 A의 월별 판매량")
plt.xlabel("월")
plt.ylabel("판매량")

plt.subplot(2, 1, 2) # 두 번째 그래프
plt.plot(months, sales_B, color = "orange", linestyle = "--", marker = "s")
plt.title("제품 B의 월 별 판매량")
plt.xlabel("월")
plt.ylabel("판매량")

plt.tight_layout() # 그래프 간 간격 조정
plt.show()
```

# Seaborn

### Matplotlib를 기반으로 하여 더 간단하면서 
고급 시각화와 더 나은 디자인을 기본적으로 제공
데이터 프레임과 통합하기 편리

## 특징

1. 그래프 스타일링이 자동 적용되어 시각적으로 더 깔끔하고 전문적인 결과 제공
2. 통계적 시각화 지원(히트맵, 분포그래프 등)
3. Pandas의 DataFrame과의 호환성 높음
4. 복잡한 그래프를 간단한 코드로 구현 가능

## 활용 예시

- 데이터 분석 및 통계적 시각화
- 머신러닝 모델의 데이터 탐색 및 결과 시각화
- 대규모 데이터 셋에서의 패턴 분석

## Matplotlib과 Seaborn 비교

| 특징 | Matplotlib | Seaborn |
| --- | --- | --- |
| 사용 용도 | 저수준의 그래프, 커스터마이징에 유리 | 고수준의 그래프, 빠르게 고품질 시각화 가능 |
| 스타일링 | 기본 스타일은 단순 | 세련된 기본 스타일 제공 |
| 데이터 프레임 지원 | 직접 지원하지 않음(Pandas와 별도 사용 필요 | 데이터 프레임과 자연스럽게 연동 |
| 학습 곡선 | 상대적으로 복잡 | 직관적이고 간단 |

## 주요 그래프 함수

### 데이터 분포 확인-히스토그램(histplot)

- 데이터의 분포 확인

### 데이터 관계 시각화-산점도(scatterplot)

- 두 변수 간의 관계 시각화

### 범주형 데이터 시각화-박스플롯(boxplot)

- 범주형 데이터의 분포와 이상치를 확인

### 데이터의 전반적 관계 확인-페이플롯(pairplot)

- 여러 변수 간의 관계를 한번에 시각화

## 예시

### 한글 깨짐 방지 코드

```python
import matplotlib.pyplot as plt
import seaborn as sns

!sudo apt-get install -y fonts-nanum
!sudo fc-cache -fv
!rm ~/.cache/matplotlib -rf

plt.rc('font', family = "NanumBarunGothic")
plt.rcParams['axes.unicode_minus'] = False
```

```python
tips = sns.load_dataset('tips')
tips
# total_bill : 총 청구 금액
# tips : 팀 금액
# sex : 성별
# smoker : 흡연 여부(y, n)
# day : 요일
# time : 식사시간(lunch, dinner)
# size : 동석한 인원 수
# total_bill	tip	sex	smoker	day	time	size
```

```python
print(tips)
print(tips.info())
print(tips.shape)
print(tips.describe())
print(tips.isnull().sum())
```

### 히스토그램 + KDE

```python
sns.histplot(tips['total_bill'], kde = True) # KDE : 분포를 부드럽게 표시
plt.title("총 계산 금액의 분포 (Histogram + KDE)")
plt.xlabel("총 계산 금액")
plt.ylabel("빈도")
plt.show()
```

### 페어플롯(PairPlot)

```python
sns.pairplot(tips, hue = "sex")
plt.show()
```

## 예시 2

```python
print("사용 가능한 seaborn 데이터셋 목록 : ")
print(sns.get_dataset_names())

# 예시
penguins = sns.load_dataset("penguins")
sns.scatterplot(x = "bill_length_mm" ,
                y = "bill_depth_mm", 
                hue = "species", data = penguins)
plt.title("펭귄 데이터 - 부리 길이와 깊이")
plt.xlabel("부리 길이 (mm)")
plt.ylabel("부리 깊이 (mm)")
plt.legend(title = "종")
plt.show()
```
