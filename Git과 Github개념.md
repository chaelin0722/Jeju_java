**1. Git과 Github개념**

먼저 Git은 버전 관리 툴이며, Github은 웹 상에 소스 코드를 올려서 여러 사람과 공유하는 장소입니다.

자신의 PC에서 작업하는 공간을 Local Repository라 하며, Github에 있는 공간을 Remote Repository라 하는데,

Git에 대한 자세한 개념은 [여기](https://victorydntmd.tistory.com/72)를 참고해주세요!



윈도우, 리눅스 등에서 git을 사용하려면 git이 먼저 설치되어 있어야 합니다. ( [링](https://git-scm.com/downloads)[크](https://git-scm.com/downloads) )



**2. 기본 명령어**

- git init

- - 새로운 local repository 생성

- git add

- - 변경된 파일을 storage에 추가

- git commit

- - add한 파일을 local repository에 저장 

- git push

- - local repository를 remote repository에 업로드





**3. Github에 소스코드 올리기**

**1) 레포지토리 생성**

Github 홈페이지( [링크](https://github.com/) )에서 회원 가입을 한 후 repository를 생성합니다.

( repository를 생성한 후 **readme.md**를 읽어보시면 앞으로 소개할 내용이 나와있습니다. )





**2) 업로드할 폴더로 이동**

커맨더 창을 통해, 깃헙에 업로드할 파일이 있는 폴더로 이동합니다.

```
# cd 폴더경로
```





**3) init**

커맨더 창에서 아래의 명령어를 통해, 위의 폴더를 git이 추적할 수 있도록 **.git 폴더**를 생성합니다.

즉, local repository를 생성하는 것입니다.

```
# git init
```





**4) 상태 확인**

git이 버전관리 대상 파일들의 상태를 파악합니다.

```
# git status
```

git status는 매우매우 유용한 명령어입니다.

- 명령어가 동작하지 않을 때 에러 확인
- 내가 작업한 파일 외에 다른 파일이 수정되진 않았는지 확인





**5) add**

버전 관리할 파일들을 추가합니다.

git add 파일 명령어는 특정 파일을 추가하는 명령어이며,  아래의 명령어는 변경 모든 파일을 local repository에 추가하는 명령어입니다.

```
# git add .
```





**6) 커밋**

commit 메시지를 작성합니다.

```
# git commit -m "메시지내용"
```

-m 옵션은 간단하게 한줄로 메시지를 작성하기 위함이며, 긴 메시지 작성이 필요하다면 git commit 명령어만 실행하면 됩니다.







**7) remote 등록**

remote repository를 등록합니다.

```
# git remote add origin {remote repository 주소}
```

origin은 remote repository의 별칭을 의미하며, 매 번 remote repository의 주소를 입력하는 것이 귀찮으므로 별칭을 사용합니다.

일반적으로 origin을 사용합니다.



repository의 주소는 본인의 github 주소를 입력하면 되는데, 아래 사진처럼 HTTPS를 한 후, 복사를 클릭하면 주소를 복사할 수 있습니다.



![img](https://t1.daumcdn.net/cfile/tistory/99DC58335A1520B41D)







**8) push**

commit 한 내용을 remote repository에 push( 업로드 ) 합니다.

```
# git push origin master
```

master는 브랜치( branch )의 이름이며, remote repository를 생성하면 기본적으로 master 브랜치가 생성됩니다.

( 참고로 브랜치는 독립적인 작업 공간을 의미하며, 브랜치 덕분에 협업이 수월해지기 때문에 꼭 알아둬야 하는 개념입니다. )



master가 아닌 다른 branch로 push 하고 싶으면, 아래와 같이 master를 특정 브랜치명으로 바꿔서 명령어를 실행하면 됩니다.

```
# git push origin {브랜치명}
```





**9) config 설정**

git을 설치한 후 특별한 설정을 하지 않았다면, **Github 이메일 주소** 및 **비밀번호**를 입력하라고 합니다.

이메일 주소와 비밀번호를 입력하면 소스 코드가 Github으로 푸시가 잘 되는 것을 확인할 수 있습니다.



**4. 작업한 코드 올리기**

위의 과정은 처음 깃헙에 코드를 올릴 때의 과정입니다.

이제 작업을 진행하면서 수정된 내용을 계속 깃헙에 업로드를 해야 하는데, 첫 push 이후에는 위의 과정을 조금 생략할 수 있습니다.



커맨더 창에서 소스코드가 있는 폴더로 이동한 후, 아래의 명령어를 실행합니다.

```
# git add .# git commit -m "메시지 내용"# git push origin {브랜치명}
```

