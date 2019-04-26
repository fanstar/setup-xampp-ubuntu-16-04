# Step1 Setup XAMPP
# Ubuntu 16-04
```Unix
$ sudo -s
$ apt update
$ apt upgrade
$ wget https://www.apachefriends.org/xampp-files/7.1.10/xampp-linux-x64-7.1.10-0-installer.run
$ chmod +x xampp-linux-x64-7.1.10-0-installer.run
$ ./xampp-linux-x64-7.1.10-0-installer.run
$ /opt/lampp/xampp start
```
## Command Control
```Unix
$ /opt/lampp/xampp start
$ /opt/lampp/xampp stop
$ /opt/lampp/xampp restart
$ /opt/lampp/xampp --help
$ /opt/lampp/uninstall
```

# step2 Create DB Admin from phpmyadmin
## Goto phpmyadmin link lie below 
```Unix
https://xx.xx.xx.xx/phpmyadmin/
```
# Fix Error
Access forbidden!
New XAMPP security concept:

Access to the requested object is only available from the local network.

This setting can be configured in the file "httpd-xampp.conf".

## config - httpd-xampp.conf
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
### 2.3 restart xampp
```Unix
$ /opt/lampp/xampp restart
```
# step3 create root DB from php addmin
```Unix
Select "User Account" --> "Change password" for "root" - "localhost"
Then will get an error
MySQL said: Documentation
#1045 - Access denied for user 'root'@'localhost' (using password: NO)
 
Fix error from below - config.inc.php
```

# step3 config phpmyadmin
## config -  config.inc.php
### 3.1 Goto file path
```Unix
$ cd /opt/lampp/phpmyadmin/config.inc.php
```

### 3.2 Chang Config
```Unix
$cfg['Servers'][$i]['auth_type'] = 'cookie';
$cfg['Servers'][$i]['user'] = 'root';
$cfg['Servers'][$i]['password'] = '';
$cfg['Servers'][$i]['extension'] = 'mysqli';
$cfg['Servers'][$i]['AllowNoPassword'] = false;
```
### 3.3 restart xampp
```Unix
$ /opt/lampp/xampp restart
```

Link Reference: https://linoxide.com/ubuntu-how-to/install-xampp-stack-ubuntu-16-04-terminal/
