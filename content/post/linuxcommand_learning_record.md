+++
title = "常见60个Linux指令"
author = "lyt"
date = "2024-11-30"
description = "A learning record of linux command"
tags = [
    "Linux学习记录"
]
weight = 10 # 加这个可以固定在前面，按升序排列
+++
## 1.ssh 登录到计算机主机
```bash
ssh -p port username@hostname
```

**username：** 远程计算机上的用户账户名。

**hostname：** 远程计算机的 IP 地址或主机名。

 `-p` 选项指定端口号。


## 2.ls 列出目录内容
```bash
ls
ls -l  # 显示详细列表
ls -a  # 显示包括隐藏文件在内的所有内容
```

## 3.pwd 当前终端会话所在的完整路径
```bash
pwd
```

## 4.cd 切换当前工作目录
```bash
cd [directory]
cd .. #上一级目录
cd ~ #返回当前用户主目录
```

## 5.touch 创建空文件或更新文件的时间戳
```bash
touch [options] file
```

## 6.echo 终端输出文本或变量值
```bash
echo [options] [string...]
echo "This is a new line" > newfile.txt #写入文件
echo "Another line" >> existingfile.txt #追加到文件
```
**string**：要输出的文本或变量。

## 7.nano 在终端中编辑文件
```bash
nano [options] [file]
# 例如：创建或编辑文件
nano myfile.txt
```

## 8.vim 文本编辑器
普通模式（Normal Mode）： 默认模式，用于浏览和执行命令。

插入模式（Insert Mode）： 用于文本输入。

命令行模式（Command-Line Mode）： 用于输入命令（如保存、退出等）。

```bash
vim filename.txt
```


## 9.cat 查看、连接和创建文件
```bash
cat filename.txt	#显示文件内容
cat file1.txt file2.txt	#连接多个文件并显示
cat file1.txt file2.txt > combined.txt	#将多个文件合并为一个文件
cat file1.txt >> existingfile.txt	#追加内容到文件末尾
cat -n filename.txt	#显示文件内容和行号
cat -v filename.txt	#显示不可打印字符
```

## 10.shred 安全删除敏感文件
```bash
shred [options] file...
```
`-u`：在删除文件后删除文件名，即在销毁文件内容后删除文件本身。

`-v`：显示详细信息，输出进度信息。

`-n`：指定覆盖文件内容的次数，默认是 3 次。

`-z`：在覆盖后用零填充文件，以进一步掩盖删除的痕迹。

## 11.mkdir 创建新目录
```bash
mkdir [options] directory...
```
`-p`：递归创建目录。如果上级目录不存在，mkdir 会自动创建它们。

`-v`：显示创建目录的详细信息。

`-m`：设置新目录的权限（模式），以八进制表示。

## 12.cp 复制文件和目录
```bash
cp [options] source destination
```
source：要复制的源文件或目录。

destination：目标路径，可以是文件或目录。

`-r`, `--recursive`：递归复制，用于复制目录及其所有内容。

`-i`, `--interactive`：交互模式，如果目标文件已存在则提示是否覆盖。

`-v`, --verbose`：显示详细信息，输出复制操作的详细`信息。

## 13.rm 删除文件和目录
```bash
rm [options] file...
```
-r, --recursive：递归删除，用于删除目录及其所有内容。

-f, --force：强制删除，不提示错误信息，即使文件不存在也不会报错。

-i：交互式删除，在删除每个文件之前都会询问确认。

-v, --verbose：显示详细信息，输出删除操作的详细信息。

-d：删除空目录。

## 14.rmdir 删除空目录
```bash
rmdir [options] directory...
```
`-p`：递归删除目录，即删除指定目录及其所有空的父目录。

`-v`, `--verbose`：显示详细信息，输出删除操作的详细信息。

## 15.ln 创建链接
```bash
ln [options] source [target]
```
`-s`, `--symbolic`：创建符号链接。如果不使用此选项，将创建硬链接。

