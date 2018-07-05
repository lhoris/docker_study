# docker_study
# 도커 명령어 사전
## 1.설치
### Linux 환경
<pre><code>sudo apt-get update
sudo apt-get install docker.io
</code></pre>
### Window / OS X 환경
https://www.docker.com/
## 2.도커 이미지 관련 명령어
### docker images
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
### docker inspect
<pre><code>docker inspect [옵션] <컨테이너 또는 이미지의 이름, ID>
ex) docker inspect centos
    docker inspect --format="{{ .Os }}" centos
    docker inspect --format="{{ .ContainerConfig.Image }}" centos
</code></pre>
### docker pull
<pre><code>docker pull [옵션] <이미지명:태그명>
ex) docker pull centos:7
    docker pull -a centos
    docker pull registry.hub.docker.com/centos:7
</code></pre>
### docker push
<pre><code>docker push [옵션] <이미지명:태그명>
구성 : <Dockerhub 사용자명/이미지명:태그명>
ex) docker push lhoris23/docker_study:1.0
</code></pre>
### docker search
<pre><code>docker search [옵션] <검색 키워드>
--automated=false (Automated Build만 표시)
--no-trunc=false (모든 결과 표시)
-s[--stars=0] (특정 개수 이상의 별 수)
</code></pre>
### docker rmi
<pre><code>docker rmi [옵션] <이미지명>
[옵션]
-f, --force=false (이미지 강제 삭제)
--no-prune=false (태그가 없는 부모 이미지를 삭제하지 않음)
</code></pre>

## 3.도커 컨테이너 구동 명령어
### docker run
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
### docker start
<pre><code>docker start [옵션] <컨테이너명 또는 ID>
[옵션]
-a, --attach=false (표준 출력, 표준 에러를 연결)
-i, --interactive=false (컨테이너 표준 입력을 연결)
</code></pre>
### docker stop
<pre><code>docker stop [옵션] <컨테이너명 또는 ID>
[옵션]
-t, --time=10 (컨테이너 중지 시간을 지정. 기본값은 10초)
</code></pre>
### docker restart
<pre><code>docker restart [옵션] <컨테이너명 또는 ID>
[옵션]
-t, --time=10 (컨테이너 재시작 시간을 지정. 기본값은 10초)
</code></pre>
### docker pause / docker unpause
<pre><code>docker pause/unpause <컨테이너명 또는 ID></code></pre>
### docker rm
<pre><code>docker rm [옵션] <컨테이너명 또는 ID>
[옵션]
-f, --force=false (구동 중인 컨테이너를 강제 삭제)
-v, --volumes=false (할당된 볼륨을 삭제)
ex) 모든 컨테이너 삭제
    docker rm -f 'docker ps -a -q'
</code></pre>
### docker stats
<pre><code>docker stats <컨테이너명 또는 ID>
상태 확인 후, 커맨드 종료 Ctrl + C
</code></pre>
### docker ps
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

## 4.도커 컨테이너 중급 활용
### docker attach
<pre><code>$ docker attach test
// 구동중인 컨테이너에 접속할 땐 docker attach 커맨드를 사용
[root@36c5325ceb2d /]#
// bash 상태에서 컨테이너 종료하지 않고 bash 상태를 빠져나올때는 위 상태에서 Ctrl + P, Ctrl + Q 입력
</code></pre>
### docker exec
<pre><code>$ docker exec [옵션] <컨테이너명 또는 ID> <커맨드> [값]
[옵션]
-d, --detach=false (커맨드를 백그라운드에서 실행)
-i, --interactive=false (컨테이너 표준 입력 열기)
-t, --tty=false (tty(단말디바이스) 사용)
ex) docker exec -it oracle11g sqlplus
</code></pre>
### docker top
<pre><code>구동 중인 컨테이너에서 실행 중인 프로세스를 확인
ex) docker top oracle11g
</code></pre>
### docker port
<pre><code>구동 중인 컨테이너에서 실행 중인 프로세스의 전송 포트를 확인
ex) docker port oracle11g
</code></pre>
### docker rename
<pre><code>컨테이너명을 변경
ex) docker rename oracle11g ora11g
</code></pre>
### docker cp
<pre><code>컨테이너 내의 파일 호스트로 복사 <-> 호스트파일 컨테이너로 복사
docker cp <컨테이너명 또는 ID:컨테이너 내 파일경로> <호스트 디렉토리 경로>
docker cp  <호스트파일> <컨테이너명 또는 ID:컨테이너 내 파일경로>
</code></pre>
