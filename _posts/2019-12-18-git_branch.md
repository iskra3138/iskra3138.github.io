# git branch 사용법 정리

- branch: 독립적으로 어떤 작업을 진행하기 위한 개념
    - 여러 개발자들이 동시에 다양한 작업을 할 수 있게 지원
    - 필요에 의해 만들어지는 branch는 다른 branch의 영향을 받지 않음

- master branch: Repository를 처음 만들 때 생성되는 branch

- branch 만들기: 사전에 팀원들과 어떻게 만들고 관리할지 상의 필요 (생성/통합시점, 이름 규칙 등)
    - Integration branch(통합 브랜치): 
        - 언제든지 배포할 수 있는 버전을 만들 수 있어야 하는 branch
        - 늘 안정적인 상태(정상적으로 작동하는 상태)를 유지해야 함
        - 버그수정/기능 추가 등은 topic branch를 만들어 수행
        - 일반적으로 'master' branch를 Integration branch로 사용
    - topic branch(토픽 브랜치)
        - 버그수정/기능추가 같은 단위 작업을 위한 branch
        - 여러 개의 작업을 동시에 진행할 때는 그 수만큼 토픽 브랜치 생성
        ```bash
        # branch 만들기
        $ git branch <branch name>
        # branch 삭제하기
        $ git branch -d <branch name>
        # branch 확인하기
        $ git branch
        ##  * 이 붙어있는 것이 현재 선택된 브랜치
        ```
        - Feature branch(피쳐 브랜치)라고 부르기도 함

- branch 전환하기
    - git에서는 항상 작업할 branch를 미리 선택해야 함
    - 'checkout'명령어를 사용하여 원하는 branch로 전환
    ```bash
    # branch 전환하기
    $ git checkout <branch name>
    # branch 생성하면서 전환하기
    $ git checkout -b <branch name>
    ```
    - branch가 전환되면 마지막 commit 내용이 work tree에 펼쳐짐
    - 이 후, 실행한 commit은 전환한 branch에 추가됨

- HEAD: 
    - 현재 사용 중인 branch의 선두 부분을 나타내는 이름
    - 'HEAD'를 이동하면 사용하는 branch가 변경됨
    - ~(틸드) 기호와 숫자를 'HEAD'뒤에 붙여 몇 세대 앞의 commit을 가리킬 수 있음
    - ^(캐럿)은 branch 병합에서 원본이 여럿 있는 경우 몇 번째 원본인지를 지정할 수 있음
    <img src="/_posts/HEAD.jpg" width="70%" height="70%" title="" alt=""></img>

- stash
    - commit하지 않은 변경 내용이나 새롭게 추가한 파일이 index와 work tree에 남아 있는 채로 다른 branch로 전환(checkout)하면, 기존 branch가 아닌 전환된 branch에서 commit할 수 있음
    - 단, commit 가능한 변경 내용 중에 전환된 branch에서도 한 차례 변경이 되어 있는 경우에는 checkout에 실패할 수 있음. 이 경우, 이전 branch에서 commit하지 않은 변경 내용을 commit하거나 stash를 이용해 일시적으로 변경 내용을 다른 곳에 저장하여 충돌을 피하게 한 뒤 checkout을 해야 함
    - stash는 파일의 변경 내용을 일시적으로 기록해두는 영역
    - stash를 사용하여 work tree와 index 내에 아직 commit하지 않은 변경을 일시적으로 저장할 수 있음
    - stash에 저장된 변경 내용은 나중에 다시 불러와 원래의 branch나 다른 branch에 commit할 수 있음
    - stash 사용법 참고: <https://wit.nts-corp.com/2014/03/25/1153>

- branch 통합하기
    - 작업이 완료된 topic branch는 최종적으로 integration branch에 병합
    - 통합에는 'merge'를 사용하는 방법과 'rebase'를 사용하는 방법 2가지가 있음
    ```bash
    # merge
    $ git merge <branch name>
    # rebase
    $ $ git rebase <branch name>
    ## rebase에서 충돌이 났다면, commit이 아니라 
    ## rebase에 --continue 옵션 추가
    ## rebase를 취소할 거면 --abort 옵션 추가
    $ git add <conflict file>
    $ git rebase --continue
    ```
    - merge
        - master에서 topic branch로 분기한 후, master는 변화가 없다면 fast-forward 병합해서 Commit history가 동기화됨
            - non fast-forward 옵션을 통해 각각의 history를 별도로 관리할 수도 있음
        - master에 변경사항이 발생한 후 병합하면, non-fast-forward 병합해서 각각의 Commit history를 유지함
    - rebase
        - topic branch를 master에 rebase하면, topic branch의 history가 master branch 뒤로 이동해서 하나의 history같이 됨
        - 이 때, mater의 위치는 topic 앞쪽이 되므로, fast-forward 병합을 통해 위치를 변경할 수 있음
    - merge의 경우 변경 이력이 모두 그래도 남아 있으나, 이력이 복잡해지게 되고, rebase의 경우 이력은 단순해지지만, 원래의 commit이력이 변경됨, 정확한 이력을 남겨야 할 필요가 있을 때는 사용하지 않음 