`-f`, -`-force`：强制创建链接，覆盖已存在的文件或链接。

`-i`, `--interactive`：交互式创建链接，如果目标已存在则提示确认。

## 16.clear 清除终端屏幕
```bash
clear
```

## 17.whoami 显示当前的用户的用户名（确定当前用户身份）
```bash
whoami
id	#当前用户的详细信息，包括用户 ID (UID)、组 ID (GID) 以及所属组
who	#系统中所有当前登录的用户
```

## 18.useradd 创建新用户账户（系统管理员添加新用户）
```bash
sudo useradd [options] username
```
`-m`：创建用户的家目录（/home/username），如果家目录不存在时。

`-d`：指定用户的家目录路径。

`-s`：指定用户的默认 shell（如 /bin/bash）。

`-g`：指定用户的初始主组。

`-G`：指定用户所属的附加组（可以指定多个组，用逗号分隔）。

`-e`：设置用户账户的过期日期（格式为 YYYY-MM-DD）。

`-p`：指定用户的密码（通常是加密后的密码，明文密码不推荐）。

`-c`：添加用户的注释（如全名）。

`-f`：指定用户账户过期后的天数，-1 表示用户账户永不过期。

## 19.sudo 超级用户（root）权限执行命令
普通用户执行管理员权限的任务，而不需要直接登录root用户

使用 sudo 时通常需要输入用户密码，而不是 root 密码

```bash
sudo command [options]
# 以超级用户权限安装软件（例如使用 apt-get）
sudo apt-get update
sudo apt-get install package_name
```

## 20.adduser 创建新用户账户
```bash
sudo adduser [options] username
```
在一些 Linux 发行版中，adduser 是 useradd 的一个友好封装，功能上类似但提供了更多的默认设置和提示。

`--home`：指定用户的家目录路径。

`--shell`：指定用户的默认 shell。

`--gecos`：添加用户的注释（如全名）。

`--ingroup`：指定用户的初始主组。

`--disabled-password`：创建用户时不设置密码。

`--disabled-login`：创建用户时禁用登录。

## 21.su 切换用户账户
`su` 是 "substitute user" 或 "switch user" 的缩写，它可以让你切换到另一个用户账户，包括 root 用户。

```bash
su [options] [username]
su -	#切换到 root 用户并模拟登录
su -c 'ls /home/username' username	# username 用户身份执行 ls 命令列出 /home/username 目录的内容
```

## 22.exit 退出当前终端会话或shell
```bash
exit [n]
```
`n`（可选）：退出状态码。如果指定了状态码，exit 将返回这个状态码。默认情况下，exit 返回上一个命令的退出状态码（通常为 0 表示成功，其他值表示错误）。

## 23.passwd 修改用户密码
在 Unix 和 Linux 系统中，你可以使用 `passwd` 命令来更改自己的密码或其他用户的密码（需要管理员权限）。

```bash
sudo passwd [options] [username]
```
`username`（可选）：要更改密码的用户。如果省略用户名，`passwd` 将修改当前用户的密码。

`-d`：删除用户密码，使用户无法使用密码登录（仅限 root 用户）。

`-l`：锁定用户账户，禁止用户使用密码登录。

`-u`：解锁用户账户，允许用户使用密码登录。

`-e`：强制用户在下次登录时更改密码（即将密码设置为过期状态）。

`-i`：设置密码过期时间，单位为天。若设置为 0，密码会立即过期。

## 24.apt 处理软件包的安装、升级、删除和管理

```bash
sudo apt update	#更新软件包列表
sudo apt upgrade	#升级已安装的软件包
sudo apt full-upgrade	#升级所有软件包并处理依赖关系
sudo apt install package_name	#安装软件包
sudo apt remove package_name	#卸载软件包
```

## 25.finger 显示用户信息
在 Unix 和 Linux 系统中，finger 可以用来查看用户的基本信息、登录状态以及其他与用户相关的细节。
```bash
finger [options] [username]
finger $USER	#查看当前用户的信息
```
`-l`：以详细模式显示用户信息。

`-s`：以简洁模式显示用户信息，只包括基本信息。

## 26.man 查看命令、函数、配置文件和其他程序文档
`man` 是 "manual" 的缩写，通过它你可以访问系统的手册页（manual pages），这些手册页提供了详细的使用说明和参考信息。

```bash
man [options] command
man ls	#查看命令的手册页
```
`-k`：根据关键字搜索手册页。

`-f`：显示命令或函数的简要说明。

`-a`：显示所有匹配的手册页，而不仅仅是第一个。

`-P pager`：指定使用的分页程序。默认是 `less`，但你可以指定其他分页程序，例如 `more`。

## 27.whatis 显示命令或程序的简短描述
`whatis` 命令依赖于系统的手册页数据库，因此如果系统没有更新数据库，或者手册页没有被正确安装，`whatis` 可能无法提供描述。

你可以使用 `mandb` 命令来更新手册页数据库，以确保 `whatis` 命令能提供最新的描述。
```bash
whatis [options] command
```

## 28.curl 从命令行传输数据
`curl` 是一个用于从命令行传输数据的工具，支持多种协议，如 HTTP、HTTPS、FTP、SFTP 等。它通常用于下载或上传文件、测试 API、检索网页内容等任务。

```bash
curl [options] [URL]
```
`-o`：将输出保存到文件中。
`-O`：使用 URL 中的文件名保存文件。
`-d`：发送 POST 请求时使用的数据。
`-H`：添加 HTTP 请求头。
`-i`：显示响应头和响应体。
`-I`：仅显示响应头。
`-L`：跟踪重定向。
`-x`：使用代理服务器。

## 29.zip 创建和管理压缩文件
```bash
zip [options] zipfile files
```
`-r`：递归压缩目录及其子目录和文件。
`-e`：为压缩文件添加密码保护。
`-u`：更新压缩文件，添加新文件或更新已存在的文件。
`-d`：从压缩文件中删除指定的文件。
`-l`：列出压缩文件中的内容。
`-T`：测试压缩文件的完整性。

## 30.unzip 解压缩zip文件
```bash
unzip [options] zipfile
```
`-d`：指定解压缩到的目标目录。
`-l`：列出 .zip 文件中的内容。
`-t`：测试 .zip 文件的完整性。
`-u`：更新目标文件，仅在目标文件比 .zip 文件中的文件旧时更新。
`-o`：覆盖现有文件而不提示。

## 31.less 查看文本文件
`less` 是一个用于查看文本文件的分页工具，可以逐页或逐行浏览文件内容。它比 `more` 命令功能更强大，支持在文件中向前和向后滚动、搜索和其他导航功能。

```bash
less [options] file
```
`-N`：显示行号。
`-S`：禁用自动换行，水平滚动显示长行。
`-F`：如果内容能在一屏内显示，则自动退出 less。
`-X`：禁用终端的显示控制（例如颜色），在使用管道时很有用。

## 32.head 显示文件的开头部分
`head`用于查看文件的前几行内容

```bash
head [options] file
head -n 15 file.txt	#查看 file.txt 的前 15 行
```

## 33.tail 显示文件尾部的部分
`tail`用于查看文件的前几行内容，特别是在查看日志文件时非常有用。

```bash
tail [options] file
tail -n 15 filename.txt	#指定显示的行数
tail -f filename.txt	#实时查看文件的新增内容（跟随模式）
```

## 33.cmp 比较两个文件内容
`cmp`逐字节比较文件内容，并报告文件之间的第一个不同之处。如果文件相同，则没有输出；如果不同，则输出第一个不同字节的位置和它们的不同内容。
```bash
cmp [options] file1 file2
```
`file1`：第一个要比较的文件。`file2`：第二个要比较的文件。
`-l`：显示所有不同字节的位置和它们的不同内容。
`-i`：忽略文件末尾的空白字符。
`-b`：显示所有不同字节的位置和它们的不同内容，以十进制显示。
`-s`：静默模式，不输出任何内容，仅返回退出状态码。0 表示文件相同，1 表示文件不同。
`-i`：指定从哪个字节开始比较。

## 34.diff 比较文件内容并显示差异
`diff`可以显示两个文件之间的不同之处，通常用于文件版本控制和差异分析。

```bash
diff [options] file1 file2
```
`file1`：第一个要比较的文件。`file2`：第二个要比较的文件。
`-u`：以统一格式显示差异。
`-c`：以上下文格式显示差异。
`-q`：简洁模式，仅指示文件是否不同。
`-r`：递归比较目录及其内容。
`-w`：忽略空白字符的差异。
`-i`：忽略大小写的差异。
`-b`：忽略行尾的空白字符差异。

## 35.sort 对文本内容进行排序
可以对文本中的行进行升序或降序排序
```bash
sort [options] file
```
`-r`：按降序排序。
`-n`：按数值排序。
`-u`：去除重复行。# 36.find
`-k`：指定排序字段。字段是通过空白字符或其他指定分隔符分隔的。
`-t`：指定字段分隔符。
`-b`：忽略行首的空白字符。
`-f`：忽略大小写进行排序。
`-M`：按月份排序，适用于日期字段。

## 36.chmod 改变文件或目录权限
在 Unix 和 Linux 系统中，文件和目录的权限控制是确保系统安全的重要组成部分。chmod 允许你设置文件或目录的读、写、执行权限。
```bash
chmod [options] mode file
```
**mode**：权限设置模式，指定新的权限。
**file**：你要修改权限的文件或目录。
权限模式：可以通过符号模式或八进制模式来设置：
**符号模式**：
r：读权限
w：写权限
x：执行权限

权限设置的符号表示方法：
u：用户（文件的所有者）
g：组（文件所属的组）
o：其他（文件的其他用户）
a：所有用户（即 u, g, o 的并集）
操作符：
+：添加权限
-：移除权限
=：设置权限，覆盖已有权限

**八进制模式**：由三个数字组成，每个数字代表文件的用户、组和其他用户的权限：
rwxrwxrwx（表示文件所有者、组、其他用户的权限）
每种权限用一个数字表示：
4：读权限
2：写权限
1：执行权限
这三个数字可以组合成其他权限：
7：读、写和执行（4+2+1）
6：读和写（4+2）
5：读和执行（4+1）
3：写和执行（2+1）
2：写（2）
1：执行（1）
0：没有权限

## 37.chown 更改文件或目录所有者和所属组的命令行
```bash
chown [options] owner:group file
```
**owner**：新所有者的用户名或 UID（用户ID）。
**group**：新所属组的组名或 GID（组ID）。如果省略，chown 只更改所有者。
**file**：你要更改所有权的文件或目录。

`-R`：递归地更改目录及其内容的所有者和所属组。
`--reference=file`：将所有者和所属组更改为另一个文件的所有者和所属组。
`--verbose` 或 `-v`：在更改文件或目录的所有者和所属组时显示详细信息。

## 38.ifconfig 配置和显示网络接口
```bash
ifconfig [interface] [options]
```
**interface**：要配置或查看的网络接口名称（如 eth0、wlan0 等）。
**options**：配置选项或参数。

显示所有网络接口的信息：`ifconfig`
启用（禁用）网络接口：`ifconfig eth0 up（down）`
设置网络掩码：`ifconfig eth0 netmask 255.255.255.0`

## 39.ip address 显示和修改网络接口的地址
```bash
ip address
ip address show [interface]#显示特定网络接口的地址
ip address add [ip_address]/[mask] dev [interface]#添加新的IP地址到网络接口
ip address flush [ip_address]/[mask] dev [interface]#删除网络接口的IP地址
```

## 40.grep 文本搜索
```bash
grep "text" filename
```
`-i`：忽略大小写
`-v`：显示不包含匹配文本的行（反转匹配）
`-n`：显示匹配行及行号
`-E`：使用扩展正则表达式   grep -E "regex1|regex2" filename

## 41.awk 处理和分析文本
```bash
awk 'pattern { action }' filename
awk '/error/ { print $0 }' filename #打印包含 "error" 的行
awk '{ count[$1]++ } END { for (i in count) print count[i] }' filename #计算某个字段出现的次数
awk '{ if ($2 == "value") count++ } END { print count }' filename #计算某个字段中特定值的出现次数
```
**pattern**：一个条件表达式，如果满足条件，那么后面的 action 将被执行。
**action**：当 pattern 匹配成功时执行的一系列命令。
**filename**：要处理的文件名。

## 42.resolvectl status 查询和控制系统DNS解析服务
主要用于与 systemd-resolved 服务交互，后者是 systemd 的一部分，负责处理系统的DNS查询和缓存结果。
```bash
resolvectl [OPTIONS...] COMMAND ...
```
**OPTIONS** 是命令行选项，用于改变 resolvectl 的行为，
**COMMAND** 是想要执行的具体操作。

`-4`: 仅使用 IPv4 查询。
`-6`: 仅使用 IPv6 查询。
`-i IFACE`: 指定查询所用的网络接口。
`-p PORT`: 指定查询所用的端口号。
`-t TYPE`: 指定查询的 DNS 资源记录类型。
`-c CLASS`: 指定查询的 DNS 类别。
`-d`: 启用调试输出。
`-h`: 显示帮助信息。
`-V`: 显示版本信息。

## 43.ping 网络诊断
它通过发送 ICMP（Internet Control Message Protocol）回声请求消息给目标主机，并监听回声应答来检查网络连接。
```bash
ping [选项] [目标主机]
```
**目标主机**：可以是IP地址或域名

`-c`：发送指定数量的回声请求
`-s`：指定发送的数据包大小（字节）
`-i`：指定发送回声请求的时间间隔（秒）
`-t`：设置生存时间（TTL）
`-W`：设置等待回声应答的超时时间（秒）
`-v`：输出详细的诊断信息

## 44.netstat 显示网络状态
它可以提供关于网络连接、路由表、接口状态、伪装连接以及广播域成员等多种网络信息。
```bash
netstat -a #显示所有连接
netstat -t #列出 TCP 协议的连接
netstat -u #列出 UDP 协议的连接
netstat -n #禁用反向域名解析，这可以加快查询速度
```

## 45.ss 显示 socket 统计信息
```bash
ss [options]
```
`-a`：显示所有的套接字，包括监听和非监听的
`-t`：仅显示 TCP 套接字
`-u`：仅显示 UDP 套接字
`-n`：以数字形式显示地址，而不是解析成主机名
`-r`：将主机名解析为 IP 地址
`-i`：显示详细的内部信息。
`-o`：显示 TCP 计时器信息
`-K`：通过 ID 杀死指定的 socket
`-f`：指定协议族（如 inet, inet6, unix, link）
`-v`：显示详细的输出

## 46.iptables 配置网络流量的包过滤规则
iptables 允许管理员设置规则来允许、拒绝、记录或修改经过 Linux 系统的网络流量。
```bash
iptables -A链名 -j动作 规则条件  #添加规则
```
`-A` 表示在链的末尾追加规则，`-j` 指定规则匹配后执行的动作（如 ACCEPT、DROP、REJECT）

```bash
iptables -D链名 -j动作 规则条件 #删除规则
```
`-D` 表示从链中删除规则
```bash
iptables -R链名 规则编号 -j动作 规则条件 #修改规则
```
`-R` 表示替换指定编号的规则

```bash
iptables -L链名 #查看规则
iptables -L链名 -v -n #查看规则详细信息
```
`-L` 表示列出链中的规则  `-v` 表示显示详细信息，`-n` 表示不解析域名

```bash
iptables-save > /path/to/iptables.rules #保存规则
iptables-restore < /path/to/iptables.rules #恢复规则
```

## 47.ufw 管理 iptables 防火墙规则
它是一个用户友好的前端界面，用于管理 iptables 防火墙规则。
```bash
sudo ufw enable #启用
sudo ufw disable #禁用
sudo ufw status #查看当前 ufw 状态
sudo ufw allow http #允许特定服务（例如 HTTP）
```

## 48.uname 显示关于当前系统的特定信息
这个命令是 "Unix name" 的缩写，它可以提供包括内核名称、节点名称、内核发布号、节点名称、系统版本号、机器类型、处理器类型等信息。
```bash
uname [选项]
```
`-a` 或 --all：显示所有信息。
`-s` 或 --kernel-name：显示内核名称。
`-n` 或 --nodename：显示网络节点名称。
`-v` 或 --version：显示内核版本。
`-r` 或 --release：显示系统版本。
`-m` 或 --machine：显示机器类型。
`-p` 或 --processor：显示处理器类型。
`-i` 或 --hardward-platform：显示硬件平台。
`-o` 或 --opeating-system：显示操作系统名称。

## 49.neofetch 显示系统的基本信息和硬件配置
neofetch 能够快速获取关键系统信息，如操作系统、内核、运行时间、软件包、Shell、分辨率、桌面环境、窗口管理器、主题和图标等。
在终端中输入 neofetch 命令，即可显示默认输出，其中包含发行版的 ASCII 徽标和一些系统信息：
```bash
neofetch
```

## 50.cal 在终端中显示一个简单的日历
```bash
cal
cal -y # 显示当前整年的日历
cal -m # 显示当前月份的日历，并且这个日历是从周一开始的
```

## 51.free 显示系统内存使用情况
它可以显示物理内存和交换空间（swap）的总量、已用量、空闲量以及缓冲区和缓存的使用情况。
```bash
free
free -h # 将输出格式化为人类可读的格式
free -m # 查看交换空间（以 MB 为单位）
free -g # 显示内存和交换空间使用情况（以 GB 为单位）
free -t # 显示内存的详细统计信息
```
 - 总内存 (total)
 - 已用内存 (used)
 - 空闲内存 (free)
 - 缓冲区和缓存占用的内存 (buffers 和 cache)

## 52.df 显示文件系统的磁盘空间使用情况
它会显示每个挂载的文件系统的总空间、已用空间、可用空间以及挂载点。df 是查看磁盘空间使用情况的一个非常实用的命令，尤其在系统维护和监控时非常有用。
```bash
df
```
`-h`（human-readable）：以更易读的格式（如 KB、MB、GB）显示空间。
`-T`：显示每个文件系统的类型。
`-i`：显示 inode 使用情况，而不是磁盘空间。
`--total`：显示所有文件系统的总使用情况。

## 53.ps 显示当前系统中进程状态
```bash
ps # 只会显示当前终端会话中的进程信息
```
`a`：显示所有用户的进程。
`u`：以用户格式显示进程。
`x`：显示没有控制终端的进程（包括后台进程）。
`e`：显示所有进程。
`f`：显示进程树。
`l`：显示长格式的信息。
`p PID`：显示指定进程的详细信息。

## 54.top 实时查看系统的资源使用情况
适合用于实时监控系统状态，尤其是在处理服务器性能调优时。
```bash
top # 启动 top 命令，默认显示所有正在运行的进程及系统资源使用情况。
top -u username # 显示指定用户 (username) 的进程。
top -p pid # 显示指定进程 ID (pid) 的信息。
top -d seconds # 设置刷新间隔，seconds 是刷新时间的秒数，默认是 3 秒。
top -n number # 设置更新次数，number 是显示的更新次数。
```

## 55.htop 交互式的进程查看器
htop 允许用户通过上下箭头键选择并操作进程。它提供了更直观的图形界面，可以更轻松地监视 CPU、内存、进程等资源的使用情况。
在 Ubuntu/Debian 系统上，使用以下命令安装：
```bash
sudo apt-get install htop
```

```bash
htop
```
常用操作：
 - F3: 搜索进程 
 - F4: 过滤进程 
 - F5: 切换到树形视图 
 - F6: 排序列，选择排序依据 
 - F9: 杀死进程 
 - F10: 退出

htop 的界面会显示如下信息：
 - CPU: 显示每个 CPU 核心的使用情况。 
 - Memory: 显示内存的使用情况。 
 - Swap: 显示交换分区的使用情况。 
 - Task: 显示当前运行的进程列表，支持排序和过滤。

## 56.kill 终止或发送信号到进程
默认情况下，它发送 SIGTERM（信号 15），请求进程正常终止。可以使用不同的信号来控制进程的行为。
```bash
kill -l # 列出所有可用的信号
kill -<signal_number> <PID> # 发送特定信号
kill -9 <PID> # 强制结束进程（发送 SIGKILL 信号，进程不会处理）
```

## 57.pkill 根据进程名称或其他条件终止进程
它是 kill 命令的一个更高级的版本，可以使用进程名、用户、进程组等条件来查找并终止进程，而无需指定进程的 PID（进程标识符）。
```bash
pkill [选项] <进程名>
```
`-u <用户>`: 根据指定的用户名杀死该用户所有的进程。
`-f`: 匹配完整的命令行，而不仅仅是进程名。
`-9`: 强制杀死进程，类似于 kill -9，使用 SIGKILL 信号。
`-l`: 列出所有匹配的进程名称。
`-n`: 终止最早启动的匹配进程。
`-o`: 终止最晚启动的匹配进程。

## 58.systemctl 管理 systemd 系统和服务管理器
```bash
sudo systemctl start 服务名 # 启动服务
sudo systemctl stop 服务名 # 停止服务
sudo systemctl restart 服务名 # 重启服务
sudo systemctl status 服务名 # 查看服务状态
sudo systemctl enable 服务名 # 用服务开机启动
sudo systemctl disable 服务名 # 禁用服务开机启动
sudo systemctl daemon-reload # 重新加载 systemd 配置
```

## 59.history 显示当前用户在终端中执行过的命令历史
```bash
history
history 10 # 显示最近的 10 条命令历史
history -c # 清除命令历史
history -w # 将命令历史写入文件
history -r # 从历史文件读取命令
```
默认情况下，历史记录会保存在 ~/.bash_history 文件中，且可以通过 HISTSIZE（控制命令历史的条数）和 HISTFILESIZE（控制历史文件的最大大小）进行调整。

## 60.reboot 重启系统
这个命令通常是通过具有管理员权限的用户来执行的，比如root用户，或者是一个拥有足够权限的用户（例如，通过使用sudo命令）。
```bash
reboot
sudo reboot # 立即重启系统（需要根权限）
sudo reboot +5 # 在延迟之后重启系统
sudo reboot 22:00 # 在特定的时间重启系统
```

## 61.shutdown 关闭计算机或重新启动计算机
它可以让你在指定的时间内优雅地关闭系统，通知所有用户系统即将关闭，并可以选择进行重启或关闭。
```bash
sudo shutdown now # 立即关闭系统
sudo shutdown +10 # 会在 10 分钟后关闭系统
sudo shutdown -c # 取消关机
sudo shutdown -r now # 立即重启系统
sudo shutdown -h +5 "System going down for maintenance" # 令将在 5 分钟后关闭系统，并通知所有用户系统将被关闭
```
`-h`：表示关机（halt）。
`-r`：表示重启（reboot）。
`+m`：表示在 m 分钟后执行操作。
`now`：立即执行操作。
`-c`：取消已安排的关机。
`message`：自定义关机前通知消息