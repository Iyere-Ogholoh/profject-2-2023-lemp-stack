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

TESTING PHP WITH NGINX

Test to validate that Nginx can correctly hand .php files off to your PHP processor. Do this by creating a test PHP file in your document root.

`sudo nano /var/www/projectLEMP/info.php`

paste code in nano editor

![creating php file in root document](./images/testing-php-with-nginx/paste-code-in-nano-editor.png)

access page on browser followed by /info.php

[accesing page on browser followed by /info.php](http://3.73.130.171/info.php)

![accesing page on browser followed by /info.php](./images/testing-php-with-nginx/accesing-page-followed-by-info.php.png)

remove file created on php server as it contains sensitive information about php environment

`sudo rm /var/www/your_domain/info.php`

RETRIEVING DATA FROM MYSQL DATABASE WITH PHP (CONTINUED)

Connect to mysql console using root account

`sudo mysql -p`

![connecting to mysql console using root account](./images/retrieving-data-from-mysql-database-with-php/connecting-to-mysql-console-using-root-account.png)

Create a new database called example_database by running command below in mysql console

`CREATE DATABASE `example_database`;`

![running command to create database](./images/retrieving-data-from-mysql-database-with-php/running-command-to-create-database.png)

create a new user

`CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';`

![creating a new user](./images/retrieving-data-from-mysql-database-with-php/creating-new-user.png)

grant new user full previledges

`GRANT ALL ON example_database.* TO 'example_user'@'%';`

![granting new user full privilidges](./images/retrieving-data-from-mysql-database-with-php/granting-new-user-full-priviledges.png)

exit mysql console

`exit`

test if new user has proper permissions by logging into MySql console again

`mysql -u example_user -p`

![logging into mysql console with example_user credentials](./images/retrieving-data-from-mysql-database-with-php/logging-into-mysql-console-with-example-user-credentials.png)

confirm that you have access to database as example_user

`SHOW DATABASES;`

![showing access to database as example_user](./images/retrieving-data-from-mysql-database-with-php/showing-access-to-database-as-example_user.png)

create a table named todo_list

`CREATE TABLE example_database.todo_list(item_id INT AUTO_INCREMENT, content VARCHAR(255), PRIMARY KEY(item_id));`

![creating table called todo_list](./images/retrieving-data-from-mysql-database-with-php/creating-table-todo_list.png)

Insert few rows of content in table named todo_list

`INSERT INTO example_database.todo_list (content) VALUES ("My first important item");`

`INSERT INTO example_database.todo_list (content) VALUES ("My second important item");`

`INSERT INTO example_database.todo_list (content) VALUES ("My third important item");`

`INSERT INTO example_database.todo_list (content) VALUES ("My fourth important item");`

`INSERT INTO example_database.todo_list (content) VALUES ("My fifth important item");`

![inserting rows of content into table](./images/retrieving-data-from-mysql-database-with-php/inserting-rows-of-content-into-table.png)

confirm that data inserted was properly saved

`SELECT * FROM example_database.todo_list;`

![confirming data was successfully saved](./images/retrieving-data-from-mysql-database-with-php/confirming-data-was-successfully-saved.png)

`exit`

![exiting mysql console](./images/retrieving-data-from-mysql-database-with-php/exiting-mysql-console.png)

create a PHP script that will connect to MySQL and query for your content

Create a new PHP file in your custom web root directory using your preferred editor

`nano /var/www/projectLEMP/todo_list.php`

Paste the following PHP script connects to the MySQL database and queries for the content of the todo_list table, displays the results in a list

<?php
$user = "example_user";
$password = "password";
$database = "example_database";
$table = "todo_list";

try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>";
  foreach($db->query("SELECT content FROM $table") as $row) {
    echo "<li>" . $row['content'] . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}

![querying content of todo_list](./images/retrieving-data-from-mysql-database-with-php/querying-content-of-todo_list.png)

access webpage by visiting domain name or public IP address configured for the website followed by/todo_list.php

[accessing webpage](http://3.73.130.171/todo_list.php)

![accessing webpage](./images/retrieving-data-from-mysql-database-with-php/accessing-webpage.png)





























