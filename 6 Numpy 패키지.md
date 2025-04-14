# 6. Numpy 패키지

# 데이터 전처리

### 데이터 분석 및 모델링 전에 데이터를 정리하고 변환하는 과정

## 필요성

- 결측값, 이상치 처리
- 데이터 정규화 및 표준화
- 범주형 데이터 인코딩

## 전처리 흐름

- 데이터 로드
- 결측값 확인 및 처리
- 데이터 스케일링
- 불필요한 컬럼 삭제 또는 변환

# 데이터 분석 패키지

## 패키지

- 하나의 디렉터리에 모아놓은 여러 모듈의 집합

## 넘파이(numpy)

- 배열 계산기능, 반올림, 버림 가능
    - floor, celi, power
- 다차원 배열 연산을 효율적으로 처리하는 python 라이브러리
- 빠른 배열 연산(C언어 기반)
- 효율적인 메모리 사용
- 선형대수와 수치 계산 지원

## 판다스(pandas)

- 데이터 프레임으로 데이터를 입력, 가공
    - describe, groupby

## 맷플롯립(matplotlib)

- 그래프 그리기 기능
    - plot(), bar() 등

## 그 외

### 수학(math), 통계 모델 작성 및 분석(ststsmodels) 등

# 배열(Array) 구조

### 하나의 자료형을 기준으로 순서가 있는 원소로 나열된 자료구조
파이썬에서 순차적으로 원소를 나열하는 배열 형태의 리스트(list)를 제공

## list 구조

- 순서를 가지고 일렬로 나열한 원소들의 모임
- 크기가 변할 수 있는 동적 할당
- 여러가지 자료형 허용
- 2차원 이상의 배열구조일 경우 내부 배열에서 원소의 개수가 달라도 됨

## 넘파이 배열구조

- 다차원 배열인 ndarray 클래스의 객체
- 하나의 자료형으로만 만들어진 원소들을 보관
- 고정된 크기를 갖는 정적 할당
- 숫자형과 문자열이 섞이게 되면 모두 문자열로 전환됨(한 가지 자료형만 허용)
- 내부 배열 내 원소 개수는 모두 같아야 함

# 행렬의 주요 연산

## 행렬 덧셈

- 같은 크기의 행렬에서 같은 위치의 원소를 더함

