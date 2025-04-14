# 7. Pandas-Series 패키지

# Pandas

### 데이터 분석을 위한 효율적인 데이터 구조를 제공
서로 다른 여러가지 유형의 데이터를 공통의 포맷을 정리하기 용이
데이터 분석에 관한 작업이 쉽게 가능
1차원 배열형태 데이터 구조 Series
2차원 배열형태 데이터 구조 DataFrame

# Series

### 1차원의 배열의 값에 각 값에 대응되는 인덱스를 부여할 수 있는 구조
열의 이름 : name
행의 이름 : index
별도 입력이 없을 때 열의 이름은 빈값(None)
행의 이름은 0부터 시작하는 정수 값
딕셔너리 구조와 유사

- 1차원 데이터 구조(인덱스 + 데이터)
- python 리스트와 유사하지만 가 값에 인덱스가 연결됨
- 데이터 분석에서 데이터 라벨링과 필터링에 강점

## Series 기본 구조

```python
import pandas as pd
s = pd.Series(data, index = index, name = name)
```

## 리스트 데이터를 Series로 변환

```python
import pandas as pd
data = [100, 200, 300]
s = pd.Series(data)
print("pandas Series : |w", s)
```

## Series의 형태

| index | Data |
| --- | --- |
| 0 | 100 |
| 1 | 200 |
| 2 | 300 |

## 구성 요소

| index(인덱스) | 데이터를 참조하기 위한 레이블 |
| --- | --- |
| Values(값) | 저장된 실제 데이터 |

## 속성

| series.index | Series의 인덱스 반환 |
| --- | --- |
| series.values | Series의 데이터 반환 |
| series.dtype | 데이터 타입 반환 |

## Series 생성 방법

### 1. 리스트로 생성

```python
pd.Series([값1, 값2, 값3])
```

### 2. 딕셔너리로 생성

```python
pd.Series({'key1' : value1, 'key2' : value2})
```

### 3. Numpy 배열로 생성

```python
pd.Series(numpy_array)
```

## Series 생성 예시

```python
import pandas as pd

data = [100, 200, 300]
print(data, type(data))

s = pd.Series(data)
print(s, type(s))
```

```python
import numpy as np

# 딕셔너리 생성 {key : value}
s2 = pd.Series({'a' : 100, 'b' : 85, 'c' : 25})
print(s2)

# Numpy 배열 생성
s3 = pd.Series(np.array([1.1, 2.2, 3.3]))
print(s3, type(s3))
```

```python
print(s)
print('인덱스 : ', s.index)
print('값 ; ', s.values, type(s.values))
print('자료형 : ', s.dtype)
print('기본 통계 정보 : |n', s.describe())
```

## Series에서 컬렉션 변환

- Series 객체에서 제공하는 메서드를 사용하여 다양한 데이터 타입으로 변환이 가능

### series → 리스트(List)

- tolist() 메서드를 사용하여 Series 데이터를 리스트로 변환

```python
# 리스트로 변환
result1 = s1.tolist()
print("리스트로 변환 : ", result1)
```

### series → 딕셔너리(Dictionary)

- to_dict() 메서드를 사용하여 Series 데이터를 딕셔너리로 변환
- Series 인덱스는 딕셔너리의 Key로 같은 Value로 변환됨

```python
# 딕셔너리로 변환
result2 = s1.to_dict()
print("딕셔너리로 변환 : ", result2)
```

### Series → Numpy 배열

- .values 속성을 사용하여 Series 데이터를 Numpy 배열로 변환

```python
# Numpy 배열 변환
result3 = s1.values
print("Numpy 배열로 변환 : ", result3, type(result3))
```

### Series → 데이터프레임(DataFrame)

- pd.DataFrame() 메서드를 사용하여 Series를 DataFrame으로 변환
- 기본적으로 Series는 DataFrame의 한 열(Column)으로 설정됨

### 컬렉션 → Series

```python
data1 = [10, 20, 30, 40]
print(data1, type(data1))

index = ['a', 'b', 'c', 'd']
s1 = pd.Series(data1, index = index, name = '숫자')
print(s1, type(s1))
```

## Series 추가, 수정, 삭제

### 새로운 데이터 추가

- 새로운 인덱스와 값 할당

```python
series[new_index] = new value
```

### 데이터 수정

- 특정 값을 수정 시에 해당
- 인덱스를 참조하여 값 업데이트

```python
series[index] = new_value
```

### 데이터 삭제

- drop() 메서드 사용
- 삭제 후 새로운 Series가 반환되며 기존 Series는 변경되지 않음

```python
series = series.drop(index)
```

## 예시

```python
# Series 생성
scores = pd.Series({'1번' : 95, '2번' : 70, '3번' : 50}, name = "점수")
print("기존 series 값 : \n", scores)

# 추가
scores['4번'] = 60
print(scores)

# 수정 3번의 점수 -> 70
scores['3번'] = 70
print(scores)

# 삭제
scores = scores.drop('1번')
print(scores)
```