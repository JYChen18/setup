# Intro
This repo records some steps to initialize my faviorate work environment (including oh-my-zsh, conda, pytorch) on a new Ubuntu machine.

### Commonly used commands

```
df -h          # see the memory usage of each disk
du -d 1 -h     # see the memory usage of a folder
```

### Clash

quick links: [Tutorial](https://segmentfault.com/a/1190000041862051), [clash](https://github.com/Dreamacro/clash/releases/)

```
# download
unzip Clash.zip    # online link is not supported anymore. Use our zip file.
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


2. Modify the defualt theme and add the plugin (inside ~/.zshrc):
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
wget https://repo.anaconda.com/miniconda/Miniconda3-py38_4.12.0-Linux-x86_64.sh

# Install 
sh Miniconda3-py38_4.12.0-Linux-x86_64.sh
```

To create and remove environments,
```
# create new envs
conda create -n ${ENV_NAME}

# remove envs
conda remove -n ${ENV_NAME}
```


### Qinghua Mirror

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


### pytorch

quick-links: [pytorch](https://pytorch.org/get-started/previous-versions/)

NOTE: If you are using Qinghua Mirror through pip to install pytorch, the default version of torch is CUDA10.2. It may have problem to run on machine with CUDA 11.0+ !

NOTE: If you are using Qinghua Mirror through conda to install pytorch, remove '-c pytorch'. (But it may fail to find the suitable version)

Recommended way:

1. Use Clash and move to [pytorch_all_versions](https://pytorch.org/get-started/previous-versions/) and choose the suitable link to run. 

Another possible way: 

1. Choose suitable version and download .whl file from [here](https://download.pytorch.org/whl/torch_stable.html)

2. Directly install from .whl file

```
# stable version 1.9.1+cu111 (Linux, python 3.8)
wget https://download.pytorch.org/whl/cu111/torch-1.9.1%2Bcu111-cp38-cp38-linux_x86_64.whl

# install from .whl file
pip install torch-1.9.1+cu111-cp38-cp38-linux_x86_64.whl

```

### Git

```
git config --global user.email {$YOUR_EMAIL}
git config --global user.name {$YOUR_NAME}
```

