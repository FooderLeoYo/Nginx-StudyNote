# wordpress

## 目录

[安装](#jump1)

[](#jump)

[](#jump)

[](#jump)

[](#jump)

[](#jump)

---	

<span id="jump1"></span>

## 安装

1. 从官网下载最新压缩包

2. 将wordpress文件夹丢到：/usr/share/nginx/html

3. 检查lnmp环境是否全部搭建完整

4. /etc/nginx/conf.d/default.conf中的server的location的index，添加index.php

5. 浏览器输入：公网ip/wordpress，进入安装向导

6. 安装成功后，以后登录地址为：http://121.37.185.108/wordpress/wp-login.php

7. 如果更新插件时报“Failed to connect to FTP Server”，则编辑wp-config.php，在

```shell
/* That's all, stop editing! Happy publishing. */
```

的上一行添加：

```shell
define('FS_METHOD', "direct");
```