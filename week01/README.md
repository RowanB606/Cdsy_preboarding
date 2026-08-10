# Week 01: 개발 워크스테이션 구축 - Docker 기초 및 웹서버 컨테이너화

## 1. 기술 문서

### 1-1. 프로젝트 개요
리눅스 CLI, Docker, Git/GitHub를 사용하여 개발 워크스테이션을 구축한다.
Docker를 설치하고, 커스텀 웹 서버 이미지를 만들어 포트 매핑, 볼륨 관리를 실습한다.

### 1-2. 실행 환경
- OS: macOS Sequoia v15.7.4
- Docker Version: 29.4.0
- Git Version: [나중에 기록]

### 1-3. 수행 항목 체크리스트
- [ ] 터미널 조작 로그 기록(파일/폴더)
- [ ] 권한 관리 (chmod)
- [ ] Docker 설치 및 점검
- [ ] Docker 기본 운영
- [ ] 커스텀 Dockerfile 작성
- [ ] 포트 매핑 검증
- [ ] 볼륨 영속성 검증
- [ ] Git/GitHub 연동

## 2. 터미널 기초

### 2-1. 현재 위치 및 디렉토리 생성/이동
- 현재 위치 확인
```text
pwd
```
[2-1-(1). 출력화면](./docs/02.%20터미널%20기초/2-1-(1).md)

- 디렉토리 생성/이동
```text
mkdir -p Cdsy_preboarding/week01
cd Cdsy_preboarding/week01
pwd
```
[2-1-(2). 출력화면](./docs/02.%20터미널%20기초/2-1-(2).md)

### 2-2. 빈 파일 생성/수정/내용확인
- 빈 파일 생성
- 파일 내용 수정
- 파일 내용 확인
```text
touch README.md
echo "# Week 01: 개발 워크스테이션 구축 - Docker 기초 및 웹서버 컨테이너화" > README.md
cat README.md
```
[2-2. 출력화면](./docs/02.%20터미널%20기초/2-2.md)

### 2-3. 파일 복사/이동/이름변경/삭제
- 디렉토뢰/파일 목록 확인
```text
pwc
ls
```
[2-3-(1). 출력화면](./docs/02.%20터미널%20기초/2-3-(1).md)

- README.md 파일을 README_copy.md 이름으로 복사
```text
cp README.md README_copy.md
ls
```
[2-3-(2). 출력화면](./docs/02.%20터미널%20기초/2-3-(2).md)

- README_copy.md 파일 이동
```text
mv README_copy.md ../                            # 복사본을 상위폴더로 이동
ls

cd ..
pwd

ls
```
[2-3-(3). 출력화면](./docs/02.%20터미널%20기초/2-3-(3).md)

- 파일 이름 변경
```text
mv README_copy.md "README(2).md"
# 괄호를 특수문자로 인식하기 때문에 "" 사용
ls
```
[2-3-(4). 출력화면](./docs/02.%20터미널%20기초/2-3-(4).md)

- 파일 삭제
```text
rm "README(2).md"
ls
```
[2-3-(5). 출력화면](./docs/02.%20터미널%20기초/2-3-(5).md)

### 2-4. GitHub 업로드(동기화)
- Git 초기화
```text
git init
```
[2-4-(1). 출력화면](./docs/02.%20터미널%20기초/2-4-(1).md)

- Git 레포지토리 목록에 신규 주소 등록 & Commit 대상 등록
```text
git remote add origin https://github.com/RowanB606/Cdsy_preboarding.git
git add .
git status                                       # git 현재 상태 확인
```
[2-4-(2). 출력화면](./docs/02.%20터미널%20기초/2-4-(2).md)

- Git Commit
```text
git commit -m "Commit #01 - New"

git status                                       # git 현재 상태 확인
```
[2-4-(3). 출력화면](./docs/02.%20터미널%20기초/2-4-(3).md)

- Branch 이름 "main"으로 강제 변경
```text
git branch -M main
```

- GitHub origin 주소의 main branch에 업로드(push) 
```text
git push -u origin main
```
[2-4-(4). 출력화면](./docs/02.%20터미널%20기초/2-4-(4).md)

- 디렉토리 내용 확인
```text
pwd

ls -la
# -l: long format 형식으로 표시
# -a: 숨김 파일까지 모두(all) 표시
```
[2-4-(5). 출력화면](./docs/02.%20터미널%20기초/2-4-(5).md)

## 3. 권한 실습 및 증거 기록

### 3-1. 권한 변경 전
- Auth 디렉토리 생성
```text
cd week01
pwd

mkdir Auth
ls -la
```
[3-1. 출력화면](./docs/02.%20터미널%20기초/3-1.md)

### 3-2. 권한 변경 - 8진수 표기법(절대모드)
```text
chmod 777 Auth
chmod 000 test.txt
ls -la
```
[3-2. 출력화면](./docs/02.%20터미널%20기초/3-2.md)

### 3-3. 권한 변경(2) - 기호 표기법(상대모드)
```text
chmod go-w Auth
chmod u+rw,go=r test.txt
ls -la

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ(r=읽기, w=쓰기, x=실행, -=권한없음)ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
|    7 : rwx    |    u : 소유자        |    + : 권한추가         |
|    6 : rw-    |    g : 그룹         |    - : 권한제거          |
|    5 : r-x    |    o : 기타사용자     |    = : 지정값으로 설정    |
|    4 : 4--    |    a : 모두(all)    |                       |
|    0 : ---    |                    |                       |
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
```
[3-3. 출력화면](./docs/02.%20터미널%20기초/3-3.md)

## 4. Docker 설치 및 기본 점검
### 4-1. Docker 버전 확인
```text
docker --version
```
[4-1. 출력화면](./docs/02.%20터미널%20기초/4-1.md)

### 4-2. Docker Daemon 동작 여부 확인
```text
# Docker Desktop 대신 OrbStack 실행

docker info
```
[4-2. 출력화면](./docs/02.%20터미널%20기초/4-2.md)
[출력 결과 보기](./4-2.출력.md)

## 5. Docker 기본 운영 명령 수행
### 5-1. 이미지 다운로드 및 목록 확인
- 이미지 목록 확인
```text
docker images
```

- 이미지 다운로드
```text
docker pull busybox:latest
```

- 이미지 목록 확인
```text
docker images
```
[5-1. 출력화면](./docs/02.%20터미널%20기초/5-1.md)

### 5-2. 컨테이너 다운로드 및 목록 확인
### 5-3. 로그 확인
### 5-4. 리소스 확인

## 6. 컨테이너 실행 실습


## 7. 기존 Dockerfile 기반 커스텀 이미지 제작


## 8. 포트 매핑 및 접속 증거


## 9. Docker 볼륨 영속성 검증


## 10. Git 설정 및 GitHub 연동

