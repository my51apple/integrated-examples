介绍：

此配置包括 v2ray 与 trojan（trojan-go）集成。v2ray 包括如下应用：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

4、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）


注意：

1、利用 vless tcp 强大的回落/分流特性，实现了 vless tcp 与任意 ws 类应用完美共存，且vless tcp 以 http/1.1 或 http/2 自适应代理科学上网。

2、nginx 同时为 v2ray 与 trojan 提供 web 回落服务。

3、因 trojan（trojan-go）不支持 PROXY protocol，故统一不启用此项应用。

4、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c serve r共用一个端口或一个进程，故回落端口或进程必须分开。

5、nginx 不支持 h2c proxy，故无法搭建 vless\vmess+h2 反代应用。

6、nginx 预编译程序包不带支持SNI分流协议的模块。如要使用此项协议应用，需加 stream_ssl_preread_module 模块构建自定义模板，再进行源代码编译和安装。

7、配置1：v2ray 与 trojan 各自公开一个监听端口，各自分别提供科学上网服务。配置2：v2ray 通过配置相关参数为 v2ray、trojan(trojan-go) 进行 SNI 分流（四层转发），除 v2ray kcp 外，实现共用443端口。配置3：nginx 为 v2ray、trojan(trojan-go) 进行 SNI 分流（四层转发），除 v2ray kcp 外，实现共用443端口。
