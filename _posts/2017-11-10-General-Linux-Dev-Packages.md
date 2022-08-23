---
layout: post
title: Linux packages for developers
---

# Index
Software | Link |
| ------------ | ------------- | 
| [Redshift](#redshift) | [link](https://encrypted.google.com/) | 
| [Github](#git) | [link](https://encrypted.google.com/) | 
| [ZSh](#zsh) | [link](https://encrypted.google.com/) | 
| [htop](#htop) | [link](https://encrypted.google.com/) | 
| [iPython](#ipython) )  | [link](https://encrypted.google.com/) | 
| Nemo File Explorer | [link](https://encrypted.google.com/) | 
| Terminator | [link](https://encrypted.google.com/) | 
| Pulse Audio | [link](https://encrypted.google.com/) | 
| Pycharm | [link](https://encrypted.google.com/) | 
| Sublime Text 3 | [link](https://encrypted.google.com/) | 
| Spring STS | [link](https://encrypted.google.com/) | 
| Eclipse | [link](https://encrypted.google.com/) | 
| Anaconda | [link](https://encrypted.google.com/) | 
| Geany | [link](https://encrypted.google.com/) | 
| MongoDB | [link](https://encrypted.google.com/) | 
| Redis | [link](https://encrypted.google.com/) | 
| Mysql | [link](https://encrypted.google.com/) | 
| Elasticsearch | [link](https://encrypted.google.com/) | 
| Tensorflow | [link](https://encrypted.google.com/) | 
| Google Chrome | [link](https://encrypted.google.com/) | 
| Java | [link](https://encrypted.google.com/) | 


<a name="redshift"></a>
# Redhshift installation: 

```
sudo apt-get gtk-redshift
gtk-redshift -l 2.97:77.59
```

#### Crontab Setup

*Not necessary to setup crontab, use incase auto start option is not available*

**To see the list with the programs you can type**

```
crontab -l
```

**To edit the list type**
```
crontab -e
```

**Add this line in the end, to boot redshift whenever computer starts up**
```
@reboot export DISPLAY=:0.0 && /usr/bin/redshift -l 2.97:77.59
```

*Access help for redshift using:*
```
redshift -h
```

<a name="git"></a>
# Install Git in terminal 
```
sudo apt-get update
sudo apt-get install git

# Enter username and email:
git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"

# To check config items
git config --list

# Edit config:
nano ~/.gitconfig

# To enable password caching so that you need not have to re-enter pwd everytime you git push
git config --global credential.helper "cache --timeout=3600"

```

<a name="zsh"></a>
# Install ZSH shell 

```
apt-get install zsh
apt-get install git-core
```
Then download and install oh-my-zsh for customization using:
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
**------OR------**	
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```
Use source to enable zsh or change shell using:
```
chsh -s `which zsh`
```
Official Github repo for [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)	
Find all themes [here](https://github.com/robbyrussell/oh-my-zsh/wiki/External-themes)	
*Restart if required.* 	

<a name="htop"></a>
# Install htop  
```
sudo apt-get install htop
sudo apt install htop
```


<a name="ipython"></a>
# Install ipython and setup autoreload  
```
sudo apt-get install ipython
```
All the links you have above use commands within ipython. You should try editing your config file. Open up your terminal and complete the following steps.

Step 1: Make sure you have the latest ipython version installed
```python
$ ipython --version
```
Step 2: find out where your config file is
```python
$ ipython profile create
```
Step 3: Open the config file with an editor based on the location of your config file. I use atom. For example:
```python
$ atom ~/.ipython/profile_default/ipython_config.py
```
Step 4: Look for the following lines in the config file:
```python
c.InteractiveShellApp.extensions = []
```
change it to:
```python
c.InteractiveShellApp.extensions = ['autoreload']
```
and then uncomment that line

find:
```python
c.InteractiveShellApp.exec_lines = []
```
change it to:
```python
c.InteractiveShellApp.exec_lines = ['%load_ext autoreload', '%autoreload 2']
```
and then uncomment that line

Done.
