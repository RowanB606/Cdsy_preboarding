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

## 2. 터미널 조작 로그

### 2-1. 현재 위치 및 디렉토리 생성/이동
```text
# 현재 위치 확인
pwd
===[출력]==================
| /Users/rok-dam0029     |
==========================

# 디렉토리 생성/이동
mkdir -p Cdsy_preboarding/week01
cd Cdsy_preboarding/week01
pwd
===[출력]=======================================
| /Users/rok-dam0029/Cdsy_preboarding/week01  |
===============================================
```

### 2-2. 빈 파일 생성/수정/내용확인
```text
touch README.md
% echo "# Week 01: 개발 워크스테이션 구축 - Docker 기초 및 웹서버 컨테이너화" > README.md
% cat README.md
===[출력]=====================================================
| # Week 01: 개발 워크스테이션 구축 - Docker 기초 및 웹서버 컨테이너화  |
=============================================================
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

% mv README_copy.md "README(2).md"                 # 파일 이름변경(괄호를 특수문자로 인식하여 "" 사용)
% ls
README(2).md	week01

% rm "README(2).md"                                # 파일 삭제
% ls
week01
```

### 2-4. GitHub 업로드(동기화)
```text
% git init
/Users/rok-dam0029/Cdsy_preboarding/.git/ 안의 기존 깃 저장소를 다시 초기화했습니다

% git remote add origin https://github.com/RowanB606/Cdsy_preboarding.git
% git add .

% git status
현재 브랜치 main
브랜치가 'origin/main'에 맞게 업데이트된 상태입니다.

커밋할 변경 사항:
  (use "git restore --staged <file>..." to unstage)
	새 파일:       .DS_Store
	수정함:        week01/README.md
	새 파일:       week01/test.txt

% git commit -m "Commit #01 - New"
[main e96f5ba] Commit #01 - New
 Committer: 백록담 <rok-dam0029@c4r1s6.codyssey.kr>
이름과 전자메일 주소를 사용자 이름과 호스트 이름을 이용해서 자동으로
설정했습니다. 이 정보가 맞는지 확인하십시오. 이 메시지를 보지 않으려면 정보를
명시적으로 설정하십시오. 다음 명령어를 실행하고 편집기의 안내에 따라 설정
파일을 편집하십시오:

    git config --global --edit

이렇게 한 다음, 이 커밋에 사용한 신원 정보를 다음과 같이 해서 바꿀 수 있습니다:

    git commit --amend --reset-author

 3 files changed, 96 insertions(+), 1 deletion(-)
 create mode 100644 .DS_Store
 create mode 100644 week01/test.txt

% git status
현재 브랜치 main
브랜치가 'origin/main'보다 1개 커밋만큼 앞에 있습니다.
  (로컬에 있는 커밋을 제출하려면 "git push"를 사용하십시오)

커밋할 사항 없음, 작업 폴더 깨끗함

% git branch -M main
% git push -u origin main
오브젝트 나열하는 중: 9, 완료.
오브젝트 개수 세는 중: 100% (9/9), 완료.
Delta compression using up to 6 threads
오브젝트 압축하는 중: 100% (5/5), 완료.
오브젝트 쓰는 중: 100% (6/6), 1.73 KiB | 1.73 MiB/s, 완료.
Total 6 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/RowanB606/Cdsy_preboarding.git
   cd8f4c7..e96f5ba  main -> main
branch 'main' set up to track 'origin/main'.

% pwd
/Users/rok-dam0029/Cdsy_preboarding
% ls -la
# -l: long format 형식으로 표시
# -a: 숨김 파일까지 모두(all) 표시
total 16
drwxr-xr-x   5 rok-dam0029  rok-dam0029   160  8  4 02:31 .
drwxr-x---+ 21 rok-dam0029  rok-dam0029   672  8  4 02:35 ..
-rw-r--r--@  1 rok-dam0029  rok-dam0029  6148  8  4 02:25 .DS_Store
drwxr-xr-x  13 rok-dam0029  rok-dam0029   416  8  4 02:43 .git
drwxr-xr-x   4 rok-dam0029  rok-dam0029   128  8  4 02:26 week01
```

