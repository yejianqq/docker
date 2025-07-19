## docker下载安装

linux：
https://get.docker.com/
curl -fsSL https://get.docker.com -o install-docker.sh
sudo sh install-docker.sh

windows：
wsl --set-deafault-version 2
wsl --update --web-download
重启
https://www.docker.com/  --》Download docker desktop --》AMD64

macos：
https://www.docker.com/  --》Download docker desktop --> MAC系统


## docker 命令：

docker pull docker.io/library/nginx:latest
docker.io 仓库的地址，官方的仓库（docker.io）可以省略
library 命名空间（作者名），library为官方的命名空间可以省略不写  
latest 标签 (版本号)
简化后 ：
docker pull nginx  = docker pull docker.io/library/nginx:latest

docker仓库地址：
https://hub.docker.com   官方仓库地址
https://docker.fxxk.dedyn.io  国内地址
https://github.com/tech-shrimp/docker_installer  安装参考git地址
sudo vi /etc/docker/daemon.json 修改配置文件
sudo service docker restart 重启docker服务

docker run -d -p 80:80 -v /website/html:/usr/share/nginx/html  nginx
-d 运行容器并进入后台
80 映射到容器的80端口
-v /website/html:/usr/share/nginx/html （绑定挂载）  映射宿主机的/website/html目录到容器的/usr/share/nginx/html目录  注意：映射目录必须存在，否则会报错；宿主机目录会覆盖容器目录下的文件

docker images  (查看本机的镜像)
docker ps(process status) 查看正在运行的容器
docker ps -a (查看所有容器)
docker stop 容器id  停止容器的服务
docker rm + 容器id 删除容器
docker rm + 容器id 强制删除容器，可以不用停止容器服务
docker rmi  镜像id  （删除镜像）

命名卷挂载
docker volume create nginx_html
docker run -d -p 80:80 -v nginx_html:/usr/share/nginx/html nginx
查看挂载卷的位置
docker volume inspect nginx_html
相比于绑定挂载，第一次使用的时候，容器会自动创建一个目录，并把镜像中的文件复制到该目录下

查看命名卷：
docker volume list
删除命名卷：
docker volume rm nginx_html
删除所有没有容器在使用的命名卷：
docker volume prune - a

docker run 其他参数：
设置账号名和密码 例如 启动mongo：
docker run -d -p 27017:27017 --name mongo -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=<PASSWORD> mongo
-p 映射宿主机的端口到容器的端口
--name 容器名
-e 设置环境变量 例如：-e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=<PASSWORD>  注意：环境变量的配置可以去官网的仓库中查看对应的配置，如果是开源项目的话可以去对应的git仓库查看相关的配置


docker file:


docker网络：


docker compose:


