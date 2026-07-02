# flux-panel-alpine
flux-panel-alpine


wget https://raw.githubusercontent.com/liang0222/flux-panel-alpine/main/install.sh

安装依赖
Alpine 上只需三个包：

bash
apk add bash curl coreutils dos2unix
Debian/Ubuntu: apt install bash curl  |  CentOS: yum install bash curl

上传 install.sh
wget https://raw.githubusercontent.com/liang0222/flux-panel-alpine/main/install.sh
从本机传到 Alpine 服务器：

bash
# 本机执行
scp install.sh root@你的节点IP:/root/
运行安装
SSH 上服务器，确保行尾正确后运行：

bash
dos2unix install.sh # 如从 Windows 上传，需要转 LF
bash install.sh -a 面板地址:端口 -s 密钥
脚本会自动：检测系统类型 → 下载对应架构的 GOST 二进制 → 创建配置文件 → 注册服务（OpenRC 或 systemd）→ 启动并设为开机自启。

验证节点状态
bash
# 服务状态（OpenRC / systemd 自动适配）
rc-service gost status # Alpine
systemctl status gost # Debian/Ubuntu/CentOS

# 进程检查
ps aux | grep gost

# 手动前台测试（可以看到实时输出）
cd /etc/gost && timeout 5 ./gost
检查面板连通性
bash
nc -zv 面板地址 端口
# 或
curl -I http://面板地址:端口
