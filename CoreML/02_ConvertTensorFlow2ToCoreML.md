# Convert TensorFlow2 to Core ML
Core ML Tools 4.0부터 `Unified Converter API` 를 사용해, 신경망 모델을 TensorFlow1 과 TensorFlow2에서 Core ML로 변환할 수 있습니다.
- **Unified Converter API** 는 최소 배포 타겟이 있는 Core ML Model을 생성합니다.
- Minimum Deployment Target : `iOS 13`, `macOS 10.15`, `watchOS 6`, `tvOS 13`

<br>

## 방법
> [참고 문서1 - Core ML Tools guides](https://coremltools.readme.io/docs/tensorflow-2)<br>
> [참고 문서2 - Installing Core ML Tools](https://coremltools.readme.io/docs/installation)

1. 먼저 위의 참고 문서2 를 참조해 가상 환경을 구축하고, Core ML Tools를 install 합니다.  
  
    구축이 되어 있다면, `pip install coremltools` 명령어만 입력

<br>

2. TensorFlow2 Model을 변환하기 위해선, 아래 리스트 중 하나를 준비해야 합니다.    
  - tf.keras.Model
  - HDF5 file path (.h5)
  - SavedModel directory path
  - A concrete function

  **❗️ TensorFlow2를 변환하는 권장 방식은 `tf.keras.Model` 클래스 객체를 사용하는 것입니다.**

<br>

3. 아래와 같이 `.h5` 파일을 load해 변환할 수 있습니다.

```python
import coremltools as ct 
import tensorflow as tf

# Load from .h5 file
tf_model = tf.keras.applications.Xception(weights="imagenet", 
                                          input_shape=(299, 299, 3))

# Convert to Core ML
model = ct.convert(tf_model)
```

<br>

4. 아래와 같이 Sequential Model을 변환할 수도 있습니다.

```python
import tensorflow as tf
import coremltools as ct

tf_keras_model = tf.keras.Sequential(
    [
        tf.keras.layers.Flatten(input_shape=(28, 28)),
        tf.keras.layers.Dense(128, activation=tf.nn.relu),
        tf.keras.layers.Dense(10, activation=tf.nn.softmax),
    ]
)

# Pass in `tf.keras.Model` to the Unified Conversion API
mlmodel = ct.convert(tf_keras_model, convert_to="mlprogram")

# or save the keras model in SavedModel directory format and then convert
tf_keras_model.save('tf_keras_model')
mlmodel = ct.convert('tf_keras_model', convert_to="mlprogram")

# or load the model from a SavedModel and then convert
tf_keras_model = tf.keras.models.load_model('tf_keras_model')
mlmodel = ct.convert(tf_keras_model, convert_to="mlprogram")

# or save the keras model in HDF5 format and then convert
tf_keras_model.save('tf_keras_model.h5')
mlmodel = ct.convert('tf_keras_model.h5', convert_to="mlprogram")
```

### Sequential Model이란?
- 연속적인 입력과 연속적인 출력을 생성하는 모델입니다.
- 음성인식과 같은 오디오 인식, 입/출력 길이가 다른 단어 인식인 기계 번역, 비디오 인식 등이 있습니다.
- 제 프로젝트인 `HandLink` 는 비디오를 인식해 모델을 생성시키는 것이기에, 해당 로직으로 변환해주었습니다.

<br>

아래와 같이 뜨면, 완료!

<img width="1219" alt="스크린샷 2022-11-23 오전 11 32 31" src="https://user-images.githubusercontent.com/92635121/203458961-905615bc-0cf6-4299-96b9-fc77dfb17a6f.png">
