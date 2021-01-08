---
title: 'Set up a local roll server for rocks-7.0'
subtitle: 'Set up a local roll server for rocks-7.0'
summary: Set up a local roll server for rocks-7.0
authors:
- admin
tags:
- Gnu/Linux
- Rocks
- HPC
categories:
- scripts
date: "2019-04-28T00:00:00Z"
lastmod: "2019-04-28T00:00:00Z"
featured: false
draft: false
---
At the very beginning of installation of rocks-7.0, we must define a roll server. It's recommended to set up a local server to facilitate roll addition. There are some scripts to make this easy for non experts [here](https://github.com/rocksclusters/roll-server). After doing steps 0, I and II, change your site configuration file (e.g /etc/apache2/sites-enabled/000-default.conf in ubuntu or mint) to be like this:

```bash
## Definitions for rocks-7-0.my.org (change according to your one)
###
<VirtualHost *:80>
ServerName rocks-7-0.my.org
</VirtualHost>

# allow all access to the rolls RPMS
<Directory /var/www/html/rocks/7.0/install/rolls>
        AddHandler cgi-script .cgi
        Options FollowSymLinks Indexes ExecCGI
        DirectoryIndex /rocks/7.0/install/rolls/index.cgi
        Allow from all
</Directory>
```

Then do

```bash
sudo a2enmod cgi
```

and finally

```bash
sudo systemctl restart apache2.service
```