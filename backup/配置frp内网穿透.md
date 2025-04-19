## 下载frp

https://github.com/fatedier/frp/releases

## 防火墙放行

> 即便ufw未启用，iptables和nft仍有可能进行了拦截。所以先得配置iptables和nft的放行规则。

```bash
sudo nft add rule ip filter INPUT tcp dport 7000 accept
sudo nft add rule ip filter INPUT tcp dport 6000 accept
sudo nft add rule ip filter INPUT tcp dport 6001 accept

sudo iptables -A INPUT -p tcp --dport 7000 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 6000 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 6001 -j ACCEPT

sudo iptables-save | sudo tee /etc/iptables/rules.v4
```

## 配置服务端（中转服务器）

1. 修改frps.toml文件

```toml
bindPort = 7000
auth.method = "token"
auth.token = "<secret_token>"
```

2. 启动并开机自启frps

```bash
chmod -R 777 /<frp文件夹>

cd /etc/systemd/system/
vim frps.service
```

将下面内容写入到frps.service

```txt
[Unit]
Description=Frp Server Service
After=network.target

[Service]
Type=simple
User=<user_name>
Restart=on-failure
RestartSec=5s
ExecStart=/<path_of_frp_dir>/frps -c /<path_of_frp_dir>/frps.toml
ExecReload=/<path_of_frp_dir>/frps -c /<path_of_frp_dir>/frps.toml
LimitNOFILE=1048576

[Install]
WantedBy=multi-user.target
```

开机自启：
```bash
sudo systemctl daemon-reload
sudo systemctl start frps.service
sudo systemctl enable frps.service
```

## 配置客户端

1. 修改frpc.toml文件

```toml
serverAddr = "<中转服务器ip地址"
serverPort = 7000
auth.token = "<secret_token>"

[[proxies]]
name = "ssh"
type = "tcp"
localIP = "127.0.0.1"
localPort = 22
remotePort = 6000
```

2. 启动并开机自启frpc

```bash
chmod -R 777 /<frp文件夹>

cd /etc/systemd/system/
vim frpc.service
```

将下面内容写入到frpc.service

```txt
[Unit]
Description=Frp Client Service
After=network.target

[Service]
Type=simple
User=<user_name>
Restart=on-failure
RestartSec=5s
ExecStart=/<path_of_frp_dir>/frpc -c /<path_of_frp_dir>/frpc.toml
ExecReload=/<path_of_frp_dir>/frpc -c /<path_of_frp_dir>/frpc.toml
LimitNOFILE=1048576

[Install]
WantedBy=multi-user.target
```

开机自启：
```bash
sudo systemctl daemon-reload
sudo systemctl start frps.service
sudo systemctl enable frps.service
```

3. 配置另一台内网机器

frpc.toml

```toml
serverAddr = "<中转服务器ip地址"
serverPort = 7000
auth.token = "<secret_token>"

[[proxies]]
name = "ssh"
type = "tcp"
localIP = "127.0.0.1"
localPort = 22
remotePort = 6001  #注意此处与上一个内网机器的端口需不同。
```

4. 连接

机器1：`ssh -o Port=6000 user1@x.x.x.x`
机器2：`ssh -o Port=6001 user2@x.x.x.x`