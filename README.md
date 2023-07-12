# envfuck

fuck environment setup
## Ubuntu
换源 https://mirror.sjtu.edu.cn/ubuntu

```bash
sudo apt update
sudo apt install git tmux htop python3 ipython3 python3-pip wget proxychains4 zsh unzip p7zip-full
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
echo 'alias dk="docker"' >> ~/.zshrc

# tmux config file
wget -O ~/.tmux.conf https://raw.githubusercontent.com/Ainevsia/.config/master/.tmux.conf
wget -O ~/.tmux.conf.local https://raw.githubusercontent.com/Ainevsia/.config/master/.tmux.conf.local

# proxychains
# 使用 sed 命令将文件的最后一行替换为新的内容
sudo sed -i 's/^socks.*/socks5 127.0.0.1 1080/' /etc/proxychains4.conf

# oh-my-zsh
proxychains sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# lazygit
LAZYGIT_VERSION=$(proxychains curl -s "https://api.github.com/repos/jesseduffield/lazygit/releases/latest" | grep -Po '"tag_name": "v\K[^"]*')
proxychains curl -Lo lazygit.tar.gz "https://github.com/jesseduffield/lazygit/releases/latest/download/lazygit_${LAZYGIT_VERSION}_Linux_x86_64.tar.gz"
tar xf lazygit.tar.gz lazygit
sudo install lazygit /usr/local/
echo 'alias lg="lazygit"' >> ~/.zshrc

# pip
pip config set global.index-url https://mirror.sjtu.edu.cn/pypi/web/simple
echo 'export PATH=$PATH:$HOME/.local/bin' >> ~/.zshrc
```


# Debain

```bash
sudo sed -i "s|http://deb.debian.org/debian|http://mirror.sjtu.edu.cn/debian|g" /etc/apt/sources.list
```
# Go
```bash
go env -w GO111MODULE=on && go env -w GOPROXY=https://goproxy.cn,direct
```

# Rust 
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
echo '[source.crates-io]\nregistry = "https://github.com/rust-lang/crates.io-index"\n\nreplace-with = "tuna"\n\n[source.tuna]\nregistry = "https://mirrors.tuna.tsinghua.edu.cn/git/crates.io-index.git"' > $HOME/.cargo/config
cargo install --git https://github.com/kamiyaa/joshuto.git --tag v0.9.5
echo 'alias ra="joshuto"' >> ~/.zshrc
mkdir -p $HOME/.config/joshuto
wget -O $HOME/.config/joshuto/keymap.toml https://raw.githubusercontent.com/Ainevsia/.config/master/keymap.toml
wget -O $HOME/.config/joshuto/mimetype.toml https://raw.githubusercontent.com/Ainevsia/.config/master/mimetype.toml
```
