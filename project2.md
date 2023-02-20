# Project 2
## LEMP stack implementation

Create  a new instance on AWS

![creating an aws instance](./images/installing-nginx/creating-an-ubuntu-instance.png)

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



