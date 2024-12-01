---
title: Linux Git
summary: Install and use Git under Linux
data: 2024-12-01
---

### 1.Install using your Linux distribution's preferred package manager
---

The easiest way to install Git on Linux is to use your Linux distribution's preferred package manager.

#### Debian/Ubuntu
```bash
sudo apt-get install git
```

#### Fedora
Versions up to Fedora 21
```bash
sudo yum install git 
```
Fedora 22 and later
```bash
sudo dnf install git
```

#### CentOS/RHEL
```bash
sudo yum install git 
```

### 2.Install using source code package
---

#### Download Git source code package
Visit the Git official website `https://git-scm.com/downloads/linux` to download the Git source code package and decompress it.For example: git-2.47.1.tar.gz.
- Expand the source package and enter the corresponding directory.
```bash
 tar -jxvf git-1.7.3.5.tar.bz2
 cd git-1.7.3.5/
```
- The installation method is written in the INSTALL file. Follow the instructions to complete the installation. The following command installs Git in `/usr/local/bin`.
```bash
 make prefix=/usr/local all
 sudo make prefix=/usr/local install
```

After the installation is complete, you can find the git command in `/usr/local/bin`.

#### Autocomplete settings

The Linux shell environment (bash) provides command completion through the` bash-completion` software package, which enables you to press the TAB key once or twice when entering command parameters to automatically complete or prompt the parameters. For example, if you enter git com and press the TAB key, it will automatically complete to git commit.

When installing Git through a package manager, automatic completion is usually configured for Git. However, if you install Git by compiling from source code, you need to do the following.

- Copy the command completion script in the Git source package to the directory corresponding to `bash-completion`.
```bash
cp contrib/completion/git-completion.bash \
     /etc/bash_completion.d/
```

- Reload the auto-completion script to make it effective in the current shell.

```bash
. /etc/bash_completion
```

- In order to automatically load the` bash_completion` script when the terminal is opened, you need to add the following content to the local configuration file `~/.bash_profile` or the global file `/etc/bashrc file`.
```bash
if [ -f /etc/bash_completion ]; then
  . /etc/bash_completion
fi
```

### 3.Install using Git repository
---

- Clone the Git repository to your local computer.

```bash
git clone git://git.kernel.org/pub/scm/git/git.git
cd git
```

- If you have cloned a Git repository locally, update it directly in the workspace to obtain the latest version of Git.

```bash
git pull
```

- Perform cleanup to avoid the impact of the previous compilation of the remaining files. Note that the following operation will discard the local changes to the Git code.

```bash
git clean -fdx
git reset --hard
```

- Check Git's milestones and select the latest version to install, for example `v2.47.1`.

```bash
git tag
```

- Check out the code for that version.

```bash
git checkout v2.47.1
```

- Execute the installation. For example, install it in the `/usr/local directory`.

```bash
make prefix=/usr/local all doc info
sudo make prefix=/usr/local install \
  install-doc install-html install-info
```

​	























