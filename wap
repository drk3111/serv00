#!/bin/bash

# 更新系统并安装依赖
apt update -y && apt install -y unzip wget curl

# 进入root目录
cd /root

# 下载 nezha-agent v0.17.5 (官方地址)
wget -O nezha-agent.zip https://github.com/nezhahq/agent/releases/download/v0.17.5/nezha-agent_linux_amd64.zip
unzip -o nezha-agent.zip
chmod +x nezha-agent
rm -f nezha-agent.zip

# 提示用户输入服务器地址和密钥
read -p "请输入你的探针服务器地址 (格式: IP:端口，例如123.123.123.123:5555)：" server
read -p "请输入你的探针密钥：" key

# 创建 systemd 服务配置文件
cat > /etc/systemd/system/nezha-agent.service <<EOF
[Unit]
Description=Nezha Agent
After=network.target

[Service]
ExecStart=/root/nezha-agent -s $server -p $key -r 30 -d -mode udp
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
EOF

# 启动并使其开机自启
systemctl daemon-reload
systemctl enable --now nezha-agent

# 输出安装完成信息
echo "✅ 安装完成！探针正在启动中，请稍后到控制面板查看上线状态～"
