# 8. Pandas-DataFrame 패키지

# DataFrame

### 2차원 데이터를 다루기 위한 자료구조
행(Row)과 열(Column)로 구성되며 각 데이터에 고유한
인덱스(index)를 가질 수 있음
행과 열 데이터를 손쉽게 가공하고 분석 가능
엑셀의 표(Table)와 유사한 구조
2차원 데이터 구조(행, 열, 인덱스)

## 기본 구조

### values

- 몇 행 몇 열인지 데이터 값

### index

- 0부터 시작하는 행 방향의 인덱스, index 원하는 값으로도 지정 가능

### columns

- 열 방향 인덱스
- 열 이름

### dtypes

- 열 데이터 타입

```python
import pandas as pd
df = pd.DataFrame(values, index = index, columns = columns)
print(df)
```

## 예시

```python
import pandas as pd

values = [{1, 2, 3}, {7, 8, 9}]
print(values, type(values))
columns = ['A', 'B', 'C']
df = pd.DataFrame(values, columns = columns)
print(df)
df
```

## DataFrame 생성

```python
# 리스트로 생성
values = [{1, 2, 3}, {4, 5, 6}, {7, 8, 9}]
columns = ['첫 번째', '두 번째', '세 번째']
index = ['0행', '1행', '2행']
df = pd.DataFrame(values, columns = columns, index = index)
df

# 딕셔너리로 생성
data = {'name' : ['A', 'B'], 'scores' : [100, 50]}
df = pd.DataFrame(data)
s = pd.Series(data)
print(s)
df

# numpy 배열로 생성
import numpy as np
arr = np.array([[1, 2], [3, 4]])
df = pd.DataFrame(arr, columns = ['일', '이'])
df
```

### 1. 리스트로 생성

- 2차원 리스트를 사용

### 2. 딕셔너리로 생성

- 딕셔너리 키는 열 이름, 값은 데이터로 변환

### Numpy 배열로 생성

- Numpy 배열을 사용하여 데이터 프레임 생성

# DataFrame ↔ 컬렉션 변환

## 리스트 → DataFrame

- 딕셔너리는 열로 변환, 리스트에서는 행으로 변환

## 딕셔너리 → DataFrame

- 딕셔너리형 자료를 판다스로 가공할 수 있는 데이터 프레임으로 만들 수 있음
- 딕셔너리형 자료를 만들고 DataFrame()을 사용
- 시리즈에서는 키 값이 인덱스
- 데이터프레임에서는 키 값이 열 이름, 자동으로 행 인덱스에 숫자가 붙음

## DataFrame → 리스트(List)

- .values.tolist() 메서드를 사용하여 리스트로 변환

## DataFrame → 딕셔너리(Dictionary)

- .to_dict() 메서드를 사용하여 변환 가능

| dict | 각 열의 값이 딕셔너리 형태로 변환 |
| --- | --- |
| list | 열 이름을 키로, 값 목록을 리스트로 변환 |
| records | 각 행을 딕셔너리로 변환 |
| index | 인덱스를 키로 변환 |

## DataFrame → Numpy 배열

- .values를 사용하여 데이터 프레임 데이터를 Numpy 배열로 변환

## DataFrame → Series)

- .iloc[] 또는 .loc[]를 사용하여 데이터 프레임의 특정 열이나 행을 Series로 변환

## DataFrame 속성

```python
# DataFrame 속성 확인
print(df.values) # 데이터 값
print(df.index) # 행 인덱스
print(df.columns) # 열 이름
print(df.dtypes) # 데이터 타입
```

| .values | 데이터 값 |
| --- | --- |
| .index | 행 인덱스 |
| .columns | 열 이름 |
| .dtypes | 데이터 타입 |

## 예시

```python
import pandas as pd

# 상품 이름과 매출액 데이터를 Series로 생성
sales = pd.Series({'노트북' : 2000, '스마트폰' : 1500, '태블릿' : '1300'})
print(sales, type(sales))

# 시리즈 -> 데이터 프레임으로 변환
# Series의 인덱스는 데이터 프레임의 첫 번째 열(상품이름), 값은 두 번째 열(매출액)으로 변환
sales_df = sales.reset_index()
sales_df.columns = ['상품이름', '매출액']
print(sales_df, type(sales_df))
```

