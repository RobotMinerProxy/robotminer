# RobotMiner

专业矿池代理，支持 ETH、ETC、BTC、TON、ERG、RVN、LTC、XMR、CFX、KDA。
Web界面操作，简单易用，一键安装，小白可以轻松上手。可以自定义抽水，独创PID抽水算法，稳定精准，秒杀一切市面上随机抽水算法。完美适配各种专业机芯片机。
采用Golang语言开发，性能稳定优异。无视CC，自动CC防护，自动封IP。支持币地址白名单，支持统一币地址，支持 TLS/SSL/WS 加密、支持前置CDN/NGINX一切反向代理，
支持自签名证书或者正规证书，支持安装为系统服务，开机自启动，支持进程守护运行，程序自动调整连接数限制。

## 功能特色

1. 支持主流币种：ETH、ETC、BTC、TON、ERG、RVN、LTC、XMR、CFX、KDA，后续支持更多，欢迎进群反馈。
2. 抽水稳定，创新PID算法，不过抽，不少抽，不像市面上所谓的随机方法，抽水不稳定不准确。
3. 特有的同池模式，专业机器DAG文件不重新下载，实测完美支持：凤凰ETC芯片机，A11-ETH专业机。
4. 兼容模式，实测支持：神马BTC专业机，蚂蚁E7-BTC专业机。
5. 支持ETH和TON双挖，配置方法欢迎进群咨询。
6. 多种挖矿协议支持，完美支持nicehash，stratum。
7. 无视CC，自动CC防护，自动封IP，还支持手动封IP，解封IP。
8. 支持设置币地址白名单，矿机的提交地址，只有在白名单里面中才能连接中转端口，全方位保护中转服务。
9. 支持统一矿机提交币地址，有效拦截矿机内核抽水。
10. 采用Golang语言开发，网络性能优异。
11. 全部web界面操作，简单易用，小白也能轻松驾驭，同时web界面还适配手机，手机上也能轻松操作。
12. 单机4核，4g，稳定带5000+矿机。
13. 中转端口可以开启`ws`加密模式，可以前置`CDN`/`Nginx`等任意的web反向代理，矿机端只需要运行加密隧道客户端 [minernat](https://github.com/RobotMinerProxy/minernat) 即可连接`ws`中转端口，全程加密，防止被监控。
14. 中转端口可以开启`ssl/tls`加密模式，配置域名证书和密钥，全程加密，防止被监控。
15. 支持ssl/tls加密协议和tcp协议。
16. 程序支持注册为系统服务，开机自启动，管理端口可以通过配置文件自由修改。
17. 程序还支持手动普通方式运行，此种方式支持`后台守护`参数运行。
18. 程序自动调整ulimit打开文件数限制，无需手动修改系统配置。

## 系统要求

- 系统类型：Linux: `Debian 9`及以后, `Centos 7`及以后, `Ubuntu 12`及以后。
- 依赖命令：iptables，ipset。
- 一台国外VPS，不要用国内VPS！

## 安装方式

`重要提示：因为会用到iptables，ipset，自动调整系统ulimit连接数限制，所有安装方式都需要root账号权限。`

下面针对不同人群，提供了2种安装方式，选择其中一种进行安装即可。

### 方式一：一键安装

如果是小白，可以执行下面的一键安装脚本，就把"RobotMiner"安装为了系统服务。

```shell
bash -c "$(curl -s -L https://github.com/RobotMinerProxy/robotminer/raw/main/install.sh)" @ install
```

具体程序的`启动`，`停止`，`重启`，`状态`命令如下：

1. 程序启动：`systemctl start robotminer`
2. 程序停止：`systemctl stop robotminer`
3. 程序重启：`systemctl restart robotminer`
4. 程序状态：`systemctl status robotminer`
5. 启动日志：`/etc/robotminer/robotminer logs`
6. 程序卸载：`/etc/robotminer/robotminer uninstall`
7. 程序配置文件路径：`/etc/robotminer/conf`，可以通过修改`/etc/robotminer/conf/app.toml`里面的配置修改程序web管理端口。
8. 默认管理端口是`51301`，假设你的vps的IP是，`192.168.1.1`，那么访问：`http://192.168.1.1:51301` 就可以进入管理登录页面，默认密码是：`123456`
   。进入后台后，点击右上角头像可以修改密码。

#### 更新程序

更新程序只需要执行：

`
bash -c "$(curl -s -L https://github.com/RobotMinerProxy/robotminer/raw/main/install.sh)" @ update
`

## 使用SSL/TLS加密

### 自定义证书

`RobotMiner`后台`端口页面`上传自定义证书，端口就使用上传的自定义证书，不需要再手动设置下面的`默认证书`。

### 默认证书

1. 准备证书文件：  
程序默认自带了自签名证书，位于`/etc/robotminer/conf`目录下面，分别是证书文件`server.crt`和私钥`server.key`,
如果需要用自己的正规证书，只需要把你的证书改名成`server.crt`，私钥文件改成`server.key`。
覆盖`/etc/robotminer/conf`目录下面的同名文件即可。

2. 端口启用SSL/TLS加密  
   在添加或者修改矿池页面，本地协议选择`TLS`，`默认证书`即可，然后在首页重载服务，矿机就可以使用SSL加密方式连接此端口了。

## ETH TON 双挖注意事项
### ETH TON 双挖现已完美支持，但有一定限制.请仔细阅读以下说明并按照要求配置

1.Windows下支持ETH TON双挖的内核有 `teamredminer` [下载地址](https://github.com/todxx/teamredminer/releases/) 请在命令行参数中添加 `--ton_pool_mode=icemining`

2.由于不同TON矿池所用协议不同，目前TON只支持内置的`TON Whales`矿池地址，请勿手动添加其他地址

3.使用双挖时务必将ETH代理模式调整为`兼容模式`！！！

### teamredminer 实例说明：

`teamredminer.exe -a ethash -o stratum+tcp://[ETH代理IP:端口] -u [ETH钱包地址].[矿机名] -p x --ton -o stratum+tcp://[TON代理IP:端口] -u [TON钱包地址].[矿机名] -p x --ton_pool_mode=icemining --ton_end`

注意使用实际真实地址后，不要带[ ]。
