# docker_study
***
# 도커 명령어 사전
## 1.설치
### Linux 환경
<pre><code>sudo apt-get update
sudo apt-get install docker.io
</code></pre>
### Window / OS X 환경 (그냥 GUI 환경에서 다운 받아 설치해요~)
https://www.docker.com/
## 2.도커 이미지 관련 명령어
### docker images (로컬저장소 이미지 목록 출력하기)
<pre><code>docker images [옵션] [repository명]
[옵션]
-a, --all=false (모든 이미지 표시)
--digests=false (digest 표시)
--no-trunc=false (모든 결과 표시)
-q, -quiet=false (docker 이미지 id만 표시)
[결과]
REPOSITORY(Docker 이미지명)
TAG(Docker 이미지 태그명)
IMAGE ID(Docker 이미지 ID)
CREATED(생성일)
VIRTUAL SIZE(사이즈)
</code></pre>
### docker inspect (이미지와 컨테이너 세부정보 출력)
<pre><code>docker inspect [옵션] <컨테이너 또는 이미지의 이름, ID>
ex) docker inspect centos
    docker inspect --format="{{ .Os }}" centos
    docker inspect --format="{{ .ContainerConfig.Image }}" centos
</code></pre>
### docker pull (원격저장소에서 이미지 다운로드)
<pre><code>docker pull [옵션] <이미지명:태그명>
ex) docker pull centos:7
    docker pull -a centos
    docker pull registry.hub.docker.com/centos:7
</code></pre>
### docker push (원격저장소에 이미지 올리기)
<pre><code>docker push [옵션] <이미지명:태그명>
구성 : <Dockerhub 사용자명/이미지명:태그명>
ex) docker push lhoris23/docker_study:1.0
</code></pre>
### docker search (원격저장소에서 이미지 검색하기)
<pre><code>docker search [옵션] <검색 키워드>
--automated=false (Automated Build만 표시)
--no-trunc=false (모든 결과 표시)
-s[--stars=0] (특정 개수 이상의 별 수)
</code></pre>
### docker rmi (로컬저장소의 이미지 삭제하기)
<pre><code>docker rmi [옵션] <이미지명>
[옵션]
-f, --force=false (이미지 강제 삭제)
--no-prune=false (태그가 없는 부모 이미지를 삭제하지 않음)
</code></pre>

## 3.도커 컨테이너 구동 명령어
### docker run (이미지 -> 컨테이너 생성 / 해당 이미지 없으면 다운로드까지 자동으로 해준다.)
<pre><code>docker run [옵션] <이미지명:태그명> [값]
[옵션]
-a, --attach=[STDIN | STDOUT | STDERR] (표준 입력(STDIN), 표준 출력(STDOUT), 표준 에러 출력(STDERR)을 연결)
--cidfile="파일명" (컨테이너 ID를 파일로 출력)
-d, --detach=false (컨테이너를 백그라운드에서 실행)
-i, --interactive=false (컨테이너 표준 입력 열기)
-t, --tty=false (tty(단말 디바이스)를 사용)
--name (컨테이너명)
-p [호스트포트번호:컨테이너포트번호] (호스트와 컨테이너의 포트를 매핑)
-h, --hostname=="호스트명" (컨테이너의 호스트명 설정)
-w, --workdir=[경로] (컨테이너의 작업 
-h, --hostname=="호스트명" (컨테이너의 호스트명 설정)디렉토리를 설정
[리소스 옵션]
-c, --cpu-shares=0 (CPU 리소스 분해)
-m, --memory=[메모리 사용량] (메모리 사용량 제한(단위는 b, k, m, g 등))
-v, --volume=[호스트 디렉토리:컨테이너 디렉토리] (호스트와 컨테이너의 디렉토리 공유)

ex) docker run -it --name "test1" centos /bin/bash
</code></pre>
### docker start (컨테이너 구동)
<pre><code>docker start [옵션] <컨테이너명 또는 ID>
[옵션]
-a, --attach=false (표준 출력, 표준 에러를 연결)
-i, --interactive=false (컨테이너 표준 입력을 연결)
</code></pre>
### docker stop (컨테이너 가동 중지)
<pre><code>docker stop [옵션] <컨테이너명 또는 ID>
[옵션]
-t, --time=10 (컨테이너 중지 시간을 지정. 기본값은 10초)
</code></pre>
### docker restart
<pre><code>docker restart [옵션] <컨테이너명 또는 ID>
[옵션]
-t, --time=10 (컨테이너 재시작 시간을 지정. 기본값은 10초)
</code></pre>
### docker pause / docker unpause (컨테이너 일시정지 / 해제)
<pre><code>docker pause/unpause <컨테이너명 또는 ID></code></pre>
### docker rm (컨테이너 삭제)
<pre><code>docker rm [옵션] <컨테이너명 또는 ID>
[옵션]
-f, --force=false (구동 중인 컨테이너를 강제 삭제)
-v, --volumes=false (할당된 볼륨을 삭제)
ex) 모든 컨테이너 삭제
    docker rm -f 'docker ps -a -q'
