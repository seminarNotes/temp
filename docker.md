# Docker
최초 작성일 : 2024-01-15  
마지막 수정일 : 2024-01-15  
  
## 0. Overview
현재 docker는 너무 많은 개발자와 유저들이 사용하고 있는 tool이다. 훌륭한 양질의 내용과 콘텐츠로 docker에 대해 소개하고 있는 영상과 글 또한 많이 있지만, 한번쯤은 docker에 대한 내용을 정리해야만 비로소 내 것이 된다는 믿음에 이 글에서 docker에 대한 내용을 정리한다. 이 글에서는 docker에 대한 개념, 설치, 간단한 조작 방법에 대해서 공부한다. 

## Table of Contents
1. [Introduction to Docker](#1.-Introduction-to-Docker)
2. [Install Docker Engine on WLS2](#2.-Install-Docker-Engine-on-WLS2)
3. [Install Airflow in Docker](#3.-Install-Airflow-in-Docker) 

## 1. Introduction to Docker  
Docker는 컨테이너화 기술을 기반으로 하는 오픈 소스 플랫폼으로, 애플리케이션을 패키징하고 실행하는 데 활용된다.  Docker는 애플리케이션과 그 의존성을 격리된 환경인 "컨테이너"에 포장하여 이식성을 높이고, 환경 간에 쉽게 배포 및 실행할 수 있다는 장점이 존재한다.


## 2. Install Docker Engine on WLS2
wsl를 통해 home/user 디렉토리로 이동한 다음, 에러를 발생시키는 패키지를 먼저 삭제한다.
```console
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

설치 전, 설치된 패키지 목록을 최신 상태로 업데이트 한다.
```console
sudo apt-get update




# practice--docker
# Linux에서 docker 삭제 

기존 있는 도커의 오래된 버전을 삭제
``` bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```

리눅스 패키지 업데이트(최신화)
``` bash
sudo apt-get update
```
설치를 위한 세
``` bash
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
``` bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | 
```
``` bash
sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
``` bash
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  sudo apt-get update
```

docker를 설치
``` bash
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

docker가 실행되었는지 확인
```bash
docker version
```






# 컨테이너 이름 또는 ID 확인


# 컨테이너 실행
```bash
docker start <CONTAINER_ID>
```



# 컨테이너 종료
실행 중인 컨테이너를 종료하는 코드는 아래와 같다.
```bash
docker stop <CONTAINER_ID>
```


실행 중인 컨테이너를 종료 / 강제 종료할 때,
```bash
docker stop $(docker ps -q)

docker kill $(docker ps -q)
```

# 컨테이너 조회

```bash
docker container ls
```
현재 시스템에서 실행 중인 모든 Docoker 컨테이너 목록을 표시
```bash
docker container ls -a
```
중지된 컨테이너도 포함하여 모든 컨테이너를 표시

# 실행 중인 Docker 컨테이너에 접속하며, 컨테이너 내부 터미널에 연결
```bash
docker attach <CONTAINER_ID>
```

# 이미지를 사용하여 새로운 컨테이너를 실행
```bash
docker run <CONTAINER_ID>
```
docker 이미지를 사용해서 새로운 컨테이너를 실행하면서, 대화형 터미널로 컨테이너 내부에 연결
```bash
docker run -it <CONTAINER_ID>
```

# 컨테이너 삭제
```bash
docker rm <CONTAINER_ID>
```
컨테이너의 파일 시스템과 설정 정보가 모두 삭제
