sudo apt install aptitude && sudo aptitude full-upgrade && sudo reboot
电脑会重启

sudo aptitude install git

sudo aptitude install npm

sudo aptitude install python-pip

sudo npm install -g ssr-helper

sudo aptitude full-upgrade

cd ～

sudo git clone -b manyuser https://github.com/shadowsocksr-backup/shadowsocksr.git

ssr config ～/shadowsocksr

输入 ssr help 可以查看详细的命令列表

ssr-helper的github地址为 https://github.com/noahziheng/ssr-helper



在执行完方法一或方法二之后可能要将系统代理设置成127.0.0.1：1080 或 给Chrome安装SwitchyOmega插件（此插件的用法请自行Google）

这时Chrome的流量就走SSR了，如何实现系统所有流量都走SSR就需要大家自己Google了，网上有很多方法。

查看ssr-helper服务的状态
sudo systemctl status ssr-helper
使能/禁止/开始/停止/重启ssr-helper服务
sudo systemctl enable ssr-helper
sudo systemctl disable ssr-helper
sudo systemctl start ssr-helper
sudo systemctl stop ssr-helper
sudo systemctl restart ssr-helper