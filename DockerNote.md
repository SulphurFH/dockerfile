# Docker

自己学习Docker记录的一些常用命令，平时查阅用

## Docker编译

```
docker build -t fanghao/centos:7.1 .    # .表示使用当前路径下的Dockerfie文件
```

## Docker镜像查看

```
docker images
```


## Docker启动镜像构建容器

```
docker run -it  #以交互式进入容器
docker run -d   #后台运行启动容器,返回一个container的id
docker run -d -p 2222:22 --name base fanghao/centos:7.1    #p与P的区别是一个指定宿主机端口映射，另一个随机分配宿主机端口映射，--name指定container的名字，后面跟要使用的容器名
docker run -d -p 80:80 --name wordpress -e WORDPRESS_DB_HOST=192.168.1.102 -e WORDPRESS_DB_USER=admin -e WORDPRESS_DB_PASSWORD=cspere2015 csphere/wordpress:4.2         # -e指定环境变量
docker run -it --rm csphere/cmd:0.1     #创建一个容器，当他退出时就把他删除掉
```

## Docker容器查看

```
docker ps -a    #查看本地所有状态的容器
docker ps       #查看本地正在运行的容器
```

## Docker镜像删除

```
docker rmi      #
```

## Docker容器删除

```
docker rm -f 'name'     # -f 为强制删除正在运行的容器
docker rm 
```

## Docker进入container

```
docker exec -it 'name' /bin/bash #以交互模式bash进入‘name’容器
```

## Docker停止容器

```
docker stop 'name'
```

## Docker VOLUME

```
docker run -d -p 3306:3306 -v /var/lib/docker/vfs/dir/mydata:/var/lib/mysql csphere/mysql:5.5 
# VOLUME参数:之前的表示宿主机路径，之后表示容器内路径当container删除之后，VOLUME的数据会在还会一直保存在宿主机，重新创建一个container，指定之前的-v，可以恢复数据
```

## Docker compose

```
sudo docker-compose -f etc/docker-compose-supervisor.yml down && sudo docker-compose -f etc/docker-compose-supervisor.yml up -d   # 使用docker-compose重启容器
```

## 常用docker容器命令

```
# Adminer
sudo docker pull adminer
sudo docker run -d --link mysql5.7:db --net mysql_net -p 9000:8080 --restart=always adminer

# thrift 生成相应代码文件并删除容器，把编译好的thirft当做命令使用
sudo docker run -v "/home/fanghao/docker/data/thrift:/data" thrift thrift -o /data --gen py /data/book.thrift && sudo docker rm -f `sudo docker ps -n=1 | awk 'NR > 1 {print $1}'`
```