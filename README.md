# envfuck

fuck environment setup
## Ubuntu
换源 https://mirror.sjtu.edu.cn/ubuntu

```bash
sudo apt update
sudo apt install git tmux python3 python3-pip wget proxychains4 zsh
git config --global user.name "Ainevsia"
git config --global user.email "zhipengxu@sjtu.edu.cn"
ssh-keygen -t ed25519

# install docker
sudo apt install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
## post docker installation
sudo usermod -aG docker $USER

# tmux config file
wget -O ~/.tmux.conf https://raw.githubusercontent.com/Ainevsia/.config/master/.tmux.conf
wget -O ~/.tmux.conf.local https://raw.githubusercontent.com/Ainevsia/.config/master/.tmux.conf.local

# proxychains
# 使用 sed 命令将文件的最后一行替换为新的内容
sudo sed -i 's/^socks.*/socks5 127.0.0.1 1080/' /etc/proxychains4.conf

# oh-my-zsh
proxychains sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
