# Core ML은 무엇인가?
#### App에 머신러닝 모델을 integrate 해주는 Framework입니다.  

<img width="150" alt="이미지 제목" src="https://user-images.githubusercontent.com/92635121/203232295-69ece942-c28c-4bef-b143-15ef422b0d31.png">


- Core ML은 머신러닝 알고리즘을 트레이닝 데이터 셋에 적용해 모델을 만들어, 만든 모델을 App에 통합시킵니다.
- Core ML은 iOS 11과 함께 출시되었습니다.  
  - 이 전에도 머신러닝을 App에 적용시킬 수 있었지만 그 방법이 어려웠고, CoreML은 그 과정을 간결하게 변화시켰습니다.
- 모델을 만든 후 앱에 통합하고, Device에 배포합니다.
  - 앱은 Core ML API와 User data를 사용해 예측, 트레이닝, 및 모델을 조정합니다.
- Core ML은 CPU, GPU 및 Neural Engine을 활용해 성능을 최적화하며, 메모리 사용과 전력 소비를 최소화합니다.
- Device에서만 모델을 실행하면, 네트워크 연결이 필요하지 않아 사용자의 데이터를 비공개해 안전성을 높일 수 있습니다.
- Core ML은 도메인 별 프레임워크와 기능을 제공합니다.

<br>

## Core ML의 Frameworks

|Framework|기능|
|---|---|
|Vision|- 컴퓨터 비전 알고리즘을 적용해 입력 이미지 및 비디오에 대한 다양한 작업을 수행<br>- 얼굴 및 얼굴 랜드마크 감지, 텍스트 감지, 바코드 인식, 이미지 등록 및 일반 기능 추적을 수행<br><br>`컴퓨터 비전 알고리즘` : 컴퓨터에게 시각(Vision) 데이터 처리 능력을 부여하는 기술로,<br>카메라가 인간의 눈이라면 컴퓨터 비전은 이 시각 데이터를 처리하는 인지능력입니다.|
|Natural Language|- 자연어 텍스트를 분석하고 언어별 메타데이터를 추론<br>- 다양한 자연어 처리(NLP) 기능을 제공하며, 해당 프레임워크로 텍스트를 단락, 문장, 단어로 분할|
|Speech|- 녹음된 오디오나, 실시간 오디오에서 음성 단어를 인식<br>- 키보드의 받아쓰기 지원은 해당 프레임워크를 사용해 오디오를 텍스트로 번역하는 것<br>- 음성 인식을 위해 Apple 서버에 의존하기 때문에, 네트워크 연결이 필요함|
|Sound Analysis|- 웃음이나 박수 소리와 같은 특정 소리를 식별<br>- 오디오 파일에서 300개가 넘는 소리를 식별할 수 있음|

<img width="400" alt="이미지 제목" src="https://user-images.githubusercontent.com/92635121/203240477-7b3766b9-7a8b-4832-8c09-763c76ef8d92.png">
 
<br>

## 모델 생성 방식

>출처: WWDC 2018 - Introducing Create ML

<br>

**아래 3가지 방식 중 하나를 택해 모델을 생성할 수 있습니다.**
1. Apple website에서 인기있는 모델들을 다운로드
2. 좋아하는 학습 라이브러리(Ex. turi, TensorFlow)를 선택하고 모델을 교육한 후, 이를 Core ML로 변환한 다음 앱에 통합
3. Swift의 Machine Learning Framwork인 Create ML 사용
