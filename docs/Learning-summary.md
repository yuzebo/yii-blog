#Learning-summary
**Using Ubuntu14.04 system**
#First of all,let us know what is apt-get.

Advanced Package Tool, also known as apt-get, is one for Unix and Linux systems application manager.For retrieving the application and load it into Debian Linux system.In its ability to resolve outstanding software dependencies One of the reasons Apt-get fame.

##apt Command Usage
```bash
apt-get update
```
Run this command after changing /etc/apt/sources.list or / etc / apt / preferences. In addition, you need to periodically run this command to make sure your package list is up to date.
```bash
apt-get install packagename
```
Install a new package (see below aptitude)
```bash
apt-get remove packagename
```
Uninstalling an installed package (reservations configuration documentation)
```bash
apt-get remove --purge packagename
```
Uninstall package (delete the configuration file) installed a
```bash
apt-get autoremove packagename
```
Remove packages and their dependent packages
```bash
apt-get autoremove --purge packagname
```
Remove packages and their dependencies package + profile, than to remove it completely above
```bash
apt-get autoclean
```
apt would have been loaded or unloaded backup software on the hard drive, so if space is needed, then, to allow the command to delete the uninstall software you have a backup.
```bash
apt-get clean
```
This command will install the backup software also deleted, but this does not affect the use of the software.
```bash
apt-get upgrade
```
You can use this command to update the package, apt-get upgrade can not only update packages from the release of the same version number, you can also update packages from the new version of the release.

#Installation and Configuration Nginx
##1.install Nginx.
```bash
$ sudo apt-get install update
$ sudo apt-get install nginx
```
##2.test Nginx.
View the machine IP address
```bash
ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
```
use a web browser then write 
```bash
http://127.0.0.1 or http:// local ip
```
to check that Nginx is working.

##3.install php.
```bash
$ sudo apt-get install php5-fpm
```

##4.Configure PHP, modify the php.ini file.

####Backup php.ini file.
```bash
$ cp /etc/php5/fpm/php.ini /etc/php5/fpm/php.ini.back
```
####Cancel that have security implications pathinfo mode.
```bash
$ vim /etc/php5/fpm/php.ini
```
The (cgi.fix_pathinfo = 1) is set to (cgi.fix_pathinfo = 0).
```bash
$  start up php-fpm
$  sudo service php5-fpm restart
```
##5.Nginx configuration process allowed to use php-fpm

####Backup / etc / nginx / sites-available / default file
```bash
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default.back
```
Modify the default document reads as follows
```bash
server {

    listen 80 default_server;
    listen [::]:80 default_server ipv6only=on;

    root /usr/share/nginx/html;
    index index.php index.html index.htm;

    server_name server_domain_name_or_IP;

    location / {
        try_files $uri $uri/ =404;
    }

    error_page 404 /404.html;
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }	
    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```
##7.Restart nginx server
```bash
$ sudo service nginx restart
```
##8.Download yii1.1 tar.gz
https://github.com/yiisoft/yii/releases/download/1.1.17/yii-1.1.17.467ff50.tar.gz

##9.Unzip yii to specify the root directory
```bash
$ sudo tar -zxvf yii-1.1.17.467ff50.tar.gz -C /usr/share/nginx/html
```
The release of the Yii version depends on the version you downloaded.
Change file name to yii
```bash
$ sudo mv yii-1.1.17.467ff50 yii
```

##10.Create the application skeleton
```bash
  /usr/share/nginx/html/yii/framework/yiic webapp /usr/share/nginx/html/blog
```
Create a Web application under '/wwwroot/blog'? [Yes|No]y

##11.Check your blog application is working
```bash
127.0.0.1/yii/blog/index.php
```

**Now you can start a blog site by Yii.**

##Successfully Accomplished next step is use github

##1.First, create a ssh key locally
```bash
$ ssh-keygen -t rsa -C "your_email@youremail.com"
```
##2.To verify successful
```bash
$ ssh -T git@github.com
```
Terminal Display:Hi yuzebo! You've successfully authenticated, but GitHub does not provide shell access.

##3.Next we need to do is to spread github up local warehouse, before also need to set the username and email
```bash
$ git config --global user.name "your name"
$ git config --global user.email "your_email@youremail.com"
```	
##4.Add the remote address
```bash 
$ git remote add origin git@github.com:yourName/yourRepo.git
$ check origin URL
$ git remote -v 
```
##5.git init in your project
```bash
$ git add (filename)
$ git commit -m 'message'
$ git push -f origin develop
```



