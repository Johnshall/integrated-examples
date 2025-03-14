介绍：

利用 caddy 支持 WebSocket（WS）、H2C、gRPC 代理及 naiveproxy 代理，实现除 Xray 或 v2ray 的 KCP 应用外，WebSocket（WS）、H2C、gRPC 类反向代理应用及 naiveproxy 正向代理应用共用443端口。包括应用如下：

1、B=vless+ws+tls（TLS由caddy提供及处理，不需配置。另可改、可增其它WS类应用，参考对应的服务端单一应用配置示例。）

2、C=shadowsocks+xray-plugin/v2ray-plugin+tls（TLS由caddy提供及处理，不需配置。）

3、D=vless+h2c+tls（TLS由caddy提供及处理，不需配置。另可改、可增其它H2C类应用，参考对应的服务端单一应用配置示例。）

4、G=vless+grpc+tls（TLS由caddy提供及处理，不需配置。另可改、可增其它gRPC类应用，参考对应的服务端单一应用配置示例。）

5、A=vless+kcp+seed（可改成vmess+kcp+seed，或添加它。）

6、naiveproxy（基于caddy的改进版forwardproxy插件实现，TLS由caddy提供及处理。）

注意：

1、Xray 版本不小于 v1.4.0 或 v2ray 版本不小于 v4.36.2 才支持 gRPC 传输方式。

2、caddy 版本不小于 v2.2.0 才支持 H2C proxy，即支持 Xray 或 v2ray 的 H2C（gRPC） 反向代理。caddy 版本不小于 v2.5.3 才支持 H2C proxy 的进程转发。

3、使用本人 Releases 中编译好的 caddy 文件，可同时支持 H2C proxy、naiveproxy 等应用。

4、本示例中 naiveproxy 除了支持 HTTP/2 代理应用，还同时支持 HTTP/3 代理应用，即 QUIC 协议传输。

5、本示例 caddy 的 Caddyfile 格式配置与 json 格式配置二选一即可（完全等同）。支持自动 HTTPS，即自动申请与更新 SSL/TLS 证书，自动 HTTP 重定向到 HTTPS。

6、配置1：采用端口转发。配置2：采用进程转发（shadowsocks+xray-plugin/v2ray-plugin+tls 反向代理部分除外）。