## 데이터 생성 예시

```python
# 데이터 생성
data = {'상품명' : ['노트북', '스마트폰', '태블릿'],
        '매출액' : [2000, 1500, 1300]}
df = pd.DataFrame(data)
```

# 행 선택과 열 선택

## loc

- 행과 열을 이름(레이블)로 접근

```python
df.loc[행 레이블, 열 레이블]
```

## loc 슬라이싱

- 슬라이싱 시 끝 값 포함

```python
df.loc[행 시작 : 행 끝, 열 시작 : 열 끝]
```

## iloc

- 행과 열을 숫자 인덱스로 접근

```python
df.iloc[행 번호, 열 번호]
```

## iloc 슬라이싱

- 슬라이싱 시 끝 값 제외

```python
df.iloc[행 시작 : 행 끝, 열 시작 : 열 끝]
```

## 기본 구조

```python
import pandas as pd

# 데이터 프레임 생성
df = pd.DataFrame({'상품명' : ['노트북', '스마트폰', '태블릿'], '매출액' : [2000, 1500, 1200]}, index = ['a', 'b', 'c'])
df
```

## loc 예시

```python
# loc를 사용하여 특정 행과 열 선택
print(df.loc['a', '상품명'], type(df.loc['a', '상품명']))
print(df.loc['a' : 'b', '상품명' : '매출액'], type(df.loc['a' : 'b', '상품명' : '매출액']))
# print("출력 끝")
df.loc['a' : 'b', '상품명' : '매출액']
```

## iloc 예시

```python
# iloc를 사용하여 특정행과 열 선택
print(df.iloc[0, 0]), type(df.iloc[0, 0])
print(df.iloc[0 : 2, 0 : 2], type(df.iloc[0 : 2, 0 : 2]))
```

# 연산 처리

## 데이터 프레임(DataFrame) 추가

### 새로운 열 추가

- 새로운 열에 데이터 추가

```python
df['새로운 열 이름'] = 값
```

```python
df['카테고리'] = ['전자기기', '전자기기']
print(df)
```

### 새로운 행 추가

- 새로운 행에 데이터 추가

```python
df.loc[새로운 인덱스] = 값
```

```python
df.loc[2] = ['태블릿', 1200, '전자기기']
print(df)
```

## 데이터 프레임 수정

### 특정 열 전체 수정

- 기존 열 데이터를 새로운 데이터 값으로 변경

```python
df['열이름'] = '새로운 값'
```

```python
df['카테고리'] = '가전제품'
print(df)
```

### 특정 값 수정

- 특정 행과 열의 값 변경

```python
df.loc[행 인덱스, '열이름'] = 새로운 값
```

```python
df.loc[1, '매출액'] = 1800
print(df)
```

## 데이터 프레임 삭제

### 특정 행 삭제

```python
df.drop(행 인덱스, axis = 0, inplace = True)
```

```python
df.drop(1, axis = 0, inplace = True)
print(df)
```

### 특정 열 삭제

```python
df.drop('열 이름', axis = 1, inplace = True
```

```python
df.drop('카테고리', axis = 1, inplace = True
print(df)
```

## 데이터 프레임 정렬

### 특정 열 기준으로 정렬(sort values)

```python
sort_values(by = '열 이름') # 특정 열 기준으로 정렬
	ascending = True # 오름차순(기본 값)
	ascending = False # 내림차순
```

```python
# 매출액 기준으로 내림차순 정렬
sorted_df = df.sort_values(by = '매출액', ascending = False)
print("매출액 기준 내림차순 정렬 : |n", sorted_df)
```

### 인덱스 기준으로 정렬(sort_index)

| 메서드명 | 기능 |
| --- | --- |
| sort_index() | 행 또는 열의 인덱스 기준으로 정렬 |
| axis = 0 | 행 인덱스 정렬(기본 값) |
| axis = 1 | 열 인덱스 정렬 |
| ascending | 오름차순 or 내림차순 |

