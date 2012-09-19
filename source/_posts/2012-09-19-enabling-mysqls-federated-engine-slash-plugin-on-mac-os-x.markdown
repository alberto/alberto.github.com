---
layout: post
title: "Enabling Mysql's Federated engine/plugin on Mac OS X"
date: 2012-09-19 18:36
comments: true
categories: [mysql, osx]
---

I spent a few hours trying to get the federated engine to work on Mysql, and since I didn't
find any good sources for it, I thought a blog might help someone else.

First, install mysql if you haven't already. I used homebrew.
```
$ brew install mysql
```
The Federated plugin is not installed by default, so you'll have to do it manually. Get into mysql as root (or a user that can alter the mysql.plugin table) and type:
```
mysql> install plugin federated soname 'ha_federated.so';
```
To check if it was installed correctly run:
```
mysql> show plugins;
```

Exit the shell and edit /etc/my.cnf file. If you don't have any, you'll find an example in your mysql installation directory.
```
$ sudo cp $(brew --prefix mysql)/support-files/my-small.cnf /etc/my.cnf
```

Edit the file, and under [mysqld] add a line that contains:
```
federated
```

Restart the mysqld service:
```
mysql.server restart
```

Congrats. You're done!
