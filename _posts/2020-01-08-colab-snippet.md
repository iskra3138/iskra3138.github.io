### GCP 계정 연동
```python
from google.colab import auth
auth.authenticate_user()
```
### GCP project ID 확인
```python
!gcloud projects list
```

### GCP Bucket 생성
```python
PROJECT = "" #@param {type:"string"}
BUCKET = "gs://"  #@param {type:"string", default:"jddj"}
# bucket 생성
### option argument가 앞에오고 BUCKET이 제일 뒤로 가야 함
!gsutil mb -p {PROJECT} {BUCKET}
```

### GCP Bucket 목록 확인
```python
# bucket 목록 확인
!gsutil ls -p {PROJECT}
```

## 로컬 -> 버킷으로 파일 복사(=업로드)
```python
!gsutil cp -r src_url dst_url
```

### GCP Bucket 삭제
```python
!gsutil rm -r {BUCKET} 
```

[gsutil api 설명] <https://cloud.google.com/storage/docs/gsutil?hl=ko>
[gcloud api 설명] <https://cloud.google.com/sdk/gcloud/reference/?hl=ko>

### GCP model for serving 생성
```python
!gcloud ai-platform models create {MODEL_NAME} --project={PROJECT} --regions=us-central1
```

### GCP model version 생성
```python
!gcloud ai-platform versions create {MODEL_VERSION} --model={MODEL_NAME} --origin={export_path} --project={PROJECT} --runtime-version=1.14 --python-version=3.5
## Tensorflow version과 python version은 모델 생성 환경과 동일하게!!! 
```

### GCP model list 확인
```python
!gcloud ai-platform models list --project={PROJECT}
```

### GCP model version 삭제
```python
!gcloud ai-platform versions delete {MODEL_VERSION} --model={MODEL_NAME} --project={PROJECT}
```

### GCP model 삭제
```python
!gcloud ai-platform models delete {MODEL_NAME} --project={PROJECT}
```

### notebook process kill
```python
import os, signal
os.kill(os.getpid(), signal.SIGKILL)
```
