# docker-oracle_orgin

oracle-xe-11g
Oracle Database 11g Express Edition，Oracle数据库的免费版本，支持标准版的大部分功能。

镜像来自 docker hub wnameless/oracle-xe-11g

原作者分别基于Ubuntu 16.04，Ubuntu14.04 制作了镜像，这个仓库的latest是16.04版本。

镜像的获取

直接获取原作者的镜像

# 获得latest
docker pull wnameless/oracle-xe-11g

# 获得16.04版本
docker pull wnameless/oracle-xe-11g:16.04

# 获得14.04版本
docker pull wnameless/oracle-xe-11g:14.04.4
如果忍受不了下载速度的话，推荐使用加速器，或者直接使用daocloud hub获取方式

从Daocloud hub获取

docker pull daocloud.io/ihypo/oracle-xe-11g:latest
使用

启动

因为除了一个db之外，此镜像还有ssh，因此需要开放两个端口。 需要开放22端口（可选）和1521端口：

docker run -d -p 49160:22 -p 49161:1521 daocloud.io/ihypo/oracle-xe-11g
如果需要外部访问的话还需要添加环境变量，ORACLE_ALLOW_REMOTE=true ，如下：

docker run -d -p 49160:22 -p 49161:1521 -e ORACLE_ALLOW_REMOTE=true daocloud.io/ihypo/oracle-xe-11g
连接

容器启动之后，db的默认配置如下：

hostname: localhost
port: 49161
sid: xe
username: system
password: oracle
SSH 登录

ssh root@localhost -p 49160
password: admin
其他

Password for SYS & SYSTEM

oracle
Support custom DB Initialization

# Dockerfile
FROM wnameless/oracle-xe-11g

ADD init.sql /docker-entrypoint-initdb.d/