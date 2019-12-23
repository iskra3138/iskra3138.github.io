### 원격 terminal 창을 닫아도 계속 실행되도록 command를 실행하는 방법
```bash
$ nohup {실행할 command} > {로그파일} &
```
- nohup : terminal 창을 닫아도 계속 실행
- '> {로그파일}' : 실행한 command의 출력을 해당 로그파일에 기록
- & : background job으로 실행
- eg. nohup ./train.sh > ./log191223.log & 
