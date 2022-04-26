# 깃허브  정리

# `branch`

branch 란 여러 개발자들이 동시에 다양한 작업을 할 수 있게 만들어 주는 기능이다

독립적으로 어떤 작업을 진행하기 위한 개념으로 필요에 의해 만들어지는 각각의 branch 는 다른 branch 의 영향을 받지 않기 때문에, 여러 작업을 동시에 진행할 수 있다

개발자1 과 개발자2 가 있을때 두사람이 서로 코드를 공유하여 작업하는 경우 해당 작업에서 각각 코드를 작성 하여도 하나의 프로젝트로 구성할수 있도록 도와준다. 

- ps. 저장소를 처음 만들면, Git 은 바로 'master' 라는 이름의 branch 를 만들어 두눈데 이 새로운 저장소에 새로운 파일을 추가 한다거나 추가한 파일의 내용을 변경하여 그 내용을 저장(커밋, Commit)하는 것은 모두 'master' 라는 이름의 branch 를 통해 처리할 수 있는 일이다.

## branch 만들기

people 라는 브랜치 를 만들고 확인해 보자!

```jsx
// 브랜치 만들기
$ git branch people

//브랜치 확인하기
$ git branch
  people
* master
```

`git branch <branch>` branch 에 내가 넣고자 하는 브랜치의 이름을 넣으면 브랜치가 만들어 진다.

`git branch` 를 입력 하면 생성 되어 있는 브랜치를 확인 할수 있다.

- * 은 현재 활성화 되어 있는 브랜치를 뜻 한다.

## branch 전환하기

people 라는 브랜치 로 전환해 보자

```jsx
// 브랜치 전환하기
$ git checkout people
```

<aside>
💡 `$ git checkout -b <branch>` 을 사용할 경우  브랜치를 만듬과 동시에 전환 할수 있다.

</aside>

## 깃에 파일 올리는 방법

`$ git init`
현재 프로젝트에서 변경사항 추적(버전 관리)을 시작

`$ git add index.html`
변경사항을 추적할 특정 파일(index.html)을 지정할때 사용

`$ git status`

변경된 파일을 보여준다.

`$ git add .` 

모든 파일의 변경사항을 추적하도록 지정

`$ git status`

add . 가 잘 진행 되었는지 확인하는 과정으로 (붉은색에서 초록색으로 바뀌면 잘 된것이다.

`$ git commit -m '프로젝트 생성'`
메시지(-m)와 함께 버전을 생성.

- ex) git commit -m 'Start project'

`$ git log` 

변경된 log를 확인 한다.

`$ git push origin master`
*origin 이란 별칭의 원격 저장소로 버전 내역 전송*

업로드가 완료 된다.

# branch 병합하기

브랜치 병합은 `$ git merge <commit>` 명령어로 실행한다. 이 명령어에 병합할 commit 이름을 넣어 실행하면, 지정한 commit 의 변경사항을 가리키고 있는 브랜치에 넣어진다.(브랜치를 합치는 방법)

```jsx
// 마스터 브랜치에서 진행
$ git checkout master

// people 브랜치가 변경후 업로드한 issue1을 가져온다.
$ git merge issue1
```

ex) `merge` 예시

원본 file / git.txt

안녕 나는 `merge` 야

수정된 file / git.txt

안녕 나는 `merge` 야

나는 병합을 위한 명령어로 사용 되고 있어.

'master' 브랜치가 가리키는 커밋이 'people'과 같은 위치로 이동했다. (people와 master의 파일이 같아졌다.)

이런 방식의 병합을 'fast-forward (빨리감기) 병합'이라고 한다.

*** 윗 내용에 대해서는 추가 블로그를 작성 할 예정이다.

## branch 삭제하기

`$ **git branch -d people**`

people 라는 브랜치를 삭제하는 방법으로 다른 브랜치를 삭제하고자 한다면 네임을 바꾸면 된다.

## branch 동시 작업

```jsx
// 브랜치를 2개 만들고 각각 파일을 만들어 커밋한다.
$ git branch issue2
$ git branch issue3

$ git checkout issue2
$ git add L_file.txt
$ git commit -m "commit"

$ git checkout issue3
$ git add L_file.txt
$ git commit -m "설명 추가"
```

각각 같은 이름이지만 다른 내용의 파일을 만들어서 작업을 한 내용이다.

이후 브랜치를 master 와 병합 하게 되는데

issue2를 한후 issue3 를 진행한다고 가정 했을때 issue3에서 충돌이 생기는 것을 확인할수 있다.

```
$git merge issue3
Auto-merging L_file.txt
CONFLICT (content): Merge conflict in myfile.txt
Automatic merge failed; fix conflicts and then commit the result.
```

라는 에러 메세지가 뜨는데 이는 각각에 이름이 같은 파일에 다른내용이 같은 행에 존재하기 때문이다.

이경우 충돌된 부분을 확인하여 code를 수정하고

다시 커밋 하여 브랜치를 병합해주면 된다. 이와 같은 방식을 'non fast-forward 병합’이라고 한다.

연습해보자
