#Learning-summary
##1.install Nginx.
```bash
$ sudo apt-get install update
$ sudo apt-get install nginx
```
##2.test Nginx.
*  point it to (127.0.0.1) to check that Nginx is working.

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

##7.Restart nginx server
```bash
$ sudo service nginx restart
```
##8.Download yii1.1 tar.gz
  http://www.yiichina.com/download

##9.Unzip yii to specify the root directory
  tar -zxvf yii.tar.gz -C /usr/share/nginx/html

##10.Create the application skeleton
  % /wwwroot/yii/framework/yiic webapp /wwwroot/blog
Create a Web application under '/wwwroot/blog'? [Yes|No]y


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


