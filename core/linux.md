# Linux

| 目录     | 作用     |
| -------- | -------- |
| /home    | 用户目录 |
| /root    | root用户 |
| /etc     | 配置文件 |
| /var/log | 日志     |
| /tmp     | 临时文件 |
| /usr/bin | 命令程序 |

## 常用命令

| 命令          | 作用               |
| ------------- | ------------------ |
| pwd           | 当前目录           |
| ls            | 查看文件           |
| ls -l         | 详细列表           |
| ls -al        | 包含隐藏文件       |
| cd            | 切换目录           |
| mkdir         | 创建目录           |
| rm            | 删除               |
| cp            | 复制               |
| mv            | 移动/重命名        |
| touch         | 创建文件           |
| tree          | 树形结构           |
| cat file.txt  | 查看文件全部内容   |
| less file.txt | 分页查看（最常用） |
| more file.txt | 分页查看           |
| head file.txt | 查看前10行         |
| tail file.txt | 查看后10行         |
| find          | 查找文件           |
| locate        | 快速查找文件       |
| which         | 查看命令位置       |
| whereis       | 查看程序位置       |
| grep          | 搜索文本           |
| grep -r       | 递归搜索           |
| grep -n       | 显示行号           |
| grep -i       | 忽略大小写         |
| chmod         | 修改权限           |
| chown         | 修改拥有者         |

## vim or nano

```bash
nano main.py

# Ctrl + O 保存
# Ctrl + X 退出
# Ctrl + K 剪切行
# Ctrl + U 粘贴
```

```bash
vim main.py

# i      插入模式
# Esc    返回命令模式
# :w     保存
# :q     退出
# :wq    保存退出
# :q!    强制退出
```

## 权限(chmod/chown)

```bash
-rwxr-xr-x = - | rwx | r-x | r-x = 文件类型 | 用户(User) | 用户组(Group) | 其他人(Other)

# 第一位
# - = 普通文件
# d = 目录
# l = 软链接

# 后九位
# r = 读（read）
# w = 写（write）
# x = 执行（execute）

# --------------------

chmod +x start.sh
# +x = 增加执行权限
# -x = 移除执行权限
# =rwx = 设置权限

chmod +x start.sh = chmod a+x start.sh # 默认是 a
# u = 用户(User)
# g = 用户组(Group)
# o = 其他人(Other)
# a = 所有人(All)
```

## 网络

| 命令          | 作用             | 常用场景         |
| ------------- | ---------------- | ---------------- |
| `curl`        | 发起 HTTP 请求   | 测试 API         |
| `wget`        | 下载文件         | 下载脚本、安装包 |
| `ping`        | 测试网络连通性   | 检查机器是否可达 |
| `ss`          | 查看端口占用     | 排查服务是否启动 |
| `nc` (netcat) | TCP/UDP 测试工具 | 检查端口是否开放 |
| `dig`         | DNS 查询         | 域名解析排查     |

## systemctl

| 命令                       | 作用              |
| -------------------------- | ----------------- |
| `systemctl status 服务名`  | 查看状态          |
| `systemctl start 服务名`   | 启动              |
| `systemctl stop 服务名`    | 停止              |
| `systemctl restart 服务名` | 重启              |
| `systemctl enable 服务名`  | 开机启动          |
| `systemctl disable 服务名` | 取消开机启动      |
| `journalctl -u 服务名 -f`  | 实时日志          |
| `systemctl daemon-reload`  | 重载 service 配置 |

> 可编写`.service`文件来使用`systemctl`

## journalctl

| 命令                          | 作用         |
| ----------------------------- | ------------ |
| `journalctl -u 服务名`        | 查看服务日志 |
| `journalctl -u 服务名 -f`     | 实时日志     |
| `journalctl -u 服务名 -n 100` | 最近100行    |
| `journalctl --since today`    | 今天日志     |
| `journalctl -p err`           | 错误日志     |
| `journalctl -b`               | 本次开机日志 |
| `journalctl -b -1`            | 上次开机日志 |

## 进程(ps/kill)

| 命令                 | 作用             |
| -------------------- | ---------------- |
| `ps aux`             | 查看所有进程     |
| `ps aux \| grep xxx` | 查找进程         |
| `pgrep -af xxx`      | 查找进程         |
| `top`                | 实时监控         |
| `htop`               | 增强版 top       |
| `kill PID`           | 结束进程         |
| `kill -9 PID`        | 强制结束         |
| `pkill xxx`          | 按名称结束       |
| `ss -lntp`           | 查看端口对应进程 |

```bash
# ps aux | grep uvicorn
# ss -lntp | grep 8000
# kill PID
```

## tar

```bash
压缩 = tar -cvf backup.tar . | tar -czvf backup.tar.gz app/
解压 = tar -xvf backup.tar | tar -xzvf backup.tar.gz -C /opt/

# c = create
# x = extract
# z = zip
# v = verbose
# f = file
```

## apt/yum

| 功能         | Ubuntu(Debian)         | CentOS(RHEL)         |
| ------------ | ---------------------- | -------------------- |
| 更新软件源   | `apt update`           | `yum makecache`      |
| 升级软件     | `apt upgrade`          | `yum update`         |
| 安装软件     | `apt install nginx`    | `yum install nginx`  |
| 卸载软件     | `apt remove nginx`     | `yum remove nginx`   |
| 搜索软件     | `apt search nginx`     | `yum search nginx`   |
| 查看已安装   | `apt list --installed` | `yum list installed` |
| 查看软件信息 | `apt show nginx`       | `yum info nginx`     |

## crontab

```bash
# Crontab：服务器级定时任务

# * * * * * command
# │ │ │ │ │
# │ │ │ │ └── 星期(0-7)
# │ │ │ └──── 月(1-12)
# │ │ └────── 日(1-31)
# │ └──────── 小时(0-23)
# └────────── 分钟(0-59)
```
