# Intro
This repo records some steps to initialize my faviorate work environment (including oh-my-zsh, conda, pytorch) on a new Ubuntu machine. There are some other guidance at https://pengsida.notion.site/59569d7b66954578b21bf1dc6ea35776.

### Commonly used commands

```
df -h          # see the memory usage of each disk
du -d 1 -h     # see the memory usage of a folder
nvidia-smi     # GPU utility
top            # CPU utility
nvitop        # GPU utility. But it need to install https://github.com/XuehaiPan/nvitop
```

### Clash

The online link is not supported anymore. 
If we are on the same server, you can directly use mine with
```
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7891
```

Alternatively, ask me for the ZIP file and build it yourself. 
```
# download
unzip Clash.zip    
wget -O config.yaml [代理商提供的订阅链接]    # your vpn config

# run
cd Clash
./clash -d .

# Open another terminal and set proxy for the system. 
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7891

# cancel proxy
unset https_proxy
unset http_proxy
unset all_proxy
```

### ZSH

quick-links: [oh-my-zsh](https://ohmyz.sh/#install), [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md)

1. Install
```
# install oh-my-zsh. Need Clash!
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"

# install zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

To use zsh as the default one, add the following two lines to `~/.bash_profile` and reconnect the server.

```
export SHELL=`which zsh`
[ -z "$ZSH_VERSION" ] && exec "$SHELL" -l
```


2. Modify the default theme and add the plugin (inside ~/.zshrc):
```
ZSH_THEME="flazz"

plugins=( 
    git
    zsh-autosuggestions
)
```


### Conda 

quick-links: [miniconda](https://docs.conda.io/en/latest/miniconda.html), [Anaconda](https://www.anaconda.com/products/distribution)

```
# Download Miniconda (Linux, python 3.8)
wget https://repo.anaconda.com/miniconda/Miniconda3-py310_25.1.1-2-Linux-x86_64.sh

# Install 
sh Miniconda3-py310_25.1.1-2-Linux-x86_64.sh
```

To create and remove environments,
```
# create new envs
conda create -n ${ENV_NAME}

# remove envs
conda remove -n ${ENV_NAME}
```


### Qinghua Mirror (Deprecated)

NOTE: If using clash, no need to do the following things!

Quick-links: [pip](https://mirrors.tuna.tsinghua.edu.cn/help/pypi/)

```
# pip 
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

# conda 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --set show_channel_urls yes

# remove conda channels
conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/

```


### PyTorch

quick-links: [pytorch](https://pytorch.org/get-started/previous-versions/)

Recommended way: Use Clash and move to [pytorch_all_versions](https://pytorch.org/get-started/previous-versions/) and choose the suitable link to run. 


### Git

To connect to github, first run 
```
ssh-keygen
```
to generate keys. Then put the public key to -> Settings -> SSH and GPG keys

Then, write the following lines to `~/.ssh/config`
```
Host github.com
    Hostname ssh.github.com
    Port 443
    User git
```
Now you can pull codes. To push codes, you also need 
```
git config --global user.email {$YOUR_EMAIL}
git config --global user.name {$YOUR_NAME}
```

