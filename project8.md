##  **PROJECT 8 - LOAD BALANCER SOLUTION WITH APACHE**

## STEP 1 – APACHE CONFIGURATION AS A LOAD BALANCER


### Creation of an ubuntu server, named Project-8-apache-lb in addition to nfs, web1 and web2 servers created earlier

![instances1](./images/instances1.PNG)

### Opening TCP port 80 on Project-8-apache-lb by creating an Inbound Rule in Security Group

## STEP 2 – APACHE LOAD BALANCER INSTALLATION ON LOAD BALANCER SERVER AND CONFIGURATION POINTING TRAFFIC FROM LB TO WEB SERVERS 1 AND 2

### Installation of apache2

`sudo apt update`

`sudo apt install apache2 -y`

`sudo apt-get install libxml2-dev`

![lb-sudo-update](./images/lb-sudo-update.PNG)

![lb-apache-installation](./images/lb-apache-installation.PNG)

![lb-apache-installation1](./images/lb-apache-installation1.PNG)

![lb-dependency](./images/lb-dependency.PNG)

![lb-dependency1](./images/lb-dependency1.PNG)

### Modules enabling

`sudo a2enmod rewrite`

`sudo a2enmod proxy`

`sudo a2enmod proxy_balancer`

`sudo a2enmod proxy_http`

`sudo a2enmod headers`

`sudo a2enmod lbmethod_bytraffic`

![lb-enabling](./images/lb-enabling.PNG)

### Activating the new configurations above by restarting apache servvices

`sudo systemctl restart apache2`

`sudo systemctl status apache2`

![lb-restart-apache](./images/lb-restart-apache.pNG)

![lb-apache-status](./images/lb-apache-status.PNG)

## STEP 2 – CONFIGURATION OF LOAD BALANCING

### Load balancer configuration

`sudo vi /etc/apache2/sites-available/000-default.conf`

![load-balancing-configuration](./images/load-balancing-configuration.pNG)

### Restarting apache server after load bbalancing configuration

`sudo systemctl restart apache2`

`sudo systemctl status apache2`

![lb-apache-status](./images/lb-apache-status.pNG)

### Verifying successfulness of the configuration

[TOOLING WEBPAGE](https://52.87.15.63/index.php)

![lb-adminpage](./images/lb-adminpage.pNG)

![lb-tooling-page](./images/lb-tooling-page.pNG)

### Unmounting /var/log/httpd/ from web servers 1 and 2 to have their own log directory

`sudo tail -f /var/log/httpd/access_log`

![web1-lb-display](./images/web1-lb-display.pNG)

![web2-lb-display](./images/web2-lb-display.pNG)

### Local DNS names resolution

`sudo vi /etc/hosts`

![lblocaldns-resolution](./images/lblocaldns-resolution.pNG)

### Curl web 1 and 2 from lb server

`curl http://Web1`

`curl http://Web2`

![curl-web1-fromlb](./images/curl-web1-fromlb.pNG)

![curl-web2-fromlb](./images/curl-web2-fromlb.pNG)



