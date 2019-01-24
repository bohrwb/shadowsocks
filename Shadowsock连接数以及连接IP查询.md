# Shadowsock连接数以及连接IP查询

1. 创建文件例如 shadowsocks_monitor

   ```shel
   touch  shadowsocks_monitor
   ```

2. 修改文件为可执行

   ```shell
   chmod +x  shadowsocks_monitor
   ```

3. 修改文件内容

   ```shell
   #查看Shadowsock链接数量
   #$regex 正则表达式，用来过滤符合规则的端口，例如1998或19[0-2][0-9]
   #netstat -anp | egrep $regex | grep -E "tcp.*ESTABLISHED" | awk '{print $4, $5}' | cut -d: -f2 | sort -u
   
   #要过滤的端口2000-2029
   pattern=20[0-2][0-9]
   #统计行数
   echo -n 'count: '
   netstat -anp | egrep $pattern | grep -E "tcp.*ESTABLISHED" | awk '{print $4, $5}' | cut -d: -f2 | sort -u | wc -l
   #查看各个Ip
   echo 'port    IP'
   netstat -anp | egrep $pattern | grep -E "tcp.*ESTABLISHED" | awk '{print $4, $5}' | cut -d: -f2 | sort -u
   ```
4. 
   ```shell
   当我们执行netstat命令显示 
   -bash: netstat: command not found 
   这是由于网络工具没有安装.执行下面命令就可以了. 
   yum install net-tools
   ```

5. 运行文件

   ```shell
   #在文件所在文件夹执行
   ./shadowsocks_monitor
   ```