```python
# 인덱스 기준으로 내림차순 정렬
df_sorted_index = df.sort_index(ascending = False)
print("인덱스 기준 내림차순 정렬 : |n", df_sorted_index)
```

## 데이터 프레임 중복 처리

| 메서드명 | 기능 |
| --- | --- |
| drop_duplicates() | 중복된 행을 제거 |
| subset = [’열 이름’] | 특정 열 기준으로 중복 확인 |
| keep = ‘first’ | 첫 번째 중복만 유지(기본 값) |
| keep = ‘last’ | 마지막 중복만 유지 |
| keep = False | 중복 행 모두 제거 |

## 예시

### 열 기준 정렬

```python
# 열 기준 정렬
sort_values(by = '열이름', ascending = True)
```

### 인덱스 기준 정렬

```python
sort_index(axis = 0, ascending = True)
```

### 중복 제거

```python
drop_duplicates(subset=['열 이름'], keep = 'first'
```

### 중복 행 삭제

```python
drop_duplicates(keep = False)
```

# 통계 연산

### 데이터를 요약하기 위해 통계적 지표를 사용
평균, 중앙값, 최빈값 등 데이터의 핵심적인 특성을 파악

## 평균

- 데이터를 모두 더한 후 데이터 수로 나눔

## 중앙값

- 데이터의 중앙에 위치한 값

## 최빈값

- 가장 자주 나타나는 값

# 결측값

### 데이터에서 값이 누락되거나 비어 있는 상태를 의미

## 결측값 처리(Missing Value Handling)

- 데이터에 누락된 값을 처리하는 과정
- 결측치를 제거하거나 대체값으로 채움
- 데이터 수집 과정에서 발생할 수 있음

## 결측값 탐색

- 데이터를 분석하기 전에 결측값이 “어디에 있는지, 얼마나 존재하는지” 파악

| 메서드명 | 기능 |
| --- | --- |
| isnull() | 각 셀에 결측값 여부를 확인하여 True or False 반환 |
| notnull() | 결측값이 아닌 경우 True 반환 |
| isnull().sum() | 각 열에 결측값 개수를 요약하여 표시 |

## 결측값 제거

- 결측값이 많지 않거나 해당 데이터가 분석에 중요하지 않을 경우 삭제

### 주요 메서드

| 메서드명 | 기능 |
| --- | --- |
| dropna() | 결측값이 포함된 행 또는 열을 제거 |
| how = ’any’(기본값) | 하나라도 결측값이 있는 행 또는 열 삭제 |
| how = ’all’ | 모두 결측값인 경우에만 삭제 |
| axis = 0(기본값) | 행 기준 제거 |
| axis = 1 | 열 기준 제거 |

## 결측값 대체

- 결측값을 제거하면 데이터 손실이 클 수 있으므로 대체하는 방법 사용

### 대체 방법

| 평균으로 대체 | 연속형 데이터의 경우 사용 |
| --- | --- |
| 중앙값으로 대체 | 이상치가 있는 데이터에 적합 |
| 최빈값으로 대체 | 범주형 데이터에 적합 |
| 고정값으로 대체 | 분석 목적에 따라 지정 |
| 이웃값으로 대체 | 시계열 데이터에 유용 |

### 주요 메서드

| 메서드명 | 기능 |
| --- | --- |
| fillna(value) | 특정 값으로 결측값 대체 |
| fillna(method = ‘ffill’ / ‘bfill’) | 앞 / 뒤 값으로 결측값 채우기 |
| mean() / median() / mode() | 통게값으로 결측값 채우기 |

## 결측값 처리 시 유의사항

### 데이터의 특성을 고려

- 결측값이 데이터 수집 과정의 오류인지, 자연스러운 누락인지 확인
- 대체 값이 실제 데이터 분포를 왜곡하지 않는지 확인

### 분석 목적에 맞는 처리

- 분석이나 모델링에 필요한 핵심 데이터가 손실되지 않도록 주의

### 결측값이 많은 열

- 30% 이상의 결측값이 있는 열은 삭제를 고려할 수 있음

## 예시

### 데이터 생성

