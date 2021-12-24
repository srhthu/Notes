# 误删/var/lib/dpkg/info
/var/lib/dpkg/info 保存各个软件包的配置文件列表.
解决方案：
```
sudo apt-get --reinstall install `dpkg --get-selections | grep '[[:space:]]install' | cut -f1`
```
重新下载所有包

出现错误 `E: Sub-process /usr/bin/dpkg returned an error code (1)` 在安装包`grub-efi-amd64-signed`时
```
cd /var/lib/dpkg/
sudo mv info/ info_bak          # 现将info文件夹更名
sudo mkdir info                 # 再新建一个新的info文件夹
sudo apt-get update             # 更新
sudo apt-get -f install         # 修复
sudo mv info/* info_bak/        # 执行完上一步操作后会在新的info文件夹下生成一些文件，现将这些文件全部移到info_bak文件夹下
sudo rm -rf info                # 把自己新建的info文件夹删掉
sudo mv info_bak info           # 把以前的info文件夹重新改回名
```