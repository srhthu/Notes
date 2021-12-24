### package install location
```
dpkg -L <packagename>
```

dpkg常用指令
```
# 显示包信息
dpkg -l <pkgname>

# 显示描述
dpkg -s <pkgname>
```

```
sudo apt-get purge `dpkg --get-selections | grep ":i386" | awk '{print $1}'`
dpkg --remove-architecture i386
dpkg --print-foreign-architectures

```

### 源配置文件
位置：`/etc/apt/sources.list`

`/var/lib/apt/lists`存储源的包列表


# apt-get install
apt-get install是下载命令，下载的软件都会存到/var/cache/apt/archives下。  
apt还会检查Linux系统的包依赖关系，简化了用户安装和卸载包的过程。  
要下载一个软件包时，大概需要4步：
1. 扫描本地存放的软件包更新列表，找到最新版本的软件包。
2. 进行软件包依赖关系检查，找到支持该软件的所有软件包。
3. 从镜像站点中下载相关软件包(包含所依赖的软件包)，并存放在/var/cache/apt/archive
4. 解压软件包，并自动完成应用程序的安装和配置。


```
#1. 搜索包
sudo apt-cache search package 

#2.获取包的相关信息，如说明，大小，版本。
sudo apt-cache show package 
 
#3.了解包的依赖
sudo apt-cache depends package

#4.查看该包被那些包依赖
sudo apt-get rdepends package 

#5.安装包
sudo apt-get install package

#6. 安装制定版本的包
sudo apt-get install package=version 

#7.重新安装包
sudo apt-get install package --reinstall

#8.修复安装(启动APT自动安装依赖关系的一个功能键，更新完源之后，如果APT还不能自行解决依赖关系，就可以执行一下这个命令)
sudo apt-get -f install

#下载该包的源代码
9.sudo apt-get source package 

#10.删除包
sudo apt-get remove package 

#11.删除包,包括删除配置文件等
sudo apt-get remove package --purge 

#12.更新apt软件源数据库
sudo apt-get update 

#13.更新已安装的软件包
sudo apt-get upgrade 

#14.升级系统
sudo apt-get dist-upgrade 

#15.使用dselect升级
sudo apt-get dselect-upgrade 

#16.安装相关的编译环境
sudo apt-get build-dep package

#17.清理无用的包
sudo apt-get clean & sudo apt-get autoclean

#18.检查是否有损坏的依赖
sudo apt-get check 
```
提取dependency graph教程
https://askubuntu.com/questions/1060492/generate-a-dependency-graph-for-the-whole-system
