# GCP Instance 

참조: https://course.fast.ai/start_gcp.html

참조: https://towardsdatascience.com/running-jupyter-notebook-in-google-cloud-platform-in-15-min-61e16da34d52



- Bucket을 Mount해서 사용하려면 instance 생성 시 Cloud API aceess scopes에서 전체 선택

https://github.com/GoogleCloudPlatform/gcsfuse/issues/174

https://github.com/GoogleCloudPlatform/gcsfuse/issues/174

Please check your VM's `Cloud API access scopes` in detail page.
It have to have **Write access** for Storage.
you can change scope after you stop VM



- SSH 접속할 때 필요한 포트들 추가 (하나 넣었을 때 jupyter 접속이 안되어서 두 개 넣음)

gcloud compute ssh --zone=us-central1-a instance-1 -- -L 8888:locahost:8888 -L 8081:localhost:8081



# GCP 마운트

참조: https://cloud.google.com/storage/docs/gcs-fuse

참조: https://cloud.google.com/compute/docs/disks/gcs-buckets?hl=ko

참조: https://medium.com/@antrixsh/how-to-mount-cloud-storage-bucket-with-gcp-compute-engine-ba7c95ad5349

gcsfuse 설치: https://github.com/GoogleCloudPlatform/gcsfuse/blob/master/docs/installing.md

gcloud auth application-default login

- Mount

```bash
gcsfuse {googlebucketname}  {/home/shared/local_folder/}
```

- Unmount

- ```bash
  fusermount -u /home/shared/local_folder/
  ```

Mount/unmout 참조: https://stackoverflow.com/questions/42602356/how-to-unmount-google-bucket-in-linux-created-with-gcsfuse



https://cloud.google.com/compute/docs/disks/gcs-buckets?hl=ko

https://medium.com/@antrixsh/how-to-mount-cloud-storage-bucket-with-gcp-compute-engine-ba7c95ad5349







# Colab backend로 연결

https://medium.com/@senthilnathangautham/colab-gcp-compute-how-to-link-them-together-98747e8d940e

jupyter notebook --NotebookApp.allow_origin='https://colab.research.google.com' --port=8081 --NotebookApp.port_retries=0  --no-browser





