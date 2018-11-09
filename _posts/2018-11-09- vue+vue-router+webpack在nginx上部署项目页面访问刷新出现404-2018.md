---
layout:     post
title:      "解决vue-router+webpack部署单页路由项目访问刷新出现404的bug"
subtitle:   "基于Ubuntu 18.04.1 LTS系统的远程连接以及文件上传下载"
date:       2018-11-09
author:     "Kwen"
header-img: "img/post-bg-2015.jpg"
tags:
    - vue
    - vue-router
    - webpack
---


#### 问题描述
vue-router + webpack 在nginx服务器上部署的单页路由项目页面访问刷新出现404

#### 解决方案
在nginx的conf文件的server下面添加或者修改如下配置
```
# m为该项目访问路径
location /m/ {
    try_files $uri $uri/ @router;
    index index.html;
}

# 此m与上面相同
location @router {
    rewrite ^.*$ /m/index.html last;
}
```