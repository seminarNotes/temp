# Docker
최초 작성일 : 2024-01-15  
마지막 수정일 : 2024-01-15  
  
## 0. Overview
현재 docker는 너무 많은 개발자와 유저들이 사용하고 있는 tool이다. 훌륭한 양질의 내용과 콘텐츠로 docker에 대해 소개하고 있는 영상과 글 또한 많이 있지만, 한번쯤은 docker에 대한 내용을 정리해야만 비로소 내 것이 된다는 믿음에 이 글에서 docker에 대한 내용을 정리한다. 이 글에서는 docker에 대한 개념, 설치, 간단한 조작 방법에 대해서 공부한다. 

## Table of Contents
1. [Introduction to Docker](#1.-Introduction-to-Docker)
2. [Install Docker Engine on WLS2](#2.-Install-Docker-Engine-on-WLS2)
3. [Basic Docker Commands](#3.-Basic-Docker-Commands) 

## 1. Introduction to Docker  
Docker는 컨테이너화 기술을 기반으로 하는 오픈 소스 플랫폼으로, 애플리케이션을 패키징하고 실행하는 데 활용된다.  Docker는 애플리케이션과 그 의존성을 격리된 환경인 "컨테이너"에 포장하여 이식성을 높이고, 환경 간에 쉽게 배포 및 실행할 수 있다는 장점이 존재한다.


## 2. Basic Docker Commands  
### 2-1. Commands for images
Docker는 이미지(image)를 통해 애플리케이션 및 환경을 패키징하고, 이 이미지를 Docker Hub와 같은 Docker 레지스트리에서 다른 사람들과 공유하며, 로컬 머신으로 이미지를 가져와서 컨테이너(container)로 실행하는 구조이다. 따라서, 맨 처음 image에 대한 기본적인 command에 대해서 알아보자.

#### 2-1-1. Docker Registry에서 이미지 조회  
검색어(SEARCH_KEYWORD)를 사용하여 이미지를 찾고 해당 이미지의 이름, 설명 등을 확인할 수 있다. 예를 들어, mysql에 대한 이미지를 조회하면 다음과 같은 출력을 확인 할 수 있다.
``` bash
# docker search <SEARCH_KEYWORD>
docker search mysql
```
```
NAME                            DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql                           MySQL is a widely used, open-source relation…   14767     [OK]
mariadb                         MariaDB Server is a high performing open sou…   5633      [OK]
percona                         Percona Server is a fork of the MySQL relati…   624       [OK]
phpmyadmin                      phpMyAdmin - A web interface for MySQL and M…   928       [OK]
bitnami/mysql                   Bitnami MySQL Docker Image                      106                  [OK]
bitnami/mysqld-exporter                                                         6
cimg/mysql                                                                      2
ubuntu/mysql                    MySQL open source fast, stable, multi-thread…   56
rapidfort/mysql                 RapidFort optimized, hardened image for MySQL   25
rapidfort/mysql8-ib             RapidFort optimized, hardened image for MySQ…   9
google/mysql                    MySQL server for Google Compute Engine          25                   [OK]
rapidfort/mysql-official        RapidFort optimized, hardened image for MySQ…   9
elestio/mysql                   Mysql, verified and packaged by Elestio         0
hashicorp/mysql-portworx-demo                                                   0
bitnamicharts/mysql                                                             0
newrelic/mysql-plugin           New Relic Plugin for monitoring MySQL databa…   1                    [OK]
databack/mysql-backup           Back up mysql databases to... anywhere!         105
linuxserver/mysql               A Mysql container, brought to you by LinuxSe…   41
mirantis/mysql                                                                  0
linuxserver/mysql-workbench                                                     54
vitess/mysqlctld                vitess/mysqlctld                                1                    [OK]
eclipse/mysql                   Mysql 5.7, curl, rsync                          1                    [OK]
drupalci/mysql-5.5              https://www.drupal.org/project/drupalci         3                    [OK]
drupalci/mysql-5.7              https://www.drupal.org/project/drupalci         0
datajoint/mysql                 MySQL image pre-configured to work smoothly …   2                    [OK]
```

#### 2-1-2. 이미지 다운로드
Docker 이미지를 Docker 레지스트리에서 로컬 머신으로 다운로드한다. 이미지 이름과 선택적으로 태그를 지정하여 원하는 이미지를 가져올 수 있지만, tag를 생략할 경우, 가장 최신 버전의 image를 가지고 온다.
``` bash
# docker pull <SEARCH_KEYWORD>
docker pull mysql
```
```
Using default tag: latest
latest: Pulling from library/mysql
bce031bc522d: Pull complete
cf7e9f463619: Pull complete
105f403783c7: Pull complete
878e53a613d8: Pull complete
2a362044e79f: Pull complete
6e4df4f73cfe: Pull complete
69263d634755: Pull complete
fe5e85549202: Pull complete
5c02229ce6f1: Extracting [============================>                      ]  35.09MB/62.09MB
7320aa32bf42: Download complete
```

#### 2-1-3. 로컬 머에서 이미지 조회  
로컬 머신에 저장된 모든 Docker 이미지를 나열한다. 이미지 이름, 태그, 이미지 ID 및 크기 정보가 표시된다.
``` bash
docker images
```









wsl를 통해 home/user 디렉토리로 이동한 다음, 에러를 발생시키는 패키지를 먼저 삭제한다.
```console
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

설치 전, 설치된 패키지 목록을 최신 상태로 업데이트 한다.
```console
sudo apt-get update
```
이 후, 필요한 패키지를 차례대로 설치한다.
```console
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
아래는 파일에 대한 권한을 변경하는 명령어로, 유저에게 docker.gpg 파일에 대한 읽기 권한을 부여한다.
```console
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
마지막으로, 저장소를 통해 Docker를 설치하고, 업데이트 할 수 있도록, Docker의 공식 APT 패키지 저장소를 시스템에 추가한다.
```console
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
필요한 패키지를 모두 성공적으로 설치하였으면, 최신 상태로 업데이트 한다.
```console
sudo apt-get update
```
아래는 Docker와 관련된 패키지를 설치하는 것으로, docker-ce(Docker Community Edition), docker-ce-cil(Docker Command Line Interface), containerd.io(컨테이너 실행과 관리를 담당하는 런타임), docker-buildx-plugin, docker-compose-plugin(플러그인)을 차례대로 설치한다.
```console
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Docker 프로그램을 실행하는 것으로 다음 명령어를 입력한다.
```console
sudo service docker start
```
마지막으로, "sudo docker run hello-world"를 입력하여 에러가 발생하지 않으면서, 정상적으로 설치되었음을 확인할 수 있다.
```console
sudo docker run hello-world
```

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
