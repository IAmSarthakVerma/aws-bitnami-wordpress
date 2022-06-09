# AWS-Bitnami-WordPress

This explains how to setup wordpress on AWS

## Launching Wordpress Instance

* Go to AWS Console. Select ec2 service. Create a new instance. (Check region from above before this).
* Select Marketplace and search "Wordpress". Select first result which will be as " Wordpress Cerftified by Bitnami"
* Click next on all (you can add a tag as "Name" with your preferred value in the tags section).
* You will be asked to create a keypair. Create a new keypair and download the pem file and store it SAFELY. Launch the instance.
* Within a minute or so your instance will be ready and deployed. Note the public ip and test it once.

## Logging In the Instance

* You have to login to your instance via SSH to configure it. To do this start by opening your terminal and run the following command (remember t replace []):

```
ssh -i [path\to\your\key.pem] bitnami@[ipaddress]
```

* Your machine might ask to confirm authenticity. Type "yes" and then your system password (if asked).

* You will now be logged in.

## Getting Default Credentials

* To know the default credentials of your new Wordpress instance login to instance and type in the following command:

```
cat ./bitnami_credentials
```

## Disable Bitnami Banner

* To disable banner (which appears at bottom right), run the following command:

```
sudo /opt/bitnami/apps/wordpress/bnconfig --disable_banner 1
```

## Changing Domain Name

* To change the domain name:

```
sudo nano /opt/bitnami/wordpress/wp-config.php
```

Then change the code from:

```
define('WP_SITEURL', 'http://' . $_SERVER['HTTP_HOST'] . '/');
define('WP_HOME', 'http://' . $_SERVER['HTTP_HOST'] . '/');
```

to 

```
define('WP_SITEURL', 'http://DOMAIN/');
define('WP_HOME', 'http://DOMAIN/');
```

## Installing SSL

DISCLAIMER: Point your domain to the instance before proceeding.

* Run following command:

```
sudo /opt/bitnami/bncert-tool
```

* Type in "yes" if asking for update and run the above cmmanding again.

* Follow the commands as prompted. Choose 
    * HTTP to HTTPS redirect as Y
    * non www to www as Y
    * www to non www as N
    
## Restarting

* To restart your instance, run the following command:

```
sudo /opt/bitnami/ctlscript.sh restart
```
