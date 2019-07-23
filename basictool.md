# Tool Box

这里收集了在学习和研究中会使用到的工具，多数为非Linux系统自带的第三方工具。

## 0x00 基础工具

### 1. Vim 插件

~~~ .vimrc
Plugin 'gmarik/Vundle.vim'
Plugin 'godlygeek/tabular'
Plugin 'plasticboy/vim-markdown'
Plugin 'emmet-vim'
Plugin 'jedi-vim'
Plugin 'nerdtree-master'
Plugin 'rainbow_parentheses.vim-master'
Plugin 'syntastic'
Plugin 'tagbar'
Plugin 'vim-multiple-cursors'
Plugin 'vim-powerline-develop'
~~~

### 2. terminal 快捷键
~~~ work
系统设置->设备->键盘->添加
名称: terminal
命令: gnome-terminal
快捷键: Ctrl+T
~~~
### 3. tweaks

~~~ bash
sudo dnf install gnome-tweaks # gnome-tweak-tool
~~~

### 4. pppoe 拨号
~~~ bash 
sudo pppoe-setup       # 设置
sudo /sbin/pppoe-start # 启动
sudo /sbin/pppoe-stop  # 关闭
~~~

### 5. Typora markdown 编辑器
~~~bash
wget https://typora.io/linux/Typora-linux-x64.tar.gz       #下载
tar -xzvf Typora-linux-x64.tar.gz              #解压
vim ~/.local/share/applications/Typora.desktop #设置 Desktop 启动路径
~~~
/PATH 替换成你的 Typora 的路径
~~~desktop
[Desktop Entry]
Version=1.0
Type=Application
Name=Typora
Icon=/PATH/Typora-linux-x64/resources/app/asserts/icon/icon_256x256@2x.png
Exec="/PATH/Typora-linux-x64/Typora"
Comment=Markdown editor
Categories=Development;IDE;
Terminal=false
Name[zh_CN]=Typora
~~~

### 6. TexStudio

~~~bash
sudo dnf install texstudio
~~~

### 7. Chrome

~~~bash
cd /etc/yum.repos.d/
sudo wget  http://repo.fdzh.org/chrome/google-chrome-mirrors.repo
sudo dnf install -y google-chrome-stable
~~~

### 8. IDE

* Cli : vi、vim、nano、emacs

* [CodeBlocks](http://www.codeblocks.org/)
* [VScode](https://code.visualstudio.com/docs/setup/linux)
* [PyCharm](https://www.jetbrains.com/pycharm/)
* [Sublime](https://www.sublimetext.com/)

## 0x01 架构工具

### 1. Vmware 虚拟机

Vmware WorkStation Pro [Downloads](https://my.vmware.com/en/web/vmware/downloads/ )

Vmware 虚拟机管理:
~~~ vmware
vmware -v                      # 看esx版本
vim-cmd vmsvc/getallvms        # 列出所有虚拟机
~~~
### 2. GNS3 网络架构

### 3. Anaconda 管理Python环境

Anaconda [Downloads](https://www.anaconda.com/distribution/)

**安装**

~~~ bash
export PATH=/home/user/anaconda3/bin:$PATH
~~~

**Keras环境**

```bash
# 创建环境
conda create --name py36 python=3.6

# 进入环境
activate keras-cpu
deactivate
# 进入环境
conda activate keras-cpu
conda deactivate

conda install tensorflow keras sklearn
```

### 4. VNC 服务器

### 5. Teamviewer 远程办公


## 0x02 服务架构

### 1. DNS 域名解析

### 2. Apache http 服务器

### 3. FTP 服务器

~~~bash
sudo dnf install vsftpd
sudo systemctl disable firewalld
sudo systemctl stop firewalld
sudo systemctl start vsftpd
sudo systemctl enable vsftpd
~~~

~~~txt
anonymous_enable=YES    #允许匿名访问  
local_enable=YES    #允许本地用户访问(/etc/passwd中的用户)  
write_enable=YES    #允许写入权限，包括修改，删除  
anon_upload_enable=YES    #允许匿名用户上传  
anon_mkdir_write_enable=YES    #允许匿名用户建立目录  
ascii_upload_enable=YES    #允许ascii上传  
ascii_download_enable=YES        #允许ascii下载  

userlist_deny=YES
local_root=/var/ftp/pub
~~~


### 4. ELK日志管理 

使用 zookeeper 管理 kafka，将数据输入到 logstash

ELK [Downloads](https://www.elastic.co/cn/start)

~~~bash
sudo dnf install zookeeper kafka
~~~

### 5. Zeek(Bro)

Zeek(Bro) [Downloads](https://www.zeek.org/download/index.html)

~~~bash
sudo dnf install bro
~~~

## 0x03 大数据分析架构

### 1. 大数据分析框架 [Bro-ELK](https://www.freebuf.com/sectool/179757.html)