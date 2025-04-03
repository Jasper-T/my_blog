# Git & SSH
Windows 安装 Git , 使用 Git Bash
## 1 SSH配置
### 1.1 生成 SSH 密钥
```bash
ssh-keygen -t rsa -b 4096 -C    "email@example.com"
```
`-t rsa` : 指定生成的密钥类型为 RSA（最常用的加密算法之一）。

`-b 4096` : 指定密钥的位数为 4096 位

`-C` : 注释, 通常用于标识密钥，如所连接的`服务器对应的授权邮箱`。

### 1.2 连接Github
1.  启动 SSH 代理
    ```bash
    eval $(ssh-agent -s)
    ```
    如果运行成功，你应该看到类似如下的输出：
    ```yaml
    Agent pid 1234
    ```
    然后，运行以下命令将 SSH 密钥添加到代理中：
    ```bash
    ssh-add ~/.ssh/id_rsa
    ```
2.  检查 SSH 配置
   
    确保 SSH 配置文件没有问题：
    ```bash
    nano ~/.ssh/config
    ```
    确保文件内容：
    ```config
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
    ```bash
    ssh -T git@github.com
    ```
    如果成功，你会看到类似如下的输出：
    ```
    Hi "username" ! You've successfully authenticated, but GitHub does not provide shell access.
    ```

### 1.3 连接服务器
1. 添加密钥
   ```bash
    ssh-copy-id -i ~/.ssh/id_rsa.pub User@HostName -p 22
    ```
2. 检查 SSH 配置
    确保 SSH 配置文件没有问题：
    ```bash
    nano ~/.ssh/config
    ```
    确保文件内容：
    ```config
    Host Server1
        HostName 233.233.233.233
        Port 22
        User Username
        IdentityFile ~/.ssh/id_rsa
    ```
    保存并退出

