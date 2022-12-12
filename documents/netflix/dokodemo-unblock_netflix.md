# 任意门解锁 netfix

> [参考文章](https://gist.github.com/phlinhng/c11c1268748874982fa6596fb0a4992a)

# 1.概述

目前解锁 Netflix 有三种方式，这里我们介绍的是下面的第二种

- 1.购买 dns 解锁服务
- 2.在主力机的基础中再购买 Netflix 解锁的机器
- 3.购买的 vps 自带解锁服务

# 2.准备工作

- 1.购买可以解锁 Netflix 的机器
- 2.使用本脚本搭建完毕两台机器，安装 Netflix 解锁机时不区分协议，随便安装一个协议即可

# 3.解锁步骤

- 1.需要分别设置两台 vps 的入站和出战，即**需要解锁的 vps**设置**出站**，**已经解锁的 vps**设置**入站**
- 2.举例

下面有 vpsA、vpsB 两台 vps。 vpsA 为 BWH GIA，不解锁 Netflix，vpsB 为解锁 Netflix 的 vps。

这个时候我们需要两步操作

- 1.登录**vpsA**，使用脚本中的 **流媒体工具箱->任意门落地机解锁 Netflix->设置出站**，ip 为上面的**已经解锁 Netflix 的 vpsB 的 ip**
- 2.登录**解锁的 Netflix 的 vps**，使用脚本中的**流媒体工具箱->任意门落地机解锁 Netflix->设置入站**，ip 为上面的**vpsA 的 ip**

# 4.如解锁机器仅支持 IPv6 怎么办？

- 1.vpsA 需要支持 IPv6
- 2.vpsA 解锁时需输入域名，域名需设置 IPv6，这个域名可以是搭建 IPv6 机器的域名
- 3.vpsA 按照【3.解锁步骤】搭建出站，出站写上面解析的域名，vpsB 搭建入站时 ip 写 vpsA 的 IPv6 ip
- 4.修改 vpsA 【10_ipv4_outbounds.json】文件中 tag 为 streamingMedia-443、streamingMedia-80 下的 domainStrategy 为【UseIPv6】
  <img src="https://raw.githubusercontent.com/anonymous-github-repositories/v2ray-agent/master/fodder/netflix_vpsA_10_ipv4_outbounds.png" width=700>

- 5.修改 vpsB【09_routing.json】有 source 的那一组的 outboundTag 为【IPv6-out】
  <img src="https://raw.githubusercontent.com/anonymous-github-repositories/v2ray-agent/master/fodder/netflix_vpsB_09_routing.png" width=700>

- 6.重启 vpsA、vpsB 中的核心

# 5.卸载

- 卸载不区分入站、出站，卸载即可。
