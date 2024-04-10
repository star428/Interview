# linux

## 计算机系统基础

### linux常用命令

#### 文件和目录

##### cd: 切换目录

```shell
cd .. // 返回上一级
cd ~ // 返回用户主页
cd - // 返回上一个目录

```

##### pwd: 显示工作路径

##### ls: 查看当前文件与目录命令

```shell
ls -l // 显示文件和目录的详细资料
ls -a // 列出所有文件，包含隐藏文件
ls -R // 连同子目录的内容一起列出，该目录下的所有文件都会显示
```

##### cp, mv命令：copy和move

##### rm: 删除文件或目录

```shell
rm -f // 忽略不存在的文件
rm -r // 递归删除该文件夹下所有文件
```

#### 查看文件内容

##### cat命令

```shell
cat file1 // 从第一个字节开始正向查看文件的内容
tac file1 // 从最后一行开始反向查看一个文件的内容(倒叙输出行)
cat -n file // 标记文件的行数
head -n 2 file // 查看一个文件的前两行
tail -n 2 file // 查看一个文件的后两行
tail -n +100 file // 从100行开始，显示100行以后的
cat file | tail -n +10 | head -n 10 // 从10行开始，输出10行
```

#### 文件搜索

##### find：查找相关文件

```shell
find / -name file1 // 从‘/’目录开始搜索相关名字的文件和目录
find / -user user1 // 从‘/’目录开始查找用户‘user1’的文件和目录
find / -type f -atime +100 // （access）在‘/’目录下开始查找超过100天（-100 就是100天内）内未访问的文件（atime为访问）
find / -type f -mtime -100 // （modified）搜索在10天内被创建或者修改过的文件
whereis [命令/ls/。。。] // 显示一个用于定位特定命令的二进制文件、源代码文件和帮助文档的路径。
```

#### 文件权限

##### chmod：给某个文件加权限

```shell
chmod +755 fileName
chmod：4读，2写，1执行，755代表给文件添加者给全部权限，给组用户给读+执行，给其他用户读+执行
```

#### 文本处理

##### grep：分析行是否包含某个字符串

```shell
grep Aug [路径] // 在文件路径中寻找含有Aug的行
grep ^Aug [路径] // 查找以Aug开头的行，以Aug结尾的行使用grep Aug$
grep [0-9] [路径] // 选择文件中含有数字的行([0-9]还可以写成[a-z]感觉就是一个范围内的都会选中)
```

#### 进程相关命令

##### ps：显示进程

```shell
-A // 所有进程均显示
-a // 不与termial有关的所有进程
-u username // 有效用户的相关进程
-x // 列出详细信息
-l // 较长，详细列出PID信息(跟x的输出有些不同)
```

##### kill：结束某个进程

```shell
kill PID // 结束某个进程
```

##### top: linux常用性能分析工具

```shell
top -d 1 // 1s刷新一次
top -u <username> // 显示特定用户的进程
top -p <PID> // 只显示特定进程

交互界面：
k：终止指定进程
r：改变进程优先级
q；退出top命令
```

#### 网络

##### netstat：查看网络链接状态

```shell
-a // --all 所有连接和监听端口
-t // --tcp TCP协议相关连接
-u // --udp UDP协议相关连接
-p // --program 显示与连接相关的进程
-r // --route 显示路由表

```

```sql
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State  
tcp        0      0 localhost:40099         0.0.0.0:*               LISTEN   
tcp        0      0 localhost:40241         0.0.0.0:*               LISTEN   
tcp        0      0 localhost:35215         0.0.0.0:*               LISTEN   
tcp        0      0 localhost:46624         0.0.0.0:*               LISTEN   
tcp        0      0 localhost:41613         0.0.0.0:*               LISTEN   
tcp        0      0 localhost:44041         0.0.0.0:*               LISTEN   
tcp        0      0 localhost:49153         0.0.0.0:*               LISTEN   
tcp        0      0 localhost:49152         0.0.0.0:*               LISTEN  
```

##### route: 查看路由表

```sql
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         0h.xjtu.edu.cn  0.0.0.0         UG    100    0        0 eno1
link-local      0.0.0.0         255.255.0.0     U     1000   0        0 eno1
172.17.0.0      0.0.0.0         255.255.0.0     U     0      0        0 docker0
202.117.43.0    0.0.0.0         255.255.255.0   U     100    0        0 eno1
```

* Destination（目的地址）：目的地址，表示目的网络地址或目的地主机的IP地址，default表示匹配不到这个子网
* Gateway（网关）：下一跳路由器的IP地址，未指定网关，表示直接连接到本地子网
* Genmask（子网掩码）：用于确定目标地址是不是和路由表上的Destnation对应
* Flag（标志）：
  * U（up）：路由是活动的（有效不需要再配置）
  * G（Gateway）：表示路由需要通过网关
* Iface（接口）：发送的网卡

## 服务器编程

### select，poll，epoll

IO多路复用技术，同时处理多个IO操作

* select：同时监视多个文件描述符FD（file describer）的IO状态（可读，可写，异常）
* poll：使用文件描述符数组
* epoll：linux特有的高效IO多路复用技术，使用事件驱动方式处理IO操作，只会返回就绪的文件描述符

### 边缘触发和条件触发

边缘触发只触发一次，条件触发会持续触发

### client & Server通信双方API调用流程

## 同步与异步，阻塞与非阻塞

同步异步关注的是调用者与被调用者的关系

阻塞与非阻塞更关注IO操作的行为
