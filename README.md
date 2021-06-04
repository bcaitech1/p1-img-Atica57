# BoostCamp P stage 1
## -Mask Image Classification

# 프로젝트 개요

* 카메라로 비춰진 사람 얼굴 이미지 만으로 이 사람이 마스크를 쓰고 있는지, 쓰지 않았는지, 정확히 쓴 것이 맞는지 자동으로 가려낼 수 있는 모델 구축

* 마스크를 쓴 사람의 이미지를 입력으로 받아 나이, 성별, 마스크 착용 여부 등을 판별하여 18가지 클래스로 구별함

* 아래의 그림은 18가지 클래스 분류 기준을 나타낸 그림임

  ![img](https://github.com/Atica57/p1-img-Atica57/issues/1#issue-910967507)



# 코드 설명

### 코드 목록

> * [dataset.py](#dataset.py)
>   * 마스크 데이터셋을 읽고 전처리를 진행한 후 데이터를 하나씩 꺼내주는 Dataset 클래스를 구현한 파일
> * [train_inference_integrated.ipynb](#train_inference_integrated.ipynb)
>   * data set 설정, 모델 정의, train 및 test를 진행하는 주피터 노트북 코드



### 코드 주요 기능 설명



#### dataset.py

1. BaseAugmentation class(resize, mean, std, **args)
   *  Resize(), Normalize() 구현한 가장 기초적인 data augmentation 클래스
2. CustomAugmentation(resize, mean, std, **args)
   * CenterCrop(), ColorJitter() 등 다양한 data augmentation를 설정하는 클래스
3. MaskBaseDatasetdata_dir, mean=(0.548, 0.504, 0.479), std=(0.237, 0.247, 0.246), val_ratio=0.2)
   * 이미지 데이터를 입력으로 받아 이미지 경로, 성별, 나이, 마스크 착용여부에 대한 판별 결과를 반환하는 클래스
4. TestDataset(img_paths, resize, mean=(0.548, 0.504, 0.479), std=(0.237, 0.247, 0.246)))
   * 테스트 이미지 데이터셋에 관한 초기값, 연산함수 정의 클래스



#### train_inference_integrated.ipynb

1. Libarary 불러오기 및 경로설정
2. Parameter 설정
3. Loss Function, Creterion 정의
   * Cross Entropy Loss 클래스 정의, creterion 객체 선언 코드
4. Model(Pretrained) && Optimizer 정의
   * ResNet-50, EfficientNet-b4, EfficientNet-b7 선언 코드
   * Optimizer 정의(Adam, SGD 정의)
5. Scheduler 정의
   * StepLR, ReduceLROnPlateau, CosineAnnealingLR 정의
6. Training process
   * dataset 정의
     * dataset.py에 정의한 class를 이용하여 train dataset 객체 정의
   * Training loop
     * 사전에 정의한 파라미터 값을 이용하여 학습 진행

7. Test
   * dataset.py에 정의한 class를 이용하여 test dataset 객체 정의
   * test 진행, 결과를 submission.cvs 파일에 저장