</code></pre>
### docker stats (컨테이너 상태 확인)
<pre><code>docker stats <컨테이너명 또는 ID>
상태 확인 후, 커맨드 종료 Ctrl + C
</code></pre>
### docker ps (컨테이너 목록 출력)
<pre><code>docker ps [옵션]
[옵션]
-a, --all=false (구동, 중지 상태의 모든 컨테이너를 표시
--before="" (입력한 컨테이너명 또는 ID보다 이전에 구동된 컨테이너를 표시)
-f, --filter '[key]=[value]' (목록에 표시할 컨테이너를 필터링)
--format '[key]=[value]' (목록에 표시할 포맷을 설정)
-l, --latest=false (마지막에 구동된 컨테이너를 표시)
--no-trunc=false (생략된 정보 없이 모두 표시)
-q, --quiet=false (컨테이너 ID만 표시)
-s, --size=false (파일 사이즈를 표시)
--since="" (입력한 컨테이너명 또는 ID보다 이후에 구동된 컨테이너를 표시)
</code></pre>

## 4.도커 컨테이너 활용법
### docker attach (컨테이너 접속하기 / bash 진입한다)
<pre><code>$ docker attach test
// 구동중인 컨테이너에 접속할 땐 docker attach 커맨드를 사용
[root@36c5325ceb2d /]#
// bash 상태에서 컨테이너 종료하지 않고 bash 상태를 빠져나올때는 위 상태에서 Ctrl + P, Ctrl + Q 입력
</code></pre>
### docker exec (컨테이너 bash 진입 없이 내부 어플리케이션 실행 명령)
<pre><code>$ docker exec [옵션] <컨테이너명 또는 ID> <커맨드> [값]
[옵션]
-d, --detach=false (커맨드를 백그라운드에서 실행)
-i, --interactive=false (컨테이너 표준 입력 열기)
-t, --tty=false (tty(단말디바이스) 사용)
ex) docker exec -it oracle11g sqlplus
</code></pre>
### docker top (실행 프로세스 확인)
<pre><code>구동 중인 컨테이너에서 실행 중인 프로세스를 확인
ex) docker top oracle11g
</code></pre>
### docker port (포트 확인)
<pre><code>구동 중인 컨테이너에서 실행 중인 프로세스의 전송 포트를 확인
ex) docker port oracle11g
</code></pre>
### docker rename (컨테이너명 변경)
<pre><code>컨테이너명을 변경
ex) docker rename oracle11g ora11g
</code></pre>
### docker cp (컨테이너 내부 파일 복사)
<pre><code>컨테이너 내의 파일 호스트로 복사 <-> 호스트파일 컨테이너로 복사
docker cp <컨테이너명 또는 ID:컨테이너 내 파일경로> <호스트 디렉토리 경로>
docker cp  <호스트파일> <컨테이너명 또는 ID:컨테이너 내 파일경로>
</code></pre>

## 5.도커 컨테이너 이미지 생성
### docker commit (컨테이너 -> 이미지 생성)
<pre><code>docker commit [옵션] <컨테이너명 또는 ID> [이미지명:태그명]
[옵션]
-a, --author="~" (생성자 (예: LHORIS (lhoris@naver.com) ) )
-m, --message="~" (메시지)
-p, --pause=true (컨테이너를 일시 중지한 후 commit)
</code></pre>

## 6.Dockerfile
### Dockerfile 형식
<pre><code>명령어
FROM (베이스 이미지 지정) ADD (파일 및 디렉토리 추가)
MAINTAINER (Dockerfile 생성자) COPY (파일 복사)
RUN (커맨드 실행) VOLUME (볼륨 마운트)
CMD (데몬 실행) ENTRYPOINT (데몬 실행)
LABEL (라벨 설정) USER (사용자 설정)
EXPOSE (포트 export) WORKDIR (작업 디렉토리 지정)
ENV (환경변수 설정) ONBUILD (build 완료 후 실행될 명령어)

FROM [이미지명]
FROM [이미지명:태그명]
FROM [이미지명@Digest]

MAINTAINER [Dockerfile 작성자]
</code></pre>



## 7.기타
### Container 상태 configration 변경
<pre><code>[도커엔진On / 컨테이너Stop 상태]
아래 파일 내부 설정 변경
[리눅스 경로]
/var/lib/docker/containers/[hash_of_the_container]/hostconfig.json && config.v2.json
[맥OS 경로]
아래 명령어 입력 후
screen ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/tty
/var/lib/docker/containers/[hash_of_the_container]/hostconfig.json && config.v2.json
[config 설정 후 저장]
[도커엔진 Restart]
</code></pre>
