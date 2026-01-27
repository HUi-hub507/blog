---
title: Docker部署frp的指令
published: 2025-1-27
description: 一个教程，关于怎么使用Docker部署frp
image: ./image/深海色.png
tags: ["Docker", "学习"]
category: 学习
draft: false
---

## Docker部署frp

这是指令，一般来说都可以直接用

```
sudo docker run -d \
--restart=always \
--network=host \
--name "容器名字" \
-v /home/hui/frpc/"文件名字":/etc/frp/frpc.toml \
fatedier/frpc:v0.61.2 \
-c /etc/frp/frpc.toml
#示例
sudo docker run -d \
--restart=always \
--network=host \
--name frpc-poker \
-v /home/hui/frpc/frpc-poker.toml:/etc/frp/frpc.toml \
fatedier/frpc:v0.61.2 \
-c /etc/frp/frpc.toml
```

