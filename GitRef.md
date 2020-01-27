# 참고사항

### Git

```shell
> git config --global user.name "이름"
> git config --global user.email "깃허브 메일주소"


> git init  // 깃 명령어를 사용할 수 있는 디렉토리로 만든다.
> git status
> git add 파일
> git add .
> git commit -m '설명'

> git remote add origin https://github.com/username/myproject.git // 로컬과 원격 저장소를 연결
> git remote -v // 연결상태 확인
> git push origin master

> git rm -r --cached name
> git commit -m ""
> git push origin master

> git clone /로컬/저장소/경로

> git clone 사용자명@호스트:/원격/저장소/경로  // 원격 서버의 저장소를 복제
```



### 브랜치

```shell
> git switch -c brach_name
> git add .
> git commit -m "commit"
> git push origin branch_name
> git checkout master
> git merge branch_name
> git branch -d branch_name
```



requirements.txt에 있는 것들 모두 install

```shell
$ pip install -r requirements.txt 
```



