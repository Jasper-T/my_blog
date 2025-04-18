# 《论如何使用VS Code + Anaconda进行Python项目开发》

## 1 项目目录结构

## 2 VSCode开发环境配置

### 2.1 基础设置

- **详细文档👉：[vscode.md](/doc/QA/vscode.md)**

### 2.2 Python相关


## 3 Python 下载与安装

### 🛠 下载与安装步骤

- 镜像源：<https://mirrors.huaweicloud.com/python/>

  ```shell
    下载
    wget https://mirrors.tuna.tsinghua.edu.cn/python/3.11.8/Python-3.11.8.tgz
    
    # 解压
    tar -xzf Python-3.11.8.tgz
    cd Python-3.11.8

    # 安装依赖
    sudo apt update
    sudo apt install -y build-essential libssl-dev zlib1g-dev \
      libncurses5-dev libncursesw5-dev libreadline-dev libsqlite3-dev \
      libgdbm-dev libdb5.3-dev libbz2-dev libexpat1-dev liblzma-dev tk-dev

    # 配置
    ./configure --enable-optimizations

    # 编译 & 安装
    make -j$(nproc)
    sudo make altinstall
  
  ```

## 4 Anaconda安装

### 4.1 容器中安装

  1. update

  ```shell
    apt-get update
  ```

  2. 检查容器中可用的语言环境

  ```shell
    locale -a
  ```

  3. 安装必要的语言环境支持

  ```shell
    apt-get install -y locales
    dpkg-reconfigure locales
  ```

  在交互式界面中，选择"en_US.UTF-8"或"C.UTF-8"。
  
  4. locale -a
  
  5. 设置语言环境

  ```shell
    export LC_ALL=C.utf8
    export LANG=C.utf8
  ```

### ...


------------------------------------------------------------

**[返回Python](/doc/QA/python/README.md)**
