# 00-basics

## 목표

WSL2 우분투에서 리눅스 기본 명령, 파일 권한, 패키지 설치를 익힌다.
아파치 웹 서버를 직접 설치하고 실행한다.
수동 설치 과정을 셸 스크립트 한 개로 재현한다.

## 구성도

작성 예정이다.
파일 이름은 `diagram-basics.png`로 한다.

## 수행 과정

참고 교재는 Do it 리눅스 입문이다.

| 파트 | 교재 범위 | 결과물 | 상태 |
|---|---|---|---|
| p1 기본 명령과 경로 | 02-4, 03장, 04-1, 04-2 | 실습 폴더 구조 | 완료 |
| p2 사용자와 권한 | 04-3, 04-4 | 권한을 바꾼 파일 | 완료 |
| p3 패키지와 프로세스 | 05-1의 apt, 05-3 | 설치한 패키지 목록 | 진행 중 |
| p4 문서 편집과 로그 | 06-1, 06-2, 06-3 | 편집한 설정 파일 | 대기 |
| p5 웹 서버 | 08-1, 08-2, 08-3의 아파치 부분 | 아파치 기본 페이지 | 대기 |
| p6 셸 스크립트 | 07-1, 07-2, 07-3 | `install-apache.sh` | 대기 |

### p1 기본 명령과 경로

실습 환경은 WSL2 우분투 24.04이다.
실습 폴더는 `~/practice`이다.

| 순서 | 명령 | 한 일 |
|---|---|---|
| 1 | `pwd`, `cd /`, `cd ~`, `cd ..` | 현재 위치를 확인하고 루트, 홈, 상위 폴더로 이동했다. |
| 2 | `ls -a`, `ls -l`, `ls -R` | 숨김 파일, 상세 정보, 하위 폴더 목록을 확인했다. |
| 3 | `mkdir -p web/html web/logs` | 중간 폴더까지 한 번에 만들었다. |
| 4 | `touch memo.txt` | 빈 파일을 만들었다. |
| 5 | `cp memo.txt web/html/index.html` | 파일을 다른 이름으로 복사했다. |
| 6 | `mv memo.txt web/logs/access.log` | 파일을 옮기면서 이름을 바꿨다. |
| 7 | `rm -i trash.txt` | 확인을 거쳐 파일을 지웠다. |
| 8 | `getconf LONG_BIT` | 운영체제가 64비트인 것을 확인했다. |
| 9 | `sudo apt install tree` | 검증에 쓸 tree를 설치했다. |

운영체제 확인 캡처는 `images/p1-os-version.png`이다.

최종 구조는 다음과 같다.

```
.
└── web
    ├── html
    │   └── index.html
    └── logs
        └── access.log

4 directories, 2 files
```

### p2 사용자와 권한

실습 파일은 `~/practice/perm-lab/note.txt`이다.
`ls -l` 출력은 권한, 하드 링크 수, 소유자, 그룹, 크기, 수정 시간, 이름 순서이다.

| 순서 | 명령 | 한 일 |
|---|---|---|
| 1 | `touch note.txt`, `ls -l note.txt` | 파일을 만들고 기본 권한 `-rw-r--r--`을 읽었다. |
| 2 | `chmod 754 note.txt` | 소유자 rwx, 그룹 r-x, 그 외 r--로 바꿨다. |
| 3 | `chmod 600 note.txt` | 소유자만 읽고 쓰게 바꿨다. |
| 4 | `chmod 644 note.txt` | 기본 권한으로 되돌렸다. |
| 5 | `whoami`, `id` | 현재 사용자와 uid, gid, 속한 그룹을 확인했다. |
| 6 | `sudo whoami`, `sudo id` | 관리자 권한으로 실행하면 root로 나오는 것을 확인했다. |
| 7 | `sudo chown root:root note.txt` | 소유자와 그룹을 root로 바꿨다. |
| 8 | `echo hello > note.txt` | 그 외 사용자 권한이 r--라서 `Permission denied`가 나왔다. |
| 9 | `sudo chown haeans:haeans note.txt`, `echo hello > note.txt`, `cat note.txt` | 소유자를 되돌리자 쓰기가 되고 hello가 출력됐다. |

소유자 변경 전후 확인 캡처는 `images/p2-permission.png`이다.

### p3 패키지와 프로세스

이 섹션은 W46-T4 범위인 apt 부분만 쓴다.
프로세스 부분은 작성 예정이다.

| 순서 | 명령 | 한 일 |
|---|---|---|
| 1 | `sudo apt update` | 패키지 목록을 새로 받았다. 125개가 업그레이드 가능하다고 나왔다. |
| 2 | `apt list --upgradable \| head -n 6` | 새 버전이 있는 패키지와 설치된 버전을 확인했다. |
| 3 | `cowsay hi` | 설치 전에 `Command 'cowsay' not found`가 나오는 기준 상태를 확인했다. |
| 4 | `sudo apt install cowsay` | cowsay를 설치했다. |
| 5 | `cowsay hi` | 말풍선과 소 그림이 출력되는 것을 확인했다. |
| 6 | `sudo apt remove cowsay`, `cowsay hi` | 삭제한 뒤 `Command 'cowsay' not found`가 다시 나오는 것을 확인했다. |

