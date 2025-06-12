# 24. MNIST 데이터 셋 & 실습

# MNIST 데이터 셋

### 손 글씨 숫자 이미지(0~9)로 구성된 데이터 셋
머신러닝 및 딥 러닝 연구에서 가장 널리 사용되는 대표적인 벤치마크 데이터 셋
총 70,000개의 이미지 데이터
이미지 크기 28X28 픽셀, 1채널(회색조)
데이터 분할 : 훈련 데이터 60,000개 테스트 데이터 10,000개

## 모델 설계 주요 단계

### 1 단계 : 데이터 준비

- 데이터 전처리
    - 정규화, 원-핫 인코딩
    - 학습 데이터와 검증 데이터 분리

### 2 단계 : 모델 정의

- Sequential API
    - 단순한 모델 정의 방식
- Functional API
    - 복잡한 모델 정의 및 멀티 입력/출력 설계 가능

### 3 단계 : 학습 과정 설정

- 손실함수(Loss Function)
    - Cross-Entropy, MSE 등
- 옵티마이저(Optimizer)
    - SGD, Adam 등
- 평가지표(Metrics
    - Accuracy, Precision, Recall 등

## Mnist의 모델 설계

### 1 단계 : 데이터 준비

- 데이터 전처리
    - MNIST 이미지를 정규화(0~1 범위)
    - 레이블 데이터를 원-핫 인코딩
- 데이터 분리
    - 학습 데이터와 검증 데이터를 분리

### 2단계 모델 정의

- Sequential API
    - 단순한 모델 정의 방식
- Functional API
    - 복잡한 구조 설계 가능

### 3단계 : 학습 과정

## 과정

### 입력 → 예측 → 손실 계산 → 역전파 → 가중치 업데이트

- 옵티마이저를 사용해 반복적으로 가중치 업데이트
- 데이터의 반복학습(에포크 단위)

### 배치 크기

- 학습 속도와 메모리의 균형

### 에포크

- 데이터 셋 전체 학습 횟수

# 정규화 기법

## Dropout (드롭아웃)

- 학습 중 뉴런의 일부를 랜덤하게 비활성화하여 과적합(Overfitting)을 방지하는 기법
- 학습 시 특정 뉴런에 지나치게 의존하는 것을 방지
- 테스트 시에는 드롭아웃을 적용하지 않음

### **작동 원리**

- 뉴런의 활성화 값을 일정 비율로 랜덤하게 제거 (0으로 설정)
- 학습 시 매번 다른 뉴런 조합으로 학습, 모델의 일반화 성능 향상

## Batch Normalization (배치 정규화)

- 각 층의 출력을 정규화하여 학습을 안정화하고 학습 속도를 향상시키는 기법

### **작동 원리**

- 미니배치(mini-batch)마다 층의 출력을 평균과 분산을 기준으로 정규화
- 학습 시 각 층의 입력값 분포를 안정화하여 Gradient Vanishing/Exploding 문제 완화

# 학습 최적화

## Learning Rate Scheduling

### 학습 속도(Learning Rate)를 동적으로 조정하여 학습을 최적화하는 기법

- 학습 초반에는 큰 학습 속도로 빠르게 진행
- 학습 후반에는 작은 학습 속도로 미세한 조정을 통해 최적화

## Early Stopping

- 학습 중 검증 손실(validation loss)이 더 이상 개선되지 않을 때 학습을 조기 종료하는 기법
- 불필요한 학습을 방지하고 과적합을 줄임

### **작동 원리**

- 에포크마다 검증 손실을 모니터링
- 검증 손실이 개선되지 않는 에포크 수가 `patience`를 초과하면 학습 종료

## 실습

```python
import matplotlib.pyplot as plt
from tensorflow.keras.datasets import mnist

# MNIST 데이터셋 로드
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()

# 데이터 정보 출력
print(f"Train images shape: {train_images.shape}")
print(f"Train labels shape: {train_labels.shape}")

# 샘플 이미지 시각화
def plot_sample_images(images, labels, num_samples=10):
    plt.figure(figsize=(10, 2))
    for i in range(num_samples):
        plt.subplot(1, num_samples, i + 1)
        plt.imshow(images[i], cmap='gray')
        plt.axis('off')
        plt.title(labels[i])
    plt.tight_layout()
    plt.show()

# 첫 10개 샘플 이미지 출력
plot_sample_images(train_images, train_labels)
```

### 데이터 준비

```python
from tensorflow.keras.datasets import mnist
from tensorflow.keras.utils import to_categorical

# 데이터 로드
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()

# 데이터 정규화 (0~255 -> 0~1 범위)
train_images = train_images.astype('float32') / 255.0
test_images = test_images.astype('float32') / 255.0

# 레이블 원-핫 인코딩
train_labels = to_categorical(train_labels, 10)
test_labels = to_categorical(test_labels, 10)

# 데이터 확인
print("Train images shape:", train_images.shape)
print("Train labels shape:", train_labels.shape)
print("Test images shape:", test_images.shape)
print("Test labels shape:", test_labels.shape)
```

### 모델 정의

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Flatten

# Sequential 모델 정의
sequential_model = Sequential([
    Flatten(input_shape=(28, 28)),  # 입력 이미지를 평탄화
    Dense(128, activation='relu'),  # 은닉층
    Dense(10, activation='softmax')  # 출력층
])

sequential_model.summary()
```

```python
from tensorflow.keras.layers import Input
from tensorflow.keras.models import Model

# Functional 모델 정의
input_layer = Input(shape=(28, 28))
flatten_layer = Flatten()(input_layer)
hidden_layer = Dense(128, activation='relu')(flatten_layer)
output_layer = Dense(10, activation='softmax')(hidden_layer)

functional_model = Model(inputs=input_layer, outputs=output_layer)
functional_model.summary()
```

### 학습 과정 설정

```python
# 손실 함수, 옵티마이저, 평가 지표 설정
functional_model.compile(
    optimizer='adam',                # Adam 옵티마이저
    loss='categorical_crossentropy', # 손실 함수
    metrics=['accuracy']             # 평가 지표
)

# 학습 데이터 분리 (훈련/검증)
from sklearn.model_selection import train_test_split

train_images, val_images, train_labels, val_labels = train_test_split(
    train_images, train_labels, test_size=0.2, random_state=42
)

# 모델 학습
functional_model.fit(
    train_images, train_labels,
    validation_data=(val_images, val_labels),
    epochs=5, batch_size=32
)
```

### 평가

```python
#평가
test_loss, test_accuracy = functional_model.evaluate(test_images, test_labels, verbose=0)
print(f"Test Loss: {test_loss:.4f}, Test Accuracy: {test_accuracy:.4f}")
```

### 시각화

```python
# 필요한 라이브러리 임포트
import tensorflow as tf
from tensorflow.keras.datasets import mnist
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Flatten, Dense
from tensorflow.keras.utils import to_categorical
from sklearn.model_selection import train_test_split
import matplotlib.pyplot as plt

# 1. 데이터 로드 및 전처리
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()

# 데이터 정규화
train_images = train_images.astype('float32') / 255.0
test_images = test_images.astype('float32') / 255.0

# 레이블 원-핫 인코딩
train_labels = to_categorical(train_labels, 10)
test_labels = to_categorical(test_labels, 10)

# 데이터 분리 (학습/검증)
train_images, val_images, train_labels, val_labels = train_test_split(
    train_images, train_labels, test_size=0.2, random_state=42
)

# 2. 모델 정의 (Sequential API 사용)
model = Sequential([
    Flatten(input_shape=(28, 28)),  # 입력 레이어
    Dense(128, activation='relu'), # 은닉층
    Dense(10, activation='softmax') # 출력층
])

# 3. 모델 컴파일
model.compile(
    optimizer='adam',                # 옵티마이저
    loss='categorical_crossentropy', # 손실 함수
    metrics=['accuracy']             # 평가 지표
)

# 4. 모델 학습
history = model.fit(
    train_images, train_labels,          # 학습 데이터
    validation_data=(val_images, val_labels), # 검증 데이터
    epochs=5,                            # 학습 반복 횟수
    batch_size=32                        # 배치 크기
)

# 5. 테스트 데이터로 평가
test_loss, test_accuracy = model.evaluate(test_images, test_labels, verbose=0)
print(f"Test Loss: {test_loss:.4f}, Test Accuracy: {test_accuracy:.4f}")

# 6. 학습 결과 시각화
plt.plot(history.history['accuracy'], label='Train Accuracy')
plt.plot(history.history['val_accuracy'], label='Validation Accuracy')
plt.xlabel('Epochs')
plt.ylabel('Accuracy')
plt.legend()
plt.title('Training and Validation Accuracy')
plt.show()
```