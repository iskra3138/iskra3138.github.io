<https://cloud.google.com/tpu/docs/colabs?hl=ko>

### 데이터가 작다면 TPU 효과가 많지는 않음
Do not expect outstanding TPU Performance on a dataset as small as MNIST
[출처] <https://colab.research.google.com/drive/1VszjmeR9Nqw3DwqYR408O4BDke0TZIDm?hl=en#scrollTo=TTwH_P-ZJ_xx>

### TPU 학습과 평가 phase 전환 시 오랜 시간이 걸리는 문제
in the present version of Tensorflow (1.14), switching a TPU between training and evaluation is slow (appro. 10sec). For small models, it is recommented to run a single eval at the end
[출처] <https://colab.research.google.com/drive/1VszjmeR9Nqw3DwqYR408O4BDke0TZIDm?hl=en#scrollTo=TTwH_P-ZJ_xx>

### TPU는 GCP에 위치해 있으므로 데이터도 GCP에 있는 것이 좋음
TPUS are located in Google Cloud, for optimal performance, they read data directly fromm Google Cloud Storage.
[출처] <https://colab.research.google.com/drive/1VszjmeR9Nqw3DwqYR408O4BDke0TZIDm?hl=en#scrollTo=TTwH_P-ZJ_xx>
- code 실험 결과 추가

### dataset.batch에서 TPU사용 시 drop_remainder=True
drop_remainder is important on TPU, batch size must be fixed.
[출처] <https://colab.research.google.com/drive/1VszjmeR9Nqw3DwqYR408O4BDke0TZIDm?hl=en#scrollTo=TTwH_P-ZJ_xx>

### GCP에서 Model이 Serving으로 Deploy된 이후에는 더 이상 bucket이 필요없다면, storage 비용 절감을 위해서 삭제
Model deployed on  AI Platform autoscale to zero if not used. There will be no AI Platform charges after you are done testinig. Google Cloud Storage incurs charges. Empty the bucket after deployment if you want to avoid these. Once the model is deployed, the bucket is not useful anymore
[출처] <https://colab.research.google.com/drive/1VszjmeR9Nqw3DwqYR408O4BDke0TZIDm?hl=en#scrollTo=TTwH_P-ZJ_xx>

### 모든 data type을 지원하는 것은 아님
현재 TPU에서는 tf.float32, tf.int32, tf.bfloat16, tf.bool 데이터 유형만 지원됩니다. tf.uint8, tf.string, tf.int64와 같은 다른 일반적인 데이터 유형은 데이터 사전 처리 중에 지원되는 데이터 유형 중 하나로(TPUEstimator의 input_fn으로) 변환되어야 합니다. 다른 예시는 MNIST 가이드를 참조하세요. 하나의 예시로, MNIST의 이 코드 스니펫은 tf.uint8 바이트 시퀀스로 저장된 image 텐서를 tf.float32 텐서로 변환합니다.
[출처] <https://cloud.google.com/tpu/docs/troubleshooting?hl=ko>

