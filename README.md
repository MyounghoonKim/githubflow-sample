# githubflow sample

## 준비사항

### git aliases
```
alias gs='git status'
alias gl='git pull'
alias gd='git diff'
alias gdc='git diff --cached'
alias gcf='git commit --fixup'
alias gria='git rebase -i --autosquash'
alias ga='git add '
alias gc='git commit -v'
alias gb='git branch -a'
alias gco='git checkout'
alias gcob='git checkout -b'
alias gcot='git checkout -t'
alias gcotb='git checkout --track -b'
alias gh='git log --pretty=format:"%h %s" --graph --min-parents=2' #history
alias ghut='git log --pretty=format:"%h %s [%an at %aI]" --graph--min-parents=2' # history user and time
alias ghd='git log --pretty=format:"%h %s" --graph' #history detail
alias ghdut='git log --pretty=format:"%h %s [%an at %aI]" --graph' #history detail user and time
```

### 미리 읽으면 도움이 되는 글
- https://blog.outsider.ne.kr/865 (한글)
- https://ujuc.github.io/2015/12/16/git-flow-github-flow-gitlab-flow/ (한글)
- http://scottchacon.com/2011/08/31/github-flow.html (영어)

## Fork
- 메인 원격 저장소를 Fork하여 내 원격 저장소에 복사본을 만듬
- github이나 bitbucket에서 웹 ui로 제공함

## Clone
- 내 원격 저장소의 코드를 로컬 저장소로 복사
- eg) `$ git clone https://github.com/[somebody]/githubflow-sample.git`

## 이메일 등록
- github이나 bitbucket에 들어있는 이메일 등록
- 각 사이트에서 여러 개의 이메일을 등록할 수 있음
```
$ git config user.email myounghoon.kim@gmail.com
$ git config user.email
myounghoon.kim@gmail.com
```

## Fetch
- 메인 원격저장소를 등록하여 모든 branch를 fetch
```
$ git remote add main https://github.com/MyounghoonKim/githubflow-sample.git
$ git remote -v
main  https://github.com/MyounghoonKim/githubflow-sample.git (fetch)
main  https://github.com/MyounghoonKim/githubflow-sample.git (push)
origin  https://github.com/[somebody]/githubflow-sample.git (fetch)
origin  https://github.com/[somebody]/githubflow-sample.git (push)
$ git fetch main

 # sample commit message
$ ghd
*   f8210f6 Merge branch 'auth'
|\
| * ef821e4 update api
| * 103b70d add user auth
|/
* fb8cc1a init commit
```

## 소스코드 수정
### Feature branch 생성
- 작업은 피쳐 단위
- 설명적 브랜치 네이밍(eg. svg-tests, wild-renaming)
- 예를 들어 결제 관련 작업을 한다면 다음과 같이 브랜치를 생성
- `$ gco -b infra-payment`
- 이제 `infra-payment` 브랜치에서 작업

### 커밋 & 푸시
- 작업 후 커밋
```
 # sample commit message
$ ghd
* 1005e94 update payment api
* 03ac2ea add creditcard classifier
*   f8210f6 Merge branch 'auth'
|\
| * ef821e4 update api
| * 103b70d add user auth
|/
* fb8cc1a init commit
```
- 커밋로그 작성시 다음 링크 참조: https://item4.github.io/2016-11-01/How-to-Write-a-Git-Commit-Message/
- 요약하면 If applied, this commit will ***your subject line here***
- 예를 들면
  - If applied, this commit will ***refactor subsystem X for readability***
  - If applied, this commit will ***update getting started documentation***
- 푸시는 자주 하는 게 좋음

## Pull Request
- 리뷰 및 피드백을 위해 Pull Request 전송(web ui)

## 메인 원격저장소를 다시 Fetch
- PR이 accept되면 업데이트된 메인 원격저장소를 바탕으로 개인 로컬저장소/원격저장소를 업데이트
```
$ git fetch main
$ ghd
*   22983c4 Merge pull request #1 from lumcontributor/infra-payment
|\
| * 1005e94 update payment api
| * 03ac2ea add creditcard classifier
|/
*   f8210f6 Merge branch 'auth'
|\
| * ef821e4 update api
| * 103b70d add user auth
|/
* fb8cc1a init commit
$ gco master
$ git merge main/master
$ git push origin master
```