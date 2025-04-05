# 2. Python 기초 문법

# 들여쓰기(Indentation)

- 파이썬은 들여쓰기 코드를 통해 코드의 블록을 구분
- 들여쓰기가 일치하지 않으면 오류 발생

# 연산자

[07강 연산자 1(우선순위와 결합성)](https://github.com/SansuSunbe/PYTHON/blob/main/memo/07%EA%B0%95%20%EC%97%B0%EC%82%B0%EC%9E%90%201(%EC%9A%B0%EC%84%A0%EC%88%9C%EC%9C%84%EC%99%80%20%EA%B2%B0%ED%95%A9%EC%84%B1).md) 

[08강 연산자 2(조건식)](https://github.com/SansuSunbe/PYTHON/blob/main/memo/08%EA%B0%95%20%EC%97%B0%EC%82%B0%EC%9E%90%202(%EC%A1%B0%EA%B1%B4%EC%8B%9D).md) 

[09강 연산자 3(비트연산)](https://github.com/SansuSunbe/PYTHON/blob/main/memo/09%EA%B0%95%20%EC%97%B0%EC%82%B0%EC%9E%90%203(%EB%B9%84%ED%8A%B8%EC%97%B0%EC%82%B0).md) 

[10강 삼항 연산자](https://github.com/SansuSunbe/PYTHON/blob/main/memo/10%EA%B0%95%20%EC%82%BC%ED%95%AD%20%EC%97%B0%EC%82%B0%EC%9E%90.md) 

# 변수

[03강 변수의 선언과 자료형](https://github.com/SansuSunbe/PYTHON/blob/main/memo/03%EA%B0%95%20%EB%B3%80%EC%88%98%EC%9D%98%20%EC%84%A0%EC%96%B8%EA%B3%BC%20%EC%9E%90%EB%A3%8C%ED%98%95.md) 

# 파이썬 주요 컬렉션

- 데이터를 여러 개 모아서 저장하는 자료구조
- 파이썬에서 데이터를 효과적으로 저장하고 다루는데 중요한 역할

## 리스트(List)

- 순서가 있는 변경 가능한 데이터의 집합
- 다양한 데이터 타입을 혼합해서 저장 가능
- 중복값 허용
- Mutable(변경 가능)

### Mutable 객체는 생성 후에도 상태가 바뀔 수 있지만
Immuatable 객체는 생성 이후에 상태가 바뀌지 않음

## 튜플(Tuple)

- 순서가 있는 변경 불가능한 데이터의 집합
- 한 번 생성된 후 값을 변경 불가
- Immutable

## 셋(Set)

- 순서가 없고 중복을 허용하지 않는 데이터의 집합
- 집합간의 연산을 지원
- Immutable

## 딕셔너리(Dictionary)

- 키와 값 쌍으로 이루어진 데이터의 집합
- 순서는 없지만 키를 통해 값을 빠르게 찾기 가능
- Mutable

## 컬렉션 예시

```python
# list, tuple, set, dict

# list
li = [1, 2, 3, 1, 2, 3]
print(li, type(li))

# tuple
tu = (1, 2, 3, 1, 2, 3)
print(tu, type(tu))

# set
se = {1, 2, 3, 1, 2, 3}
print(se, type(se))
se1 = {'봄', '여름', '가을', '겨울'}
print(se1, type(se1))

# dict
di = {'a' : 10, 'b' : 20}
print(di, type(di))
```

# 제어문

- 프로그램의 흐름을 제어하는 역할

## 조건문

- 특정 조건을 만족할 때만 코드 실행

### if : 조건 하나

### if - else : 조건 참과 거짓

### if - el - else : 조건 2개 이상

## 반복문

- 일정 조건이 만족할 때까지 반복 실행

### for : 범위, 개수를 알 때

### while : 조건을 알 때

## 기타 제어문

- 반복문의 제어가 필요할 때

### break : 반복문 즉시 탈출

### countinue : 반복문의 나머지 코드를 건너 뛰고(스킵) 다음 반복을 시작할 때

### pass : 구조만 만들고 나중에 내용을 채울 때 사용

# 함수(Function) 정의

### 특정 작업을 수행하는 코드 모음
코드의 재 사용성 증가
코드의 가독성 향상
코드의 모듈(부품)화 가능

## 함수

- 코드의 재사용성을 높이기 위해, 특정 작업을 수행하는 코드를 하나의 묶음으로 정의한 것

## 내장 함수

- 파이썬에서 제공하는 기본 함수

## 사용자 정의 함수

- 파이썬에서 함수는 def키워드를 사용해 정의
- 함수를 정의하고 호출하여 반복 작업을 간단히 처리 가능

## 함수 문법

```python
def 함수명(매개변수1, 매개변수2, ...) : 
	코드 블록
	return 반환값
```

### def

- 함수를 정의할 때 사용하는 키워드

### 함수명

- 호출 할 때 사용할 함수의 ㅣ름

### 매개 변수

- 함수가 외부에서 입력받은 값들, 매개변수 유무에 따라 호출 방법이 달라짐

### 코드 블록

- 함수가 실행될 때 실행할 코드

### return

- 함수 실행이 완료된 후 결과를 반환할 때 사용, return 유무에 따라 호출 방법과 결과값이 달라짐

### 인수

- 함수를 호출할 때 전달되는 실제 값

## 함수 호출

### 1. 매개변수 X, 리턴 값 X ⇒ 함수명()

### 2. 매개변수 O, 리턴 값 X ⇒ 함수명(인수1, 인수2, …)

### 3. 매개변수 X, 리턴 값 O ⇒ print(함수명())
                                         ⇒변수명 = 함수명()

### 4. 매개변수 O, 리턴 값 O ⇒ print(함수명(인수1, 인수2))
                                         ⇒ 변수명 = 함수명(인수1, 인수2)

## 람다함수(lambda)

- 런타임에서 생성해서 사용할 수 있는 익명 함수

### 특징

- 익명함수(함수 이름 없이 사용가능)
- 간결한 표현(한 줄로 정의 가능)
- 하나의 표현식만 가질 수 있음

### 장점

- 코드 간결화
- 고차 함수와 함께 사용에 용이(ex : map, filter 등)
- 일회성 함수로 적합

### 단점

- 복잡한 로직에는 부적합
- 디버깅이 어렵고 가독성이 떨어질 수 있음
- 재사용성 떨어짐

### 예시

```python
multiply =  lambda x, y : x * y
print(multiply(2, 3))
print(multiply(10, 50))
```

# 클래스(Class)

### 데이터(속성)와 기능(메서드)을 하나로 묶어 관리할 수 있는 구조
클래스로부터 여러 인스턴스(객체) 생성

```python
class 클래스명 : 
	def __init__(self, 매개변수1, 매개변수2) : 
	self.속성1 = 매개변수1
	self.속성2 = 매개변수2
	
	def 메서드명(self) : 
	# 메서드 실행 코드
	print({self.속성1})
```

## 클래스 예시

```python
class Person : 
  def __init__(self, name, age) :
    self.name = name
    self.age = age

  def info_print(self) : 
    print(f"Hello My Name Is {self.name}")
    print(f"My Age Is {self.age}")
    
# 객체명 = 클래스명(인수1, 인수2)
person1 = Person("JIN", 20)
person1.info_print()

person2 = Person("LEE", 23)
person2.info_print()
```

## 객체(Object)

- 클래스에서 생성된 실제 인스턴스
- 클래스를 통해 만들어진 하나의 독립된 개체

## 메서드(method)

- 클래스 내부에 정의된 함수, 객체가 수행할 수 있는 동작을 정의
- self 인자를 통해 객체 자체를 참조함

## 인스턴스 메서드

- 객체를 통해 호출
- 인스턴스 변수를 처리하는 함수

## 클래스 메서드

- @classmethod 데코레이션 사용
- 클래스 자체를 인자로 받아 동작
- 클래스 변수에 접근 가능

## 정적 메서드

- @staticmethod 데코레이션 사용
- 클래스나 인스턴스와 무관하게 독립적으로 실행

# 컬렉션 메서드

## 리스트

### append(x)

- 리스트의 끝에 x추가

### remove(x)

- 리스트에서 첫 번째 x제거

### pop(idx)

- 인덱스 i의 항목 제거 및 반환, 
인덱스 생략 시 마지막 항목 제거

### clear

- 모든 항목 제거

### 예시

```python
li = [1, 2, 3, 4]
# 추가
li.append(5)
print(li)

# 삭제
li.remove(2)
print(li)

# 삭제
li.pop(0)
print(li)

# 리스트 내의 모든 값 지우기
li.clear()
print(li)
```

## 튜플

### count(x)

- 튜풀에서 항목x의 개수 반환

### index(x)

- 항목 x가 처음 나타나는 인덱스 반환

### 예시

```python
# 튜플 메서드

tu = (1, 2, 3, 1)
print(tu.count(1))
print(tu.index(1))
```

## 세트 메서드

### add(x)

- 세트에 x추가

### remove(x)

- 세트에서 x제거, 없으면 keyError

### discard(x)

- x제거, 없어도 오류 없음

### clear()

- 모든 항목 제거

### 예시

```python
# 세트 메서드

se = {1, 2, 3}

# 추가 메서드
se.add(4)
print(se)

# 삭제 메서드(.remove(값))
# se.remove(0)
print(se)

# 삭제 메서드(.discard(값))
se.discard(0)
print(se)

# 삭제 메서드(.pop())
se.pop()
print(se)
```

## 딕셔너리 메서드

### get(key)

- key에 대응하는 값 반환

### pop(key)

- key에 대응하는 값 제거 및 반환

### clear()

- 모든 항목 제거

### 예시

```python
# 딕셔너리 메서드

di = {'a' : 1, 'b' : 2} 
print(di)

print(di.get('a'))

print(di.keys())

print(di.values())

print(di.clear())

print(di, type(di))
```

# 텍스트 파일 입출력

## 파일 입출력

- 데이터를 파일에 저장하거나 파일로부터 읽어오는 과정

[26강 파일 입.출력](https://github.com/SansuSunbe/PYTHON/blob/main/memo/26%EA%B0%95%20%ED%8C%8C%EC%9D%BC%20%EC%9E%85%20%EC%B6%9C%EB%A0%A5.md) 

## CSV(Comma-Separated Values) 파일 입출력

- 쉽표로 구분된 데이터 파일
- CSV 모듈을 사용하여 CSV 파일을 처리할 수 있다.

## 파일 쓰기

- csv.writer를 사용하여 데이터를 CSV 파일에 쓰기 가능

### writerow()

- 한 줄씩 데이터를 작성

### writerows()

- 여러 줄 데이터를 한꺼번에 작성

### 예시

```python
# csv 파일의 쓰기

import csv

with open("data.csv", "w", newline = '') as f : 
    writer = csv.writer(f)
    writer.writerow(["이름", "나이", "직업"])
    writer.writerow(["홍길동", 30, "백수"])
    writer.writerow(["고길동", 15, "학생"])
```

![image](https://github.com/user-attachments/assets/66624a57-068e-43be-a639-359e81609537)

## 파일 읽기

- csv.reader를 사용하여 CSV 파일을 읽기 가능
- 각 줄의 데이터를 리스트 형태로 반환

### 예시

```python
# csv 파일 읽기

with open("data.csv", "r") as f : 
    reader = csv.reader(f)
    # print(reader) 주소값 반환
    for i in reader : 
        print(i)
```
