---
layout: post
title: Development environment essentials
---

+ First take an update to upgrade all existing packages in your system.


```bash
sudo apt-get update
```

## Installing Pip

```bash
sudo apt install python-pip
````

## Installing Pipenv

+ While pip can install Python packages, Pipenv is recommended as it’s a higher-level tool that simplifies dependency management for common use cases.


```bash
pip install --user pipenv
```


General development essentials
----
```bash
sudo apt-get install -y build-essential ssh git gitk
```

Databases:
---
You may not need all of these

- none are explicit dependencies of other items in this script.
- SQLite and MySQL are pretty generally used for web development,
- and ODBC is just something we use at work.

```bash
# sqlite for quck access and tesing
sudo apt-get install -y sqlite
# mysql
sudo apt-get install -y python-mysqldb libmysqlclient-dev
```

Python development essentials
----
```bash
sudo apt-get install -y python python-setuptools python-dev && sudo easy_install -U pip
sudo apt-get install -y libxml2-dev libxslt-dev  # needed for Python package 'lxml'
```

[virtualenv](http://docs.python-guide.org/en/latest/dev/virtualenvs/) and [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/)
----
```bash
sudo pip install virtualenv virtualenvwrapper

echo "
if [ -f /usr/local/bin/virtualenvwrapper.sh ] ; then
	. /usr/local/bin/virtualenvwrapper.sh
fi
export WORKON_HOME=~/Envs" >> $HOME/.bashrc

. $HOME/.bashrc

mkdir -p $WORKON_HOME
```
+ Now you should be able to do do: `mkvirtualenv foo`

Use trash-cli([usage](https://pypi.python.org/pypi/trash-cli/))
----
+ git link for [trash-cli](https://github.com/andreafrancia/trash-cli)
```bash
sudo apt-get -y install trash-cli
```

Install java
---
```bash
$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java8-installer

# Check version
$ java -version
java version "1.8.0_151"
Java(TM) SE Runtime Environment (build 1.8.0_151-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)

# Setup environment
$ sudo apt-get install oracle-java8-set-default

# Now add the JAVA_HOME and JRE_HOME environment variable in /etc/environment
$ cat >> /etc/environment <<EOL
JAVA_HOME=/usr/lib/jvm/java-8-oracle
JRE_HOME=/usr/lib/jvm/java-8-oracle/jre
EOL

```
