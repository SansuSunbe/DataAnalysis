# 26. Iris 데이터 셋 실습

# Iris 데이터 셋

### iris 데이터 셋 : 꽃받침(sepal)과 꽃잎(petal)의 크기를 기반으로 아이리스 꽃의 품종을 분류하기 위해 만들어짐
균형잡힌 데이터로 각 클래스(품종)에 균일하게 50개 데이터를 포함함
150개의 데이터 포인트, 4개의 수치형 특징과 1개의 범주형 클래스(품종)

| 컬럼명 | 설명 | 단위 |
| --- | --- | --- |
| sepal_length | 꽃받침의 길이 | cm |
| sepal_width | 꽃받침의 너비 | cm |
| setal_length | 꽃잎의 길이 | cm |
| setal_width | 꽃잎의 너비 | cm |
| species | 꽃의 품종(3종류로 구성 | 범주형 |

| 품종(species) | 설명 |
| --- | --- |
| setosa | 아이리스 세토사 |
| versicolor | 아이리스 버시컬러 |
| virginica | 아이리스 버지니카 |

## Iris 데이터 셋 프로젝트 단계

### 1. 데이터 셋 로드

### 2. 데이터 구조 확인

### 3. 데이터 프레임 생성 및 요약

### 4. 데이터 시각화

### 5. 모델 생성

### 6. 모델 학습

### 7. 결과 시각화

### 8. 분류와 군집 비교

### 9. 군집 품질 평가

## 실습

### 데이터 셋 로드

```python
import pandas as pd
from sklearn.datasets import load_iris

iris = load_iris()
#  꽃받침(sepal)과 꽃잎(petal)
iris
```

### 데이터 구조 확인

```python
print(iris.keys())
# print(iris.data)
# print(iris.target)
# print(iris.feature_names)
# sepal : 꽃받침, petal : 꽃잎
#  ['sepal length (cm)', 'sepal width (cm)', 'petal length (cm)', 'petal width (cm)']
# print(iris.target_names)
# ['setosa' 'versicolor' 'virginica']

X = iris.data #독립변수
y = iris.target #종속변수
print(X)
print(y)
```

### 데이터 프레임 생성 및 요약

```python
df = pd.DataFrame(X, columns=iris.feature_names)
df.info()
df.describe()
# df
```

### 데이터 시각화

```python
import seaborn as sns
import matplotlib.pyplot as plt

#X[:, 0], X[:, 1] : 꽃받침 길이와 너비를 선택
plt.scatter(X[:, 0], X[:, 1])
plt.xlabel("Sepal Length")
plt.ylabel("Sepal Width")
plt.title("Sepal Length vs Sepal Width")
plt.show()

```

### 모델 생성 및 학습

```python
from sklearn.cluster import KMeans
import numpy as np

X = iris.data[:, [0, 1]]  # sepal length와 sepal width만 사용
kmeans = KMeans(n_clusters=3, random_state=42)
kmeans.fit(X)

#각 데이터 포인트의 클러스터 레이블 얻기
labels = kmeans.labels_
labels

```

### 결과 시각화

```python
labels = kmeans.labels_  # 각 데이터 포인트의 군집 레이블
center = kmeans.cluster_centers_  # 각 군집의 중심점
plt.scatter(X[:, 0], X[:, 1], c=labels, cmap='viridis')
plt.scatter(center[:, 0], center[:, 1], c='red', marker='X', s=200)

```

### 분류와 군집화 비교 시각

```python
plt.figure(figsize = (10, 6))

#왼쪽 : 분류
plt.subplot(121)
plt.plot(X[y==0, 2], X[y==0, 3], "yo", label="setosa")
plt.plot(X[y==1, 2], X[y==1, 3], "bs", label="versicolor")
plt.plot(X[y==2, 2], X[y==2, 3], "g^", label="virginica")

# 오른쪽 : 군집
plt.subplot(122)
plt.scatter(X[:, 2], X[:, 3], c = "k", marker = '.')
plt.tick_params(labelleft=False)

plt.show()
```

```python
from sklearn.cluster import KMeans

kmeans = KMeans(n_clusters = 2, random_state = 52)
kmeans.fit(X[:, 2:4])

#각 데이터 포인트에 대한 클러스터 레이블
labels = kmeans.labels_
labels

#k-means 중심점
center = kmeans.cluster_centers_
print(center)

#시각화
plt.figure(figsize = (10, 6))

#왼쪽 : 분류
plt.subplot(121)
plt.plot(X[y==0, 2], X[y==0, 3], "yo", label="setosa")
plt.plot(X[y==1, 2], X[y==1, 3], "bs", label="versicolor")
plt.plot(X[y==2, 2], X[y==2, 3], "g^", label="virginica")

#오른쪽 : kmeans 적용한 군집화
plt.subplot(122)
plt.scatter(X[:, 2], X[:, 3], c = labels, marker='.')
plt.scatter(center[:, 0], center[:, 1], c='red', marker = "x", s=50)
plt.tick_params(labelleft = False)
plt.show()
```

### 군집 품질 평가

```python
from sklearn.metrics import silhouette_score

sa = silhouette_score(X[:, 2:4], labels)
print(f"실루엣 스코어 : {sa}") #-1~1
```

```python
#calinski-harabasz 지수 : 군집간 분산과 군집내분산의 비율을 측정
from sklearn.metrics import calinski_harabasz_score

ch = calinski_harabasz_score(X[:, 2:4], labels)
print(ch)
```