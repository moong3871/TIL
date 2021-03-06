# Git

> Git은 분산 version관리시스템이다.

## 준비하기

윈도우에서 git을 활용하기 위해서 [git bash](https://git-scm.com/downloads)를 설치.

초기 설치를 완료한 이후에, 계정설정을 진행. (sh: shell script, 이를 표현하기 위해 $ 같이 표기)

``` sh
$ git config --global user.email {이메일 주소}
$ git config --global user.name {유저네임}
```

## 로컬 저장소 활용하기

### 1. 저장소 초기화

> = 이제부터 이 디렉토리를 git으로 관리하겠다. (변경 이력을 감시하겠다.)

```sh
$ git init
```

- `.git` 디렉토리가 생성되며, 여기에 git과 관련된 모든 정보가 저장.
- 초기화를 하고나면 git bash에  `(master)`라고 표시가 되는데, 이 디렉토리는 이미 git이 관리하고 있다는 뜻.
- 이미 초기화 한 repo에서는 다시 `git init`을 하지 않습니다.

### 2. add

> working directory 작업공간에서 변경된 사항을 이력으로 관리하기 위해서는 반드시 staging area를 거쳐야 한다.

```sh
$ git add {staging 할 파일}
```



### 3. Commit

> 이력을 확정 짓는, 즉 기록을 남기는 명령어이다.

```sh
$ git commit -m '커밋 메세지'
```

커밋 기록을 확인하고 싶다면 아래의 명령어 참고.

```sh
$ git log
```

### 4. Status

> git을 쓰면서 가장 많이 사용해야 하는 명령어. 

​	 현재 상황을 확인할 수 있다.

```sh
$ git status
```

## 원격 저장소 활용하기

여러 서비스 중, github을 기준으로 설명.

### 1. 준비사항

- github에 회원가입 후, 빈 repo를 만들어 둔다.

### 2. 원격 저장소 등록

- 로컬 저장소와 원격 저장소를 연결하는 일입니다.

```sh
$ git remote add origin { github repo url }
```

- 원격 저장소(remote)를 등록할건데, `origin` 이라는 이름으로 원격 저장소를 등록하겠다. 라는 의미
- 원격 저장소 등록 현황을 확인하려면 아래의 명령어를 참고.

```sh
$ git remote -v
```

<<<<<<< HEAD
- 등록된 원격 저장소를 삭제하려면 아래의 명령어를 참고하세요.
=======
### 4. 원격 저장소에서 로컬로 가져오기

github나 gitlab의 repo주소를 복사해둔 뒤,

``` sh
$ git clone {가져오고자 하는 repo url}
```

>>>>>>> 212757cb36bf993c2d939222e124592d9aab7657

  (git remote -v를 통해 origin과 주소 확인, 아닐 경우 아래의 코드로 origin 삭제)

```sh
$ git remote rm orign {삭제하고자 하는 remote name}
```

​		다시 git remote add origin https://~~(주소 paste)

### 3. 원격 저장소에 업로드

아래의 명령어를 통해 원격 저장소에 commit된 코드를 업로드할 수 있습니다.

```sh
$ git push origin master
```