- Tag
    - Commit을 참조하기 쉽도록 알기 쉬운 이름을 붙이는 것
    - 한 번 붙인 Tag는 branch처럼 위치가 이동하지 않고 고정됨
    - Git에서는 이름 정보만을 갖는 태그(Lightweight tag)와 보다 상세한 정보를 포함하는 주석 태그(Annotated tag) 두 가지를 사용할 수 있음
        - 일반 태그(Lightweight tag)
            - 이름만 붙일 수 있음
        - 주석 태그(Annotated tag)
            - 이름을 붙일 수 있음
            - 태그에 대한 설명도 포함할 수 있음
            - 서명도 넣을 수 있음
            - 태그를 만든 사람의 이름, 이메일, 날짜 정보도 포함시킬 수 있음
        - 보통 Release branch에는 주석 태그를 사용하고, 로컬에서 일시적으로 사용하는 topic branch에서는 일반 태그를 사용
        - 태그 이름만으로 checkout, reset 하여 과거 상태로 돌릴 수 있음
    ```bash
    # 일반 tag 추가하기
    $ git tag <tagname>
    # 주석 tag 추가하기
    $ git tag -a <tagname>
    # 주석을 한번에 추가하기
    $ git tag -am "주석" <tagname>
    # tag 목록 보기
    $ git tag
    # tag 목록과 주석을 같이 보기
    $ git tag -n
    # log 목록에서 tag 포함하여 보기
    $ git log --decorate
    # tag 삭제하기
    $ git tag -d <tagname>
    ```
- Commit 변경
    - 수정
        - --amend 옵션을 통해 이전에 커밋했던 내용에 새로운 내용을 추가하거나 message를 수정할 수 있음
        ```bash
        # file 수정 후 or Message만 변경할 거면 수정 없이
        ## 현재의 commit을 덮어 씀
        $ git commit --amend
        ```
    - 삭제 
        - revert 명령어를 통해 특정 commit의 내용을 삭제할 수 있음 (history가 남음)
        ```bash
        $ git revert HEAD
        ```
    - 복원 
        - reset 명령어를 이용하면 더 이상 필요 없어진 커밋들을 버릴 수 있음 (history가 같이 사라짐)
        - 모드에 따라 'HEAD'위치와 index, working tree 내용을 함께 복원할지도 선택 (mixed가 기본)
            - soft: HEAD 위치 (변경), index(변경안함), Working Tree(변경 안함)
            - mixed: HEAD 위치 (변경), index(변경), Working Tree(변경 안함)
            - hard: HEAD 위치 (변경), index(변경), Working Tree(변경)
        ```bash
        $ git reset --hard HEAD~~
        ```
        - reset 전의 커밋은 'ORIG_HEAD'라는 이름으로 참조할 수 있음. 실수로 reset했을 때 사용
        ```bash
        $ git reset --hard ORIG_HEAD
        ```
    - 삽입
        - cherry-pick을 이용하면 다른 branch의 commit을 현재 branch로 가져올 수 있음
        ```bash
        $ git cherry-pick <commit>         
        ```
    - 편집
        - rebase 명령에 i 옵션을 지정하면 
            - commit을 다시 쓰거나 
            - 다른 commit과 바꿔 넣거나
            - 특정 위치의 commit을 삭제하거나
            - 여러 commit을 하나로 통합
        - push하기 전에 이전 커밋 내용을 정리하고 싶거나, 여러 개를 하나로 묶는 게 이해하기 편할 때나, 이전 커밋에 누락된 파일들을 나중에 추가하고자 할 때 적용
        ```bash
        # commit 모두 통합하기
        $ git rebase -i HEAD~~
        ## 텍스트 에디터가 열리면 마지막 commit의 pick을 squash로 변경하고 저장
        ### pick <commit> <message>
        ### pick ...
        ### pick <commit> <message> <- pick을 squash로 변경
        ```
        ```bash
        # commit 수정하기
        $ git rebase -i HEAD~~
        ## 텍스트 에디터가 열리면 수정할 commit의 pick을 edit로 변경하고 저장
        ### pick <commit> <message> <- pick을 edit로 변경
        ### pick ...
        ### pick <commit> <message> 

        # 수정작업 진행 및 저장
        $ git add .
        $ git commit --amend
        $ git rebase --continue
        ## 충돌이 발생하면 수정한 후 git add . && git rebase --continue
        ## 도중에 rebase 작업을 중지할 경우 git rebase --abort
        ```
        - rebase 전의 커밋은 'ORIG_HEAD'라는 이름으로 참조할 수 있음. 이전 상태로 되돌리고 싶으면,
        ```bash
        $ git reset --hard ORIG_HEAD
        ```

        

    - 통합
        - --squash 옵션을 통해 브랜지를 병합하면 해당 브렌치의 커밋 전체를 통합한 커밋이 추가됨
        ```bash
        $ git merge --squash <branch name>
        # 충돌이 발생하면, 수정한 후 git add . && git commit
        ```

REF: <https://backlog.com/git-tutorial/kr/stepup/stepup1_1.html>





