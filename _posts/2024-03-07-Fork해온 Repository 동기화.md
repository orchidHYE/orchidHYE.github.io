---
layout: post
title: Fork해온 Repository 동기화
date: 2024-03-07 14:59 +0900
categories:
  - Git
tags: 
math: true
---
# **잔디가 심어지기 위한 조건**


1. GitHub 계정과 commit한 이메일이 동일해야 한다.
2. Fork한 repository가 아닌 개인 repository에서 commit해야 한다.

- **2번 같은 경우, Fork해온 repository에서 commit 후 Pull Request까지 해야만 잔디가 심어지는데
나는 Pull Request를 보낼 수 없는 상황이었다.**


# **해결 방법**

#### **bare와 mirror 옵션 사용하기**

1. GitHub에서 새 repository 생성
2. 프로젝트 파일을 관리하는 곳에서 터미널 실행
3. 원본 repository를 bare clone<br/>
	 `$ git clone --bare https://github.com/exampleuser/origin-repo.git`
4. 새 repository로 mirror push<br/>
	 `$ cd origin-repo.git`<br/>
	 `$ git push --mirror https://github.com/exampleuser/new-repo.git`
5. bare clone했던 local repository 삭제<br/>
	 `$ cd ..`<br/>
	 `$ rm -rf origin-repo.git`

**위와 같은 명령어를 통해 안보였던 잔디가 정상적으로 보여지게 됐다.**

그럼 여기서 bare / mirror가 뭐길래 안보였던 잔디가 보이는 걸까.

# **--bare**
- 로컬 저장소에 Git repository를 bare로 만든다.
	- 일반적인 repository는 working tree와 .git으로 구성된다.
	- working tree에는 실제 파일들이 존재하고, .git에는 Git 객체 데이터(object)와 메타 데이터(refs등)가 저장된다.
	- bare 옵션을 사용한 repository는 working tree 없이 오직 Git 객체 데이터(object)와 메타 데이터(refs등)만을 포함한다.
- 이는 내부적으로 Git이 `$GIT_DIR`을 사용하여 작업하기 때문이다.

# **--mirror**
- 원본 repository의 모든 refs 정보를, 타겟 repository에 복사한다.
- 이는 원격 브랜치, 태그, 풀 리퀘스트 등을 모두 포함한다.
- 이를 통해 타겟 repository는 원본 repository 간의 참조(refs) 정보의 동기화가 이루어진다 
	- (== git remote update를 실행함으로써 refspec 구성을 설정한다.)



`*refs: Git에서 사용되는 참조 정보를 뜻한다. refs를 사용하여 커밋, 브랜치, 태그등을 추적하고 관리한다. GitHub의 refs는 일반적으로 'refs/heads', 'refs/tags' 'refs/pull'등과 같은 형식으로 표현된다.`

`*$GIT_DIR: .git을 가리키는 환경 변수이다. 이를 사용하여 Git이 작업 중인 repository의 정보를 읽고 쓸 수 있다.`
