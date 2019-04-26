
## Ubuntu 16-04
```Unix
$ sudo -s
$ apt update
$ apt upgrade
$ wget https://www.apachefriends.org/xampp-files/7.1.10/xampp-linux-x64-7.1.10-0-installer.run
$ chmod +x xampp-linux-x64-7.1.10-0-installer.run
$ ./xampp-linux-x64-7.1.10-0-installer.run
```
## Command Control
```Unix
$ /opt/lampp/xampp start
$ /opt/lampp/xampp stop
$ /opt/lampp/xampp restart
$ /opt/lampp/xampp --help
$ /opt/lampp/uninstall
```

# How to config phpmyadmin
## Step 1 : config -  config.inc.php
### 1.1 Goto file path
```Unix
$ cd /opt/lampp/phpmyadmin/config.inc.php
```

### 1.2 Chang Config
```Unix
$cfg['Servers'][$i]['auth_type'] = 'cookie';
$cfg['Servers'][$i]['user'] = 'root';
$cfg['Servers'][$i]['password'] = '';
$cfg['Servers'][$i]['extension'] = 'mysqli';
$cfg['Servers'][$i]['AllowNoPassword'] = false;
```

## Step 2 : config - httpd-xampp.conf
### 2.1 Goto file path
```Unix
$ cd /opt/lampp/etc/extra/httpd-xampp.conf
```

### 2.2 Chang Config
```Unix
<Directory "/opt/lampp/phpmyadmin">
    AllowOverride AuthConfig Limit
   # Require local
    Order allow,deny
    Allow from all
    Require all granted
    ErrorDocument 403 /error/XAMPP_FORBIDDEN.html.var
</Directory>

```


Link Reference: https://linoxide.com/ubuntu-how-to/install-xampp-stack-ubuntu-16-04-terminal/