```python
import pandas as pd
import numpy as np

# 학생 데이터 생성
data = {'Name' : ['짱구', '철수', '훈이', '맹구'],
        'Age' : [15, 16, np.nan, 14],
        'Math_Score' : [88, np.nan, 95, 70],
        'Eng_Score' : [100, np.nan, 90, 100]}

df = pd.DataFrame(data)
df
```

### 요약, 탐색, 처리, 평균

```python
# 데이터 요약
print(df.describe())

# 결측값 탐색
print(df.isnull())

# 결측값 처리
# 결측값을 평균으로 채우기
df['Age'] = df['Age'].fillna(df['Age'].mean())
df

# 평균 점수
df['Avg_Score'] = df[['Math_Score', 'Eng_Score']].mean(axis = 1)
df
```

### 기술 통계 확인

```python
# 문자 데이터 기술통계 확인
data = {'Name' : ['짱구', '철수', '훈이', '맹구'], 'city' : ['서울', '부산', '경기', '광명']}
df = pd.DataFrame(data)
print(df.describe())

df
```

# 데이터 그룹화

### 특정 열 기준으로 데이터를 묶어 집계하거나 분석하는 것을 의미
데이터의 요약 통계나 특정 그룹별 연산을 수행할 때 사용함

## 활용 사례

- 카테고리 별 매출 분석
- 특정 그룹 내 평균 합계 등 계산
- 다중 조건 그룹화

## 주요 메서드

| 메서드명 | 기능 |
| --- | --- |
| groupby() | 데이터를 하나 이상의 열로 그룹화 
그룹화 된 데이터에 대해 다양한 연산 수행 가능 |
| sum() | 그룹별 합계 계산 |
| mean() | 그룹별 평균 계산 |
| count() | 그룹별 데이터 개수 |
| min() | 그룹별 최소화 |
| max() | 그룹별 최대 값 |
| agg() | 그룹별 다중 연산 수행 |

# 필터링

### 데이터 프레임에서 특정 조건에 맞는 행(row)을 선택하는 작업
데이터를 원하는 조건으로 추출하여 분석하거나 가공할 수 있음

## 활용 예시

- 특정 매출액 이상의 데이터만 선택
- 상품명이 특정 단어를 포함한 행 필터링
- 결측값 또는 특정 데이터 타입만 선택

## 필터링 방법

### 단일 조건 필터링

- 특정 열에서 조건을 만족하는 데이터 선택

```python
df[조건식]
```

### 복합 조건 필터링

- 논리 연산자를 활용해 여러 조건을 결합

### 특정 열 필터링

- 특정 열만 선택하여 반환
- 필터링 조건과 함께 열 이름을 사용해 특정 열의 값만 출력

```python
df.loc[조건식, '열 이름']
```

### 결측값(Nan) 필터링

- 결측값이 포함된 데이터만 선택하거나 제거

## 예시

### 데이터 생성

```python
import pandas as pd

df = pd.DataFrame({'상품명' : ['노트북', '스마트폰', '태블릿', '헤드폰'],
                   '매출액' : [2000, 1500, 1200, 500]
})

# 단일 조건 필터링
# 매출액이 1000이상인 데이터 선택
filtered_df = df[df['매출액'] >= 1000]
print("매출액 1000 이상 : \n", filtered_df)

# 복합 조건 필터링
# 매출액이 1000 이상이고 상품명이 '노트북'이 아닌 데이터 선택
filtered_df = df[(df['매출액'] >= 1000) & (df['상품명'] != '노트북')]
print("매출액 1000 이상 & 상품명이 '노트북'이 아닌 데이터 : \n", filtered_df)

# 매출액이 1000 이상인 상품명만 출력
filtered_items = df.loc[df['매출액'] >= 1000, '상품명']
print("매출액 1000 이상인 상품명 : \n", filtered_items)

# 결측값이 포함된 데이터 선택
df_with_nan = pd.DataFrame({
    '상품명' : ['노트북', '스마트폰', 'None', '헤드폰'],
    '매출액' : [2000, 15000, None, 500]
})

filtered_nan = df_with_nan[df_with_nan['상품명'].isna()]
print("결측값이 포함된 데이터 : \n", filtered_nan)
```