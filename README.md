** 安装Ubuntu20.04 server (exsi)
```
apt update
apt-get upgrade
reboot
```
*安装qbittorent源，安装qbittorent-nox(命令行版)
```
sudo add-apt-repository ppa:qbittorrent-team/qbittorrent-stable
sudo apt install qbittorrent-nox
```
*查看qbittorent-nox 安装成功与否

```
qbittorrent-nox
```
登陆 http://IP:8080 查看qbittorent是否成功启动

*系统添加qbittorent用户
```
sudo adduser --system --group qbittorrent-nox
```
添加sesame用户
```
sudo adduser your-username qbittorrent-nox
```
*系统添加qbittorent启动进程
```
sudo vi /etc/systemd/system/qbittorrent-nox.service
```
添加文本如下,保存退出
```
[Unit]
Description=qBittorrent Command Line Client
After=network.target

[Service]
#Do not change to "simple"
Type=forking
User=qbittorrent-nox
Group=qbittorrent-nox
UMask=007
ExecStart=/usr/bin/qbittorrent-nox -d --webui-port=8080
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
* 设定启动进程
```
sudo systemctl start qbittorrent-nox
sudo systemctl daemon-reload
sudo systemctl enable qbittorrent-nox
systemctl status qbittorrent-nox
```

*1. 访问 http://ip:8080 默认用户名:admin 密码:adminadmin
*2. 进入 设置->webui 更改登录用户名密码 sesame：password

**设置nfs 挂载
*安装nfs服务 
```
sudo apt install nfs-common
```
*新建目录
```
sudo mkdir /mnt/movie /mnt/tv /mnt/action
```

