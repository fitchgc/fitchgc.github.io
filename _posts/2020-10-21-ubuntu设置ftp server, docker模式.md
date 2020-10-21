---
layout: post
title:  "ubuntu设置ftp server, docker模式"
date: 2020-10-21 14:39
categories: other
tags: dev ubuntu docker
---

创建启动脚本

```shell
docker run -d -v /root/code/ftp:/home/vsftpd -p 20:20 -p 21:21 -p 21100-21110:21100-21110 -e PASV_MIN_PORT=21100 -e PASV_MAX_PORT=21110 -e FTP_USER=upload -e FTP_PASS=7654321Hy -e PASV_ADDRESS=0.0.0.0 --restart=always --net mnet --ip=188.88.0.9 --name vsftpd fauria/vsftpd

# 挂载宿主机的/root/code/ftp目录至容器的/home/vsftpd
-v /root/code/ftp:/home/vsftpd
# 暴露容器的相关端口给宿主机
-p 20:20 -p 21:21 -p 21100-21110:21100-21110
# 设置passive mode的port range
-e PASV_MIN_PORT=21100 -e PASV_MAX_PORT=21110
# 设置ftp的用户名, 密码
-e FTP_USER=upload -e FTP_PASS=7654321Hy
# 设置绑定的ip
-e PASV_ADDRESS=0.0.0.0 
# 加入到自定义网络
--net mnet --ip=188.88.0.9
```

添加新的ftp帐号
```shell
docker exec -i -t vsftpd bash
mkdir /home/vsftpd/myuser
echo -e "myuser\nmypass" >> /etc/vsftpd/virtual_users.txt
/usr/bin/db_load -T -t hash -f /etc/vsftpd/virtual_users.txt /etc/vsftpd/virtual_users.db
exit
docker restart vsftpd
```