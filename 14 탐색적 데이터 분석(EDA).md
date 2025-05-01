# 14. 탐색적 데이터 분석(EDA)

# EDA

### 데이터를 분석하고 이해하는 초기과정

- 데이터가 어떤 구조를 가지고 있는지, 어떤 패턴이 숨어 있는지

### 데이터의 구조, 패턴, 이상치 탐구

- 데이터 안에 이상치나 결측치 문제가 있는지

## EDA의 중요성

### 데이터 품질 확인

- 데이터가 깨끗한지, 잘못된 값이 없는지 확인

### 데이터 기반의 의사결정 지원

- 데이터를 잘 이해하면 더 나은 비즈니스나 연구 결정 가능

### 숨겨진 인사이트 발견

- 보이지 않던 중요한 패턴이나 관계를 찾을 수 있음

## EDA 3가지 주요 과정

### 1. 데이터 이해

1. 데이터 유형 확인
2. 기술 통계 분석
3. 결측치/이상치 탐구
- 숫자/날짜/범주형 데이터, 평균, 중앙값 등 기본 통계 결측치/이상치 해결

### 2. 시각적 분석

- 더 잘 이해하기 위해 그래프와 차트 활용
- 산점도
- 히스토그램
- 박스플롯
- 히트맵

### 3. 데이터 변환

- 분석하기 쉬운 형태로 바꾸는 단계
- 스케일링, 정규화, 로그변화, 파생변수 생성

### 3가지 과정이 필요한 이유

- 데이터의 결측이/이상치 발견 및 변수 간 관계 파악을 통해
데이터 분석 결과의 신뢰도 향상

## 예시

### 데이터 프레임 생성

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(42)

data = {'Category' : np.random.choice(['A', 'B', 'C'], size = 100),
        'Value1' : np.random.randint(1, 100, size = 100),
        'Value2' : np.random.normal(loc = 50, scale = 15, size = 100),
        'Date' : pd.date_range(start = '2025-01-01', periods = 100)}

df = pd.DataFrame(data)
df
```

### 기본 정보, 기술 통계 정보 확인

```python
df.info() # 기본 정보
df.describe() # 기술 통계 정보
```

### 히스토그램을 이용한 데이터 분포 확인

```python
# 데이터 분포 확인
# 히스토그램
plt.figure(figsize = (10, 6))
plt.hist(df['Value1'], bins = 15, color = 'blue', edgecolor = 'black', alpha = 0.7)
plt.xlabel('Value1')
plt.ylabel('Frequency')
plt.grid()
plt.show()
```

### KDE(커널 밀도 함수)

```python
# KDE(커널 밀도 함수)
import seaborn as sns

plt.figure(figsize = (10, 6))
sns.kdeplot(df['Value2'], fill = True, color = 'green', alpha = 0.5)
plt.xlabel('Value2')
plt.ylabel('Density')
plt.show()
```

### 데이터 비교, 관계 확인 이상치(BoxPlot)

```python
# 데이터 비교, 관계 확인 이상치
# BoxPlot

plt.figure(figsize = (10, 6))
sns.boxplot(data = df, x = 'Category', y = 'Value1', palette = 'Set2')

sns.stripplot(data = df, x = 'Category', y = 'Value1', color = 'black', size = 5, alpha = 0.7, jitter = True)

plt.xlabel('Category')
plt.ylabel('Value1')
plt.show()
```

# Iris 데이터 셋

### 꽃받침(sepal)과 꽃잎(petal)의 크기를 기반으로 아이리스 꽃의 품종을 분류하기 위해 만들어짐 균형잡힌 데이터로 각 클래스(품종)에 균일하게 50개 데이터를 포함
150개의 데이터 포인트, 4개의 수치형 특성과 1개의 범주형 클래스(품종)

## 상관 계수

- 두 변수 간의 선형관계를 나타내는 지표 값의 범위 -1 ~ 1로 표현

### 1

- 완전한 양의 상관
- 한 변수가 증가하면 다른 변수도 증가

### -1

- 완전한 음의 선형 관계
- 한 변수가 증가하면 다른 변수는 감소

### 0

- 선형 관계 없음
- 두 변수간에 선형적 관계가 없음

## 상관 분석

- 상관 계수를 사용하여 두 변수 간의 관계를 탐구하는 통계적 기법
- 변수 간의 연관성을 이해하거나 예측 모델 개발에 유용함

### 피어슨 상관 계수

- 두 변수 간의 선형적 관계 측정
- 데이터가 정규 분포를 따르고 연속성 변수일 때 적합

### 스피어만 상관 계수

- 변수의 순위를 기반으로 관계 측정
- 데이터가 비선형적이거나 정규분포를 따르지 않을 때 적합

### 캔달의 타우

- 두 변수의 순위간 일관성을 측정
- 스피어만 상관계수보다 민감도가 높음

## 예시

```python
# 라이브러리 불러오기
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# 1.iris 데이터 셋 로드
df = sns.load_dataset('iris')
df
```

```python
# 2.데이터 프레임 구조 확인
print(df.info())

# 3.데이터 프레임의 통계 확인
print(df.describe())

# 4.클래스 별 데이터 수 확인
print(df['species'].value_counts())

# 5.수치형 데이터만 선택
df_num = df.select_dtypes(include = ['float64', 'int64'])
print(df_num)
```

```python
# 6.상관계수 계산
corr_matrix = df_num.corr()
print(corr_matrix)

# 7. 히트맵 생성
plt.figure(figsize = (8, 6))
sns.heatmap(corr_matrix, annot = True, cmap = 'coolwarm', fmt = '.2f', linewidths = 0.5)
plt.title('heatmap')
plt.show()

# 분석 결과에 따른 인사이트
# petal_length와 petal_width는 강한 상관관계를 가지므로
# 하나의 특성만 선택하거나, 정규화, 차원축소 고려가 가능

# sepal_width는 독립적 특성으로 추가적인 분석에서 유용할 수 있음

# 데이터 구조
# 꽃받침(sepal)과 꽃잎(petal)의 변수들이 서로 다른 군집 정보를
# 제공할 가능성이 높음
# petal_length와 petal_width는 꽃의 분류에서 주요 역할을 할 가능성이 높음
```

# 산점도 행렬

- 여러 변수 간의 관계를 한 눈에 시각적으로 확인(표현)할 수 있는 그래프
- 다변량 데이터의 패턴을 탐색할 때 유용

## 역할

### 변수 간의 관계 탐색

- 각 변수 쌍의 산점도, 시각적 확인

### 상관 관계 파악

- 변수 간 양의 상관, 음의 상관, 무상관 여부를 직관적으로 파악

### 그룹 별 데이터 분포 확인

- 범주형 변수를 색상(hue)으로 구분하여 그룹 별 데이터 패턴을 탐색

## 구성 요소

### 대각선(Diagonal)

- 각 변수의 분포를 나타냄
- KDE Plot(커널 밀도 추정) 또는 히스토그램으로 표현 가능
- Iris 데이터셋에서 petal_length의 분포는 setosa와 다른 품종이 명확히 구분됨
- sepal_width는 겹치는 부분이 많음

### 비대각선(off-Diagonal)

- 두 변수 간의 산점도를 보여줌
- 변수 간의 선형/비선형 관계를 파악 가능
- Iris 데이터셋에서 petal_length와 petal_width는 강한 양의 상관 관계를 보임
- sepal_length와 sepal_width는 약한 관계를 가짐

![image.png](image.png)

# 다변량 데이터

- 여러 개의 변수(특징 다변량)로 구성된 데이터

## 예시

```python
# 데이터 로드 
# Iris 데이터 셋
df = sns.load_dataset('iris')
df

# 산점도 행렬 생성
sns.pairplot(df, 
             hue = 'species',           # 범주형 변수로 색상 구분
             diag_kind = 'kde',         # 대각선은 KDE plot
             palette = 'Set2',          # 색상 팔레트 설정
             markers = ['o', 's', 'D']) # 각 그룹의 마커 스타일 설정
# 그래프 출력
plt.show()
```