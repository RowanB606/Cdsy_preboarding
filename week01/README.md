# Week 01: 개발 워크스테이션 구축 - Docker 기초 및 웹서버 컨테이너화

## 1. 기술 문서

### 1-1. 프로젝트 개요
리눅스 CLI, Docker, Git/GitHub를 사용하여 개발 워크스테이션을 구축한다.
Docker를 설치하고, 커스텀 웹 서버 이미지를 만들어 포트 매핑, 볼륨 관리를 실습한다.

### 1-2. 실행 환경
- OS: macOS Sequoia v15.7.4
- Docker Version: [나중에 기록]
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

## 2. 터미널 조작 로그

### 2-1. 현재 위치 및 디렉토리 생성/이동
```text
% pwd
/Users/rok-dam0029

% mkdir -p Cdsy_preboarding/week01
% cd Cdsy_preboarding/week01
% pwd
/Users/rok-dam0029/Cdsy_preboarding/week01
```

### 2-2. 빈 파일 생성/수정/내용확인
```text
% touch README.md
% echo "# Week 01: 개발 워크스테이션 구축 - Docker 기초 및 웹서버 컨테이너화" > README.md
% cat README.md
# Week 01: 개발 워크스테이션 구축 - Docker 기초 및 웹서버 컨테이너화
```

### 2-3. 파일 복사/이동/이름변경/삭제
```text
% pwc
/Users/rok-dam0029/Cdsy_preboarding/week01
% ls
README.md
% cp README.md README_copy.md                      # 파일 복사
% ls
README.md	README_copy.md

% mv README_copy.md ../                            # 파일 이동(복사본을 상위폴더로 이동)
% ls
README.md
% cd ..
% pwd
/Users/rok-dam0029/Cdsy_preboarding
% ls
README_copy.md	week01

% mv README_copy.md "README(2).md"                   # 파일 이름변경(괄호를 특수문자로 인식하여 "" 사용)
% ls
README(2).md	week01

% rm "README(2).md"                                  # 파일 삭제
% ls
week01
```

## 3. 권한 실습 및 증거 기록


## 4. Docker 설치 및 기본 점검


## 5. Docker 기본 운영 명령 수행


## 6. 컨테이너 실행 실습


## 7. 기존 Dockerfile 기반 커스텀 이미지 제작


## 8. 포트 매핑 및 접속 증거


## 9. Docker 볼륨 영속성 검증


## 10. Git 설정 및 GitHub 연동

