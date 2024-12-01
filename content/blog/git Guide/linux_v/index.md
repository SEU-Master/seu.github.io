---
title: Linux Git
summary: Linux下安装和使用Git
date: 2024-12-01
---

## 1.使用Linux发行版的首选包管理器安装

在 Linux 上安装 Git 最简单的方法是使用 Linux 发行版的首选包管理器。

### Debian/Ubuntu

```
sudo apt-get install git
```

### Fedora

最高至Fedora 21

```
sudo yum install git 
```

Fedora 22 及更高版本

```
sudo dnf install git
```

### CentOS/RHEL

```
sudo yum install git 
```



## 2.使用源代码包安装

### 下载Git源代码包

访问Git官网https://git-scm.com/downloads/linux 下载Git的源代码包并解压。

例如：git-2.47.1.tar.gz

```bash
tar -zxvf git-2.47.1.tar.gz 
```

- 进入对应目录后进行编译和安装，指令参考`INSTALL`文件。


```
cd git-2.47.1
```
- 可能需要安装一些需要的依赖（如 `curl`、`gettext`、`zlib`、`openssl`、`perl` 等）

- 下面的命令将Git安装在/usr/local/bin中。

```
make prefix=/usr/local all 
sudo make prefix=/usr/local install 
```
安装完毕之后，就可以在/usr/local/bin下找到git命令。

### 自动补齐设置

Linux的shell环境（bash）通过`bash-completion`软件包提供命令补齐功能，能够实现在录入命令参数时按一下或两下TAB键，实现参数的自动补齐或提示。例如输入**git com**后按下TAB键，会自动补齐为**git commit**。

通过包管理器方式安装Git，一般都已经为Git配置好了自动补齐，但是如果是以源码编译方式安装Git，就需要以下操作。

- 将Git源码包中的命令补齐脚本复制到`bash-completion`对应的目录中。

```bash
cp contrib/completion/git-completion.bash \
     /etc/bash_completion.d/
```

- 重新加载自动补齐脚本，使之在当前shell中生效。

```bash
. /etc/bash_completion
```

- 为了能够在终端开启时自动加载`bash_completion`脚本，需要在本地配置文件`~/.bash_profile`或全局文件`/etc/bashrc`文件中添加下面的内容。

```
if [ -f /etc/bash_completion ]; then
  . /etc/bash_completion
fi
```



## 3.使用Git版本库安装

克隆Git版本库到本地。

```bash
git clone git://git.kernel.org/pub/scm/git/git.git
cd git
```

如果本地已经克隆过一个Git版本库，直接在工作区中更新，以获得最新版本的Git。

```bash
git pull
```

执行清理工作，避免前一次编译的遗留文件造成影响。注意下面的操作将丢弃本地对Git代码的改动。

```bash
git clean -fdx
git reset --hard
```

查看Git的里程碑，选择最新的版本进行安装。例如`v2.47.1`。

```bash
git tag
```

检出该版本的代码。

```
git checkout v2.47.1
```

执行安装。例如安装到`/usr/local`目录下

```bash
make prefix=/usr/local all doc info
sudo make prefix=/usr/local install \
  install-doc install-html install-info
```



## 查看安装git版本

```
git --version
```

