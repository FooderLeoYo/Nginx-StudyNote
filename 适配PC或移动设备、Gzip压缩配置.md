# 适配PC或移动设备、Gzip压缩配置

## 目录

[适配概念](#jump1)

[利用$http_user_agent实现适配](#jump2)

[Gzip压缩配置](#jump3)

[](#jump)

[](#jump)

[](#jump)

---	

<span id="jump1"></span>

## 适配概念

现在很多网站都是有了PC端和H5站点的

因为这样就可以根据客户设备的不同，显示出体验更好的，不同的页面了

虽然可以通过自适应实现，但是无论是复杂性和易用性上面还是不如分开编写的好

---

<span id="jump2"></span>

## 利用$http_user_agent实现适配

Nginx通过内置变量$http_user_agent，可以获取到请求客户端的userAgent

就可以用户目前处于移动端还是PC端，进而展示不同的页面给用户

操作步骤如下：

1. 在/usr/share/nginx/目录下新建两个文件夹，分别为：pc和mobile

2. 在pc和miblic目录下，新建两个index.html文件，问价内容如下：

```shell
<h1>I am pc!</h1>
```

```shell
<h1>I am mobile!</h1>
```

3. 进入etc/nginx/conf.d目录下，修改8001.conf文件:

```shell
server{
     listen 80;
     server_name nginx2.jspang.com;
     location / {
      root /usr/share/nginx/pc;
      if ($http_user_agent ~* '(Android|webOS|iPhone|iPod|BlackBerry)') {
         root /usr/share/nginx/mobile;
      }
      index index.html;
     }
}
```

---

<span id="jump3"></span>

## Gzip压缩配置

### gzip的配置项

```
gzip : 该指令用于开启或 关闭gzip模块。
gzip_buffers : 设置系统获取几个单位的缓存用于存储gzip的压缩结果数据流。
gzip_comp_level : gzip压缩比，压缩级别是1-9，1的压缩级别最低，9的压缩级别最高。压缩级别越高压缩率越大，压缩时间越长。
gzip_disable : 可以通过该指令对一些特定的User-Agent不使用压缩功能。
gzip_min_length:设置允许压缩的页面最小字节数，页面字节数从相应消息头的Content-length中进行获取。
gzip_http_version：识别HTTP协议版本，其值可以是1.1.或1.0.
gzip_proxied : 用于设置启用或禁用从代理服务器上收到相应内容gzip压缩。
gzip_vary : 用于在响应消息头中添加Vary：Accept-Encoding,使代理服务器根据请求头中的Accept-Encoding识别是否启用gzip压缩。
```

### gzip最简单的配置

1. 进入etc/nginx/nginx.conf

2. 修改http部分

```shell
http {
   .....
    gzip on;
    gzip_types text/plain application/javascript text/css;
   .....
}
```

gzip on是启用gizp模块

下面的一行是用于在客户端访问网页时，对文本、JavaScript 和CSS文件进行压缩输出

3. 重启nginx

4. 搜索“gzip 检测”，输入网址，可以查看是否成功启用gzip压缩