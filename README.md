# docker_study
# 도커 명령어 사전
## 1.설치
### Linux 환경
<pre><code>
sudo apt-get update
sudo apt-get install docker.io
</code></pre>
### Window / OS X 환경
https://www.docker.com/

## 2.도커 이미지 관련 명령어
### docker images
<pre><code>
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
<pre><code>
docker inspect [옵션] <컨테이너 또는 이미지의 이름, ID>
ex) docker inspect centos
    docker inspect --format="{{ .Os }}" centos
    docker inspect --format="{{ .ContainerConfig.Image }}" centos
</code></pre>

### docker search
<pre><code>
docker search [옵션] <검색 키워드>
--automated=false (Automated Build만 표시)
--no-trunc=false (모든 결과 표시)
-s[--stars=0] (특정 개수 이상의 별 수)
</code></pre>
