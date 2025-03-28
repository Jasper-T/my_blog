# 《论如何使用VS Code + Anaconda进行Python项目开发》
## 1 项目目录结构

## 2 VSCode开发环境配置
### 2.1 VSCode安装
官网下载：https://code.visualstudio.com/Download
### 2.2 VSCode插件安装
Better Comments
Project Manager
Pylance
python
Python Debugger
Python Indent
Material Theme
Remote - SSH
## 3 Anaconda安装
### 3.1 容器中安装
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

**[返回Python](./python.md)**
