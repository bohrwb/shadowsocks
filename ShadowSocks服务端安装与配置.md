# ShadowSocks服务端安装与配置

> [参考文档](https://jdhao.github.io/2017/08/06/vps-ss-issue-solution/)

使用root用户登录，运行以下命令：

1. ```text
   wget --no-check-certificate -O shadowsocks.sh https://cyh.abcdocker.com/vpn/shadowsocks.sh
   ```

2. ```text
   chmod +x shadowsocks.sh
   ```

3. ```text
   ./shadowsocks.sh 2>&1 | tee shadowsocks.log
   ```

安装完成后，脚本提示如下： 

```text
1. Congratulations, Shadowsocks-python server install completed!
2. Your Server IP :your_server_ip
3. Your Server Port :your_server_port
4. Your Password :your_password
5. Your Encryption Method:your_encryption_method
6. Welcome to visit:https://teddysun.com/342.html
7. Enjoy it!

```



卸载方法： 
使用root用户登录，运行以下命令： 

1. ```text
   ./shadowsocks.sh uninstall
   ```

配置文件路径：/etc/shadowsocks.json

```json
{
   "server":"0.0.0.0",
   "server_port":"1998",
   "local_address":"127.0.0.1",
   "local_port":1080,
   "password":"9cyh.net",
   "timeout":300,
   "method":"aes-256-cfb",
   "fast_open": false
}
```



多用户多端口配置文件
配置文件路径：/etc/shadowsocks.json

```json
{
    "server":"0.0.0.0",
    "local_address":"127.0.0.1",
    "local_port":1080,
    "port_password":{
        "8989":"password0",
        "9001":"password1",
        "9002":"password2",
        "9003":"password3",
        "9004":"password4"
    },
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}

```

新增的端口可能由于firewall的屏蔽而无法使用，需要把新增的端口加入白名单

```shell
firewall-cmd --permanent --zone=public --add-port=1234/tcp
firewall-cmd --permanent --zone=public --add-port=1234/udp
systemctl restart firewalld
```



```text
启动：/etc/init.d/shadowsocks start
停止：/etc/init.d/shadowsocks stop
重启：/etc/init.d/shadowsocks restart
状态：/etc/init.d/shadowsocks status
```

