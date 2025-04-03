# Server 远程服务器开发

主要涉及到网络以及ssh配置相关的问题

## ssh

```bash
ssh-genkey

ssh-copy-id -i ~/.ssh/id_rsa.pub User@HostName -p Port

vim ~/.ssh/config
```

```
Host Server1
    HostName 233.233.233.233
    Port 22
    User Username
    IdentityFile ~/.ssh/id_rsa
    
```
`IdentitiesOnly yes` 只接受 SSH key 登录

--------------------------------------------------

**[返回主页](/README.md)**