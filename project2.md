# Project 2
## LEMP stack implementation

Create  a new instance on AWS

![creating an aws instance](./images/installing-nginx/creating-an-ubuntu-instance.png)

INSTALLING NGINX WEB SERVER

`sudo apt update`

![updating servers package index](./images/installing-nginx/updating-servers-package-index.png)

`sudo apt install ngnix`

![installing nginx webserver](./images/installing-nginx/installing-nginx-page1.png)

![installing nginx webserver](./images/installing-nginx/installing-nginx-page2.png)

`sudo apt upgrade`

`sudo systemctl status nginx`

![nginx status](./images/installing-nginx/nginx-status.png)

open inbound connection to port 80

![opening inbound connectio TCP port 80](./images/installing-nginx/opening-TCP-port-80.png)

curl http://localhost:80

![accessing server locally with ubuntu shell](./images/installing-nginx/curl-accessing-server-locally.png)

`curl http://127.0.0.1:80`

![accessing server locally 2](./images/installing-nginx/accessing-server-locally-2.png)

[Testing nginx server response to requests from the internet](http://3.71.15.205/)

`curl -s http://169.254.169.254/latest/meta-data/public-ipv4`

![nginx server url request response](./images/installing-nginx/nginx-server-url-request-response.png)

INSTALLING MYSQL 

`sudo apt install msql-server`

![installing mysql server](./images/installing-mysql/installing-mysql-server-step1.png)

![installing mysql server](./images/installing-mysql/installing-mysql-server-step2.png)

![installing mysql server](./images/installing-mysql/installing-mysql-server-step3.png)

![installing mysql server](./images/installing-mysql/installing-mysql-server-step4.png)

`sudo mysql`

![login in to mysql console](./images/installing-mysql/login-in-to-mysql-console.png)

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

![setting up password for root user](./images/installing-mysql/setting-up-password-for-root-user.png)

run interactive script pre-installed with mysql to remove insecure settings and lockdown access to database

`sudo mysql_secure_installation`

![mysql installation interactive script](./images/installing-mysql/running-interactive-script-for-mysql-installation.png)

test login in into mysql console

`sudo mysql -p`

![testing login into mysql console](./images/installing-mysql/testing-login-into-mysql-console.png)

exit mysql console with command "exit"

![exiting mysql console](./images/installing-mysql/exiting-mysql-console.png)


INSTALLING PHP to process code and generate dynamic content for the webserver

`sudo apt install php-fpm php-msql`

![installing php-pfm and php-mysql](./images/installing-php/installing-php.png)


CONFIGURING NGINX TO USE PHP PROCESSOR

create root web directory for your domain as follows

`sudo mkdir /var/www/projectLEMP`

![creationg root web directory for your domain](./images/configuring-nginx-to-use-php-processor/creating-root-web-directory-for-your-domain.png)

assign ownership of the directory with the $USER environment table

`sudo chown -R $USER:$USER /var/www/projectLEMP`

![changing ownership of directory](./images/configuring-nginx-to-use-php-processor/changing-ownership-of-directory.png)

open configuration file in nginx sites-available using command line editor (NANO)

![pasting barebones configuration using nano editor](./images/configuring-nginx-to-use-php-processor/pasting-barebones-configuration.png)

Activate your configuration by linking to the config file from Nginx’s sites-enabled directory

`sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`

![activating configuration file](./images/configuring-nginx-to-use-php-processor/activating-cofiguration-file.png)

test configuration for syntax errors

`sudo nginx -t`

![testing configuratiob for syntax errors](./images/configuring-nginx-to-use-php-processor/testing-configuration-for-syntax-errors.png)

disable default nginx host currently configured to listen on port 80

`sudo unlink /etc/nginx/sites-enabled/default`

![disable nginx host](./images/configuring-nginx-to-use-php-processor/disable-nginx-host.png)

reload nginx

`sudo systemctl reload nginx`

![reloading nginx](./images/configuring-nginx-to-use-php-processor/reloading-nginx.png)

test new server block by  creating an index.html file in location /var/www/projectLEMP

`sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html`

![testing new server block](./images/configuring-nginx-to-use-php-processor/testing-new-server-block.png)

open url in browser

![opening url in browser](./images/configuring-nginx-to-use-php-processor/opening-url-in-browser.png)

accessing website with public DNS name

![accessing site with public dns name](./images/configuring-nginx-to-use-php-processor/accessing-site-with-public-dns-name.png)

