## 3. 권한 실습 및 증거 기록

### 3-1. 권한 변경 전
```text
% cd week01
% pwd
/Users/rok-dam0029/Cdsy_preboarding/week01
% mkdir Auth

% ls -la
total 24
drwxr-xr-x  5 rok-dam0029  rok-dam0029   160  8  4 03:27 .
drwxr-xr-x  5 rok-dam0029  rok-dam0029   160  8  4 02:31 ..
drwxr-xr-x  2 rok-dam0029  rok-dam0029    64  8  4 03:27 Auth
# 디렉토리Auth 소유자rwx 그룹r-x 기타사용자r-x 하드링크수2 소유자rok-dam0029 그룹rok-dam0029 64byte 8월 4일 03:27
-rw-r--r--  1 rok-dam0029  rok-dam0029  4663  8  4 02:45 README.md
-rw-r--r--  1 rok-dam0029  rok-dam0029    24  8  4 02:26 test.txt
# 파일test.txt 소유자rw- 그룹r-- 기타사용자r-- 하드링크수1 소유자rok-dam0029 그룹rok-dam0029 24byte 8월 4일 02:26
```

### 3-2. 권한 변경(1)
```text
% chmod 777 Auth
% chmod 000 test.txt
% ls -la
drwxr-xr-x  5 rok-dam0029  rok-dam0029   160  8  4 03:27 .
drwxr-xr-x  5 rok-dam0029  rok-dam0029   160  8  4 02:31 ..
drwxrwxrwx  2 rok-dam0029  rok-dam0029    64  8  4 03:27 Auth
# 디렉토리Auth 소유자rwx 그룹rwx 기타사용자rwx 로 변경
-rw-r--r--  1 rok-dam0029  rok-dam0029  4663  8  4 02:45 README.md
----------  1 rok-dam0029  rok-dam0029    24  8  4 02:26 test.txt
# 파일test.txt 소유자--- 그룹--- 기타사용자--- 로 변경
```

### 3-3. 권한 변경(2) - 원복
```text
% chmod go-w Auth
% chmod u+rw,go=r test.txt
% ls -la
total 24
drwxr-xr-x  5 rok-dam0029  rok-dam0029   160  8  4 03:27 .
drwxr-xr-x  5 rok-dam0029  rok-dam0029   160  8  4 02:31 ..
drwxr-xr-x  2 rok-dam0029  rok-dam0029    64  8  4 03:27 Auth
-rw-r--r--  1 rok-dam0029  rok-dam0029  4663  8  4 02:45 README.md
-rw-r--r--  1 rok-dam0029  rok-dam0029    24  8  4 02:26 test.txt

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ(r=읽기, w=쓰기, x=실행, -=권한없음)ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
|    7 : rwx    |    u : 소유자        |    + : 권한추가         |
|    6 : rw-    |    g : 그룹         |    - : 권한제거          |
|    5 : r-x    |    o : 기타사용자     |    = : 지정값으로 설정    |
|    4 : 4--    |    a : 모두(all)    |                       |
|    0 : ---    |                    |                       |
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
```

## 4. Docker 설치 및 기본 점검
### 4-1. Docker 버전 확인
```text
% docker --version
Docker version 29.4.0, build 9d7ad9f
```

