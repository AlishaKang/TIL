# basic command
> git 기본 문법 정리

## 초기 설정
- git을 설치 후 한 번만 진행
```bash
git config -- global user.email <이메일>
git config -- global user.name <이름> 
```

## git 저장소 만들기

- `git init`
    - `.git directory`를 생성해주는 명령어
    - 관리하고 싶은 최상위 위치에서 실행

## git 상태 체크

- `status`
    - 현재 git으로 관리되고있는 파일/폴더의 상태를 출력

## 코드 수정하고 저장소에 저장하기

- `add`
    - `git add <파일/폴더이름>`
    - working directory에서 `staging area`로 추가
    - 일반적으로 모든 파일, 폴더를 추가하기 위해 아래의 코드를 사용
        - `git add .`

- `commit`
    - `git commit -m "메세지"`
    - `staging area`에 올라간 파일들의 스냅샷을 찍어서 `.git directory`에 저장
    - 일반적으로 `-m` 옵션을 넣어서 메세지를 추가하여 등록
    
## 원격저장소에 업로드하기

- `remote add`
    - `git remote add origin <URL>`
    - 원격저장소 주소를 origin 이라는 이름으로 저장

- `push`
    - `git push <원격저장소이름> <브랜치이름>`
    - 원격저장소에 브랜치를 업로드

    add . > commit > push

## 원격저장소 Github에 업로드/다운하기

- Github에 업로드
```
git add .
git commit -m "변경사항메세지"
git push origin master
```
- Github에서 다운로드
```
git pull origin master
```

## 두 사람이 같은 파일의 같은 부분을 수정해 marging이 발생한 경우

- Github는 두 사람이 동시에 수정을 할 수 없다. 만약 두 사람이 한 파일을 동시에 수정을 할 경우, A사람의 파일과 B사람의 파일로 두 개의 파일이 생긴다. 그럼 marging하다가 겹친 부분에 Visual SC는 버튼들을 보여준다. 이 중에서 자신이 원하는 수정을 고르면 된다.
Accept Current Change / Accept Incoming Change ...etc

## Branch를 만드는 명령어
- master 또는 main branch는 모두에게 보여지는 곳이니 또다른 branch를 만들어서 작업을 할 수 있다.
```
git branch -c 브랜치명
```
- 만들어낸 브랜치로 들어가고 싶은 경우
```
git switch 브랜치명
```

## Branch를 Github에 올리기
Github에서 Pull request버튼 > New pull request > 원하는 Branch 선택

## 원격저장소Github에서 클론 코딩을 만들어 가져오기
- Code 클릭 > Local에서 코딩 복사 > 원하는 폴더의 빈공간에서 우클릭으로 터미널을 열어 
`git clone 코딩복붙`