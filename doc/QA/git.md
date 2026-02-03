# Git & SSH

Windows 安装 Git , 使用 Git Bash

## 1 SSH配置

### 1.1 生成 SSH 密钥

```shell
ssh-keygen -t rsa -b 4096 -C    "email@example.com"
```

`-t rsa` : 指定生成的密钥类型为 RSA（最常用的加密算法之一）。

`-b 4096` : 指定密钥的位数为 4096 位

`-C` : 注释, 通常用于标识密钥，如所连接的`服务器对应的授权邮箱`。

### 1.2 连接Github

1. 启动 SSH 代理

    ```shell
    eval $(ssh-agent -s)
    ```

    如果运行成功，你应该看到类似如下的输出：

    ```yaml
    Agent pid 1234
    ```

    然后，运行以下命令将 SSH 密钥添加到代理中：

    ```shell
    ssh-add ~/.ssh/id_rsa
    ```

2. 检查 SSH 配置

    确保 SSH 配置文件没有问题：

    ```shell
    nano ~/.ssh/config
    ```

    确保文件内容：

    ```yaml
    Host git
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_rsa
        AddKeysToAgent yes
    ```

    保存并退出
3. 复制pub key至GitHub

    **Settings** -> **SSH and GPG keys** -> **New SSH Key** -> **Add SSH Key**

4. 测试 SSH 连接(github)

    ```shell
    ssh -T git@github.com
    ```

    如果成功，你会看到类似如下的输出：

    ```yaml
    Hi "username" ! You've successfully authenticated, but GitHub does not provide shell access.
    ```

### 1.3 连接服务器

1. 添加密钥

   ```shell
    ssh-copy-id -i ~/.ssh/id_rsa.pub User@HostName -p 22
    ```

2. 检查 SSH 配置
    确保 SSH 配置文件没有问题：

    ```shell
    nano ~/.ssh/config
    ```

    确保文件内容：

    ```yaml
    Host Server1
        HostName 233.233.233.233
        Port 22
        User Username
        IdentityFile ~/.ssh/id_rsa
    ```

    保存并退出

--------------------------------------------------

## 分支管理策略：Git Flow

1. main 分支：

始终保持可发布状态，生产环境中的代码。

每次发布都会创建一个新的版本标签（如 v1.0.0）。

只有通过 release 或 hotfix 合并的代码才会出现在 main 分支上。

develop 分支：

所有新的功能和修复首先合并到 develop 分支。

作为开发中的“最新”版本，不可直接用于生产。

feature/* 分支：

每个新的特性都从 develop 分支创建一个新的 feature 分支。

开发完成后，合并回 develop。

release/* 分支：

当开发完成且准备发布时，从 develop 创建 release/* 分支。

release 分支主要用于 bug 修复、文档修改和版本号更新。

完成后合并到 main 和 develop 分支。

hotfix/* 分支：

当 main 分支上的生产环境发现紧急 bug 时，从 main 创建 hotfix/* 分支进行修复。

完成后合并到 main 和 develop，并打上新标签。

**[返回主页](/README.md)**
