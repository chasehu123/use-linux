# 安装

- [ ] 虚拟机, 我使用的是 [Oracle VM VirtualBox](https://www.virtualbox.org/)
- [ ] Linux 镜像, 我使用的是 [Fedora-Server-35](https://mirrors.tuna.tsinghua.edu.cn/fedora/releases/35/Server/x86_64/iso/)
- [ ] SSH 软件, 我使用的是 [XShell 官方免费版](https://www.netsarang.com/en/xshell/)



# 关键步骤

## 网卡配置

1. 一般默认为 NAT 模式, 仅能访问外部网络;

2. 建议设置两张网卡, 一张 NAT, 另一张 Host-Only, **网卡在虚拟机关闭的情况下才能设置**;

3. 测试配置是否成功:

   ```bash
   # 外网
   ping www.baidu.com
   # 内网
   ip addr
   ```

## Linux 基本设置

```bash
# add user
useradd chase
passwd chase

# edit sudoers file
vim /etc/sudoers

# 以下所有操作最好切换到普通用户, 而非 root
su chase
cd
```



## 镜像源

```bash
sudo mv /etc/yum.repos.d/fedora.repo /etc/yum.repos.d/fedora.repo.bak

sudo mv /etc/yum.repos.d/fedora-updates.repo /etc/yum.repos.d/fedora-updates.repo.bak

wget -O /etc/yum.repos.d/fedora.repo http://mirrors.aliyun.com/repo/fedora.repo

wget -O /etc/yum.repos.d/fedora-updates.repo http://mirrors.aliyun.com/repo/fedora-updates.repo

sudo yum makecache
```



## 基础软件包

```bash
# base
curl
wget

# shell
tree
neofetch
screen
sshpass

# stress testing
stress
sysstat
sysbench

# dev
gcc
g++
cmake
```





## Git

```bash

# ssh key
ssh-keygen -t rsa -C "3203078092@qq.com"

# git
sudo yum install -y git
git config --global user.email "3203078092@qq.com"
git config --global user.name "chasehu123"
```





## Python3

```bash
sudo yum install python3

sudo ln -s /usr/bin/python3 /usr/bin/python

sudo yum install -y python3-pip

pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```



## Zsh

```bash
# 考虑到访问 GitHub 总是会出现问题, 请一步一步操作

# install
sudo yum install -y zsh
sudo yum install -y autojump

# set default shell
chsh -s /bin/zsh

# oh-my-zsh
git clone https://github.com/ohmyzsh/ohmyzsh.git ~/.oh-my-zsh

git clone https://github.com/zsh-users/zsh-syntax-highlighting ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting

git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-completions.git ~/.oh-my-zsh/custom/plugins/zsh-completions
```



```bash
# ~/.zshrc
# https://github.com/antfu/dotfiles/blob/main/.zshrc


### THEME
ZSH_THEME="ys"

### PLUGIN
plugins=(
    git
    zsh-syntax-highlighting
    zsh-autosuggestions 
    autojump
    zsh-completions
)


### BASE
source $ZSH/oh-my-zsh.sh
HIST_STAMPS="mm/dd/yyyy"



### ALIAS 
alias yi="sudo yum install -y"
alias ys="yum search"
alias ds="dnf search"
alias di="sudo dnf install -y"

alias rf="source ~/.zshrc"

### TMUX
alias tl = "tmux ls"
alias ta = "tmux attach -t"
alias td = "tmux detach -t"
alias tn = "tmux new -s"
alias tk = "tmux kill-session -t"
alias ts = "tmux switch -t"
alias tz = "tmux kill-server"
```







## Tmux

```bash
# install
di tmux
```



```bash
# ~/.tmux.conf
# https://www.ruanyifeng.com/blog/2019/10/tmux.html

# tmux ls \ Ctrl+b+s
# 退出并关闭 session: Ctrl+d \ exit
# 退出但不关闭 session: tmux detach \ Ctrl+b+d
# 创建 session 并指定名字: tmux new -s <xxx>
# 接入 session: tmux attach -t <xxx>
# 杀死 session: tmux kill-session -t <xxx>
# 从一个 session 切换到另一个: tmux switch -t <xxx>
# 重命名 session: tmux rename-session -t <xxx> <xxx>
# 重命名当前 session: tmux rename-session <xxx>

bind \\ split-window -h
bind - split-window -v
set-option -g mouse on
```



## Vim

```bash
# install
di vim
```



```bash
" ~/.vimrc

" base
set nu
set mouse=a
colorscheme desert
```





## Nvim

```bash
# install
di neovim
```



## Node

```bash
# install
di nodejs
```



## Docker

```bash
sudo yum install -y docker

sudo systemctl enable docker

sudo systemctl start docker

sudo docker run hello-world

sudo groupadd docker

sudo chown root:docker /var/run/docker.sock

sudo usermod -a -G docker $USERNAME

echo "

/// MySQL ///
MySQL:

#step zero
reboot

# step one
docker pull mysql

# step two
docker run --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=jian1234 -d mysql

# step three
docker exec -it mysql-test bash

# step four
mysql -u root -p

# more steps
change the mirror source url
/// end ///

"
```