![image](https://github.com/user-attachments/assets/ac0e4011-148d-43bf-8c09-e3385db39875)

## 행렬 곱

- 두 행렬 곱 첫 번째 행렬의 행과 두 번째 행렬의 열에 대응하는 원소들을 곱하고 더한 값

![image 1](https://github.com/user-attachments/assets/23629c3b-2fcb-4503-9e98-39d139a9f5c3)

## 전치 행렬

- 행과 열을 서로 바꾼 행렬
- 원래 행렬의 각 원소를 표시함
- 화살표를 이용해A[i, j] → A[j, i]로 이동하는 과정 표시

![image 2](https://github.com/user-attachments/assets/dee4f241-10f1-42d6-8277-1d8d8c548c32)

## 역 행렬

- 원래 행렬과 곱했을 때 단위 행렬이 되는 행렬
- 행렬 A와 그 역행렬 A-1을 곱하면 단위 행렬(identity Matrix)을 얻음

![image 3](https://github.com/user-attachments/assets/a6fb2f51-c853-4362-8a3e-10e6ac459f22)

## 단위 행렬

- 주 대각선의 원소가 모두 1이고 나머지는 0인 행렬

![image 4](https://github.com/user-attachments/assets/192725cb-5c56-4347-9c90-f3b627b111bc)

# Numpy 객체 주요 속성

### .shape

- 배열의 각 차원 크기

### .ndim

- 배열의 차원 수

### .dtype

- 데이터 타입

### .size

- 배열의 총 원소 수
    
    ![image 5](https://github.com/user-attachments/assets/f3bb89a1-a5e8-43cf-92cd-b179f5347a67)


## Numpy 배열 선언

| 메서드명 | 기능 |
| --- | --- |
| np.array() | 리스트, 튜플로 배열 생성 |
| np.arrange() | 특정 범위로 배열 생성 |
| np.zeros() | 0으로 채워진 배열 생성 |
| np.ones() | 1로 채워진 배열 생성 |
| np.linspace() | 일정 간격으로 숫자 생성 |

## Numpy 주요 함수

| 메서드명 | 기능 |
| --- | --- |
| astype() | 데이터 타입 변경,
배열 추가 |
| transpose() | 행과 열 변환,
배열 수정 |
| sum() | 배열의 합계
 |
| mean() | 배열의 평균 |
| where() | 조건에 맞는 요소 검색 |
| append() | 기존 배열에 새로운 행/열추가
axis를 설정 시 추가되는 배열의 차원이 기존 배열과 동일해야함 |
| delete | 특정 행/열 삭제
삭제 후 새로운 배열로 반환되며 원본 배열은 변경되지 않음 |

## Numpy 함수 예시 1

```python
import numpy as np

# 리스트 -> numpy 배열 변환
li = [1, 2, 3, 4, 5]
print(f'리스트 : {li}', type(li))

li2 = [[1, 2, 3], [4, 5, 6]]
print(f'리스트2 : {li2}')

ar = np.array(li)
print(f'numpy 배열 : {ar}', type(ar))

# 1차원 배열
arr1 = np.array([1, 2, 5])
print(arr1)

# 차원 배열
arr2 = np.array([[1, 2, 3], [4, 5, 6]])
print(arr2)

# arange 정수 범위 생성
arr3 = np.arange(1, 10, 2) # 1부터 9까지 2간격
print(arr3)

arr4 = np.arange(0, 5, 0.5)
print(arr4)

# zeros()로 초기화된 배열 생성
zero_arr = np.zeros((3, 3))
print(zero_arr)
```

## Numpy 함수 예시 2

```python
# 기존 배열 생성
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr)
print(arr.ndim) # 2차원
print(arr.dtype) # int64
print(type(arr))
print(arr.shape)

# 추가
# 행 추가(axis = 0, 기본값)
new_row = [[7, 8, 9]]
# new_arr = np.append(arr, new_row, axis = 0)
# print(new_arr)
# print(new_arr.dtype, new_arr.shape)

# 열 추가(axis = 1)
new_column = [[10], [20]]
arr_new = np.append(arr, new_column, axis = 1)
print(arr_new, arr_new.shape)

# 배열 수정
arr_new[0][0] = 10
print(arr_new)

# 행 전체 수정
arr_new[1, :] = [100, 200, 300, 400]
print('수정된 행 확인 : \n', arr_new)
```

## Numpy 배열 슬라이싱

- 배열의 특정 요소를 선택하거나 잘라내는 작업
- 리스트 슬라이싱과 동일한 문법 사용하며 다차원 배열에서 각 차원을 ‘,’로 구분

## Numpy 배열의 사칙 연산

- 배열 간 같은 위치에 있는 요소끼리 연산
- 연산은 요소 별로 수행
  
![image 6](https://github.com/user-attachments/assets/b177a758-a8fb-46c8-a55f-c66959539002)

### 주의

- 배열의 크기(Shape)가 같아야 함
- 크기가 다르면 ‘*브로드캐스팅’*이 적용됨

## 브로드 캐스팅

- 서로 다른 크기의 배열 간 연산을 가능하게 하는 규칙
- 작은 배열이 큰 배열에 맞춰 확장됨

## 브로드 캐스팅 규칙

- 두 배열의 차원이 다르면, 작은 배열에 1추가
- 각 차원의 크기가 1이거나 같으면 연산 가능

## 결측치 처리

- 데이터셋에 값이 없는 경우를 의미
- Numpy에서는 np.nan으로 표현
- 데이터 분석에서 흔히 발생하는 문제로 Numpy는 결측치를 효율적으로 탐지하고 처리할 수 있는 기능을 제공함

### 결측지 탐지

- np.isnan()
    - 배열에서 결측지 위치를 확인

### 결측지 대체

- 평균값, 중앙값, 특정값 등으로 결측지 대체 가능
- np.nanmean()
    - 결측지를 제외한 평균값 계산
- arr[missing] = value
    - 결측지를 특정값으로 대체
