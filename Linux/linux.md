# linux 
## 常用命令
### cd
### ls
### dir
### pwd
* 当前目录
### whoami
### sudo password
* 修改密码
### alt +ctrl
* 切换光标
### ifconfig
### cd . 
* 当前目录
### cd .. 
* 上级目录
## 文件夹命令
### mkdir
* 创建目录
### rm 
* 删除
### rm -R  -f
* 强制递归删除
### rmdir
* 删除目录
### touch 
* 创建文件
### cp
* 复制文件
### mv
* 移动文件
### mv 
* 也可以重命名
### cat
* 输出
### echo
* 输出文件内容
    * echo >> aa.text
### >
* 覆盖
### >>
* 追加
### |
* 管道操作
### more
* 更多信息
### tail -10
* 末尾10行
### head
* 前10行
### nano
* 文本编辑器
## 系统常用命令
### ifconfig
### ping
### hostname
* 查看主机名称
### sudo reboot
* 重启
### find/usr/local |grep XXX
* 查找|过滤
### uname -a
* 操作系统详细信息
### file XXX .so
* 查看文件具体信息
### tar -xvzf
* 解压
### gzip
* （保留）压缩文件
### gunzip
* （不保留）压缩文件
### sudo mount
* 挂载
### sudo umount
### ln -s/exist_file link_name
### jobs
### kill%n
### ps -Af
* 显示进程
### cut -c num1-num2
### man
* 详尽帮助信息
## 目录
### /
* 根目录
### bin/sbin
* 可执行目录
### boot
* 引导
### etc
* 配置目录
### mnt
* 挂载目录
### home
* 主目录
### dev
* 设备
### /usr
## 文件类型
### d
* 目录
### -
* 文件
### c
* 字符文件
### l
* 符号链接
### b
* 块文件
## 权限
### 三种身份
* 文件拥有者
    * rwx:read write execute
* 拥有者所在的组
* other
### chomd
* chomd o+r
* chmod ugo+rw
* chmod a+rwx
* chmod 777

*XMind: ZEN - Trial Version*