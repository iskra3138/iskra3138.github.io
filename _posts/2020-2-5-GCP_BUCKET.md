https://cloud.google.com/storage/docs/quickstart-gsutil?hl=ko

https://cloud.google.com/storage/docs/quickstart-gsutil?hl=ko#make_your_object_publicly_accessible
객체에 공개적으로 액세스하기
gsutil acl ch 명령어를 사용하여 모든 사용자에게 버킷에 저장된 객체에 대한 읽기 권한을 부여합니다.
```
gsutil acl ch -u AllUsers:R gs://my-awesome-bucket/kitten.png
```
성공하면 다음과 같은 결과가 반환됩니다.
```
Updated ACL on gs://my-awesome-bucket/kitten.png
```
이제 누구나 객체에 접근할 수 있습니다.

이 권한을 삭제하려면 다음 명령어를 사용합니다.
```
gsutil acl ch -d AllUsers gs://my-awesome-bucket/kitten.png
```
성공하면 다음과 같은 결과가 반환됩니다.
```
Updated ACL on gs://my-awesome-bucket/kitten.png
```
이 객체 공개 액세스 권한을 삭제했습니다.

참고: 공개 액세스를 삭제한 후에도 일정 기간 동안 여전히 캐시된 버전에 액세스할 수 있습니다.



https://cloud.google.com/storage/docs/access-control/making-data-public#objects

https://cloud.google.com/storage/docs/access-control/making-data-public#buckets