### 4-2. Docker Daemon 동작 여부 확인
```text
# Docker Desktop 대신 OrbStack 실행

% docker info
Client:
 Version:    29.4.0
 Context:    orbstack
 Debug Mode: false
 Plugins:
  agent: Docker AI Agent Runner (Docker Inc.)
    Version:  v1.115.0
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-agent
  ai: Docker AI Agent - Ask Gordon (Docker Inc.)
    Version:  v1.27.0
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-ai
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.33.0
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v5.1.2
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-compose
  debug: Get a shell into any image or container (Docker Inc.)
    Version:  0.0.47
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-debug
  desktop: Docker Desktop commands (Docker Inc.)
    Version:  v0.4.3
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-desktop
  dhi: CLI for managing Docker Hardened Images (Docker Inc.)
    Version:  v0.0.7
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-dhi
  extension: Manages Docker extensions (Docker Inc.)
    Version:  v0.2.31
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-extension
  init: Creates Docker-related starter files for your project (Docker Inc.)
    Version:  v1.4.0
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-init
  mcp: Docker MCP Plugin (Docker Inc.)
    Version:  v0.43.3
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-mcp
  offload: Docker Offload (Docker Inc.)
    Version:  v0.6.9
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-offload
  pass: Docker Pass Secrets Manager Plugin (beta) (Docker Inc.)
    Version:  v0.2.0
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-pass
  sandbox: "docker sandbox" is deprecated, use Docker Sandboxes instead (Docker Inc.)
    Version:  v0.13.0
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-sandbox
  scout: Docker Scout (Docker Inc.)
    Version:  v1.23.1
    Path:     /Users/rok-dam0029/.docker/cli-plugins/docker-scout

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 29.4.0
 Storage Driver: overlayfs
  driver-type: io.containerd.snapshotter.v1
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 CDI spec directories:
  /etc/cdi
  /var/run/cdi
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 77c84241c7cbdd9b4eca2591793e3d4f4317c590
 runc version: c241c0bb5e60a8e8c1b2e53d4eca8d0068d8d57e
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.19.13-orbstack-gbd1dc07b8cf4
 Operating System: OrbStack
 OSType: linux
 Architecture: x86_64
 CPUs: 6
 Total Memory: 15.67GiB
 Name: orbstack
 ID: d2503a70-f1e4-40ce-a258-a19db07ed5a9
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  ::1/128
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine
 Default Address Pools:
   Base: 192.168.97.0/24, Size: 24
   Base: 192.168.107.0/24, Size: 24
   Base: 192.168.117.0/24, Size: 24
   Base: 192.168.147.0/24, Size: 24
   Base: 192.168.148.0/24, Size: 24
   Base: 192.168.155.0/24, Size: 24
   Base: 192.168.156.0/24, Size: 24
   Base: 192.168.158.0/24, Size: 24
   Base: 192.168.163.0/24, Size: 24
   Base: 192.168.164.0/24, Size: 24
   Base: 192.168.165.0/24, Size: 24
   Base: 192.168.166.0/24, Size: 24
   Base: 192.168.167.0/24, Size: 24
   Base: 192.168.171.0/24, Size: 24
   Base: 192.168.172.0/24, Size: 24
   Base: 192.168.181.0/24, Size: 24
   Base: 192.168.183.0/24, Size: 24
   Base: 192.168.186.0/24, Size: 24
   Base: 192.168.207.0/24, Size: 24
   Base: 192.168.214.0/24, Size: 24
   Base: 192.168.215.0/24, Size: 24
   Base: 192.168.216.0/24, Size: 24
   Base: 192.168.223.0/24, Size: 24
   Base: 192.168.227.0/24, Size: 24
   Base: 192.168.228.0/24, Size: 24
   Base: 192.168.229.0/24, Size: 24
   Base: 192.168.237.0/24, Size: 24
   Base: 192.168.239.0/24, Size: 24
   Base: 192.168.242.0/24, Size: 24
   Base: 192.168.247.0/24, Size: 24
   Base: fd07:b51a:cc66:d000::/56, Size: 64
 Firewall Backend: iptables

WARNING: DOCKER_INSECURE_NO_IPTABLES_RAW is set
```

## 5. Docker 기본 운영 명령 수행
### 5-1. 이미지





## 6. 컨테이너 실행 실습


## 7. 기존 Dockerfile 기반 커스텀 이미지 제작


## 8. 포트 매핑 및 접속 증거


## 9. Docker 볼륨 영속성 검증


## 10. Git 설정 및 GitHub 연동