`update`는 새 버전 목록만 받고 `upgrade`는 설치된 프로그램을 실제로 바꾼다.
이번에는 시스템 전체가 바뀌는 `upgrade`를 실행하지 않았다.

### p4 문서 편집과 로그

작성 예정이다.

### p5 웹 서버

작성 예정이다.

### p6 셸 스크립트

작성 예정이다.

## 검증

| 파트 | 검증 방법 | 증빙 |
|---|---|---|
| p1 | `tree` 출력으로 폴더 구조를 확인한다. | `p1-tree.png` |
| p2 | `ls -l` 출력을 권한 변경 전후로 비교한다. | `p2-permission.png` |
| p3 | `ps`로 프로세스를 찾고 `kill`로 종료한 뒤 사라졌는지 확인한다. | `p3-process.png` |
| p4 | `tail`과 파이프로 원하는 줄만 출력한다. | `p4-pipe.png` |
| p5 | 브라우저로 아파치 기본 페이지에 접속한다. | `p5-apache.png` |
| p6 | 아파치를 지운 뒤 스크립트 한 번으로 다시 설치되는지 확인한다. | `p6-script.png` |

## 정리

파트를 마칠 때마다 무엇을, 왜, 어떻게 확인했는지 3문장과 배운 점을 쓴다.

### p1 정리

WSL2 우분투에서 위치 확인, 이동, 파일과 폴더의 생성, 복사, 이동, 삭제 명령을 익혔다.
이후 파트에서 설정 파일과 로그를 찾고 다루려면 경로를 다루는 감각이 먼저 필요하다.
`~/practice`에 웹 서버 모양의 폴더 구조를 만들고 `tree` 출력이 4 directories, 2 files인 것으로 확인했다.

배운 점은 다음과 같다.

- `mkdir`의 `-p`는 없는 중간 폴더를 함께 만든다.
- `mv`는 같은 명령으로 이동과 이름 변경을 한다.
- `rm`은 휴지통 없이 지우므로 `-i`로 확인하고 지운다.

### p2 정리

파일 권한과 소유자를 확인하고 바꾸는 명령을 익혔다.
웹 서버가 파일을 읽지 못하거나 SSH 키가 거부될 때 권한과 소유자부터 확인해야 하기 때문이다.
`chmod`로 754, 600, 644를 적용하고, `chown`으로 소유자를 root로 바꿨을 때 쓰기가 거부되고 되돌리면 쓰기가 되는 것을 `ls -l`, `echo`, `cat` 출력으로 확인했다.

배운 점은 다음과 같다.

- `ls -l` 권한은 소유자, 그룹, 그 외 사용자 순으로 세 글자씩 읽는다.
- 사용자는 소유자, 그룹, 그 외 중 해당하는 한 칸의 권한만 적용받는다.
- `chown`은 권한 숫자를 바꾸지 않고 소유자와 그룹만 바꾼다.

### 3단계 정리

디렉터리와 파일: `pwd`, `cd`, `ls`로 위치를 확인하고 `mkdir`, `touch`, `cp`, `mv`, `rm`으로 파일과 폴더를 만들고 옮기고 지웠다.
권한: `ls -l`의 권한을 소유자, 그룹, 그 외 사용자 순으로 읽고 `chmod`와 `chown`으로 바꿔 접근이 달라지는 것을 확인했다.
apt: `apt update`로 목록을 받고 `install`과 `remove`로 cowsay를 설치하고 지워 실행 여부로 확인했다.

### 문제 해결 기록

#### p1 캡처 파일 이름

- 증상: 캡처가 `00-basicsimagesp1-tree.png`로 저장됐다.
- 원인: 저장할 때 경로가 파일 이름에 붙어 들어갔다.
- 해결: `mv`로 이름을 `p1-tree.png`로 바꿨다.
- 배운 점: 증빙을 저장한 뒤 파일 이름을 바로 확인한다.

#### p1 git mv 오류

- 증상: `git mv` 실행 결과로 `fatal: bad source`가 나왔다.
- 원인: 이름 변경이 이미 끝난 뒤 같은 명령이 다시 실행된 것으로 보인다.
- 해결: `ls`와 `git status`로 새 이름의 파일이 있는 것을 확인했다.
- 배운 점: 오류가 나면 먼저 현재 상태를 확인한다.

#### p1 줄바꿈 차이

- 증상: WSL의 `git status`에 손대지 않은 파일 9개가 modified로 나왔다.
- 원인: 윈도우에서 만든 파일의 CRLF 줄 끝을 WSL git이 수정으로 봤다.
- 해결: `git config --global core.autocrlf input`을 설정했다.
- 배운 점: `git diff --ignore-cr-at-eol --stat`으로 줄 끝 차이만 있는지 확인할 수 있다.

#### p1 WSL git push 인증

- 증상: WSL에서 `git push`를 하자 `Password authentication is not supported` 오류가 났다.
- 원인: GitHub은 비밀번호 push를 받지 않고, WSL git에는 저장된 로그인 정보가 없었다.
- 해결: 윈도우의 `ucrt64/bin/git-credential-manager.exe`를 WSL git의 `credential.helper`로 지정했다.
- 배운 점: 설치 경로는 짐작하지 말고 `Get-ChildItem -Recurse -Filter`로 찾는다.
