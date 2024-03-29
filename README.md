# LAMP_UbuntuSERVER_20_04-Installation-Guide Part I

# How to install Apache MariaDB php and phpmyadmin Server on Ubutu Server 20.04LTS 

## By Tawan Phurat 15 June 2020

## Step0 Pre Installation

### Install Ubuntu 20.04 without any bundle package.

### Step1: Update Repository

```
 sudo apt-get update
```

### Step1.1: install net-tools (for ifconfig command)

```
sudo  apt-get install net-tools
```` 

### Step2: Install Apache2

```
sudo apt-get install apache2
```

### Step3: Check Status

```
sudo systemctl status apache2
```

### Step4: Make it automatically start at boot

```
sudo systemctl is-enabled apache2
```

### Step5: check web-server at chrome browser

```
http://192.168.1.106                # replace 192.168.1.106 with your ip address
```

### Step6: Install MariaDB

```
sudo apt install mariadb-server mariadb-client
```

### Step7: Check status

```
sudo systemctl status mariadb
```

### Step8: Make it automatically start at boot

```
sudo systemctl is-enabled mariadb
```

### Step9: Make it Secure

```
sudo mysql_secure_installation

"Enter current password for root (enter for none):" Enter
"Set a root password? [Y/n]" y
"Remove anonymous users? [Y/n]" y
"Disallow root login remotely? [Y/n]" y
"Remove test database and access to it? [Y/n]" y
"Reload privilege tables now? [Y/n]" y
```

### Step10: Test security (Prevent root access from local console. Don't worry about error in this step. It's OK)

```
mysql -u root -p
```

### Step11: Test security (Enable root access by su command and specify Password)

```
sudo mysql -u root
```

### Step12: config database lissen on any address



### Step13: Install php

```
sudo apt-get install php libapache2-mod-php php-mysql
```

### Step14: check path of php

```
sudo apt-cache search php | grep php-	#show all php packages
```

### Step15: Install other module from Redis

```
sudo apt install php-redis php-zip
```

### Step16: Restart apache2

```
sudo systemctl restart apache2
```

### Step17: create info.php file

```
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
```

### Step18: test php on web

```
http://192.168.1.106/info.php      # replace 192.168.1.106 with your ip address
```

#### Step19: Install phpmyadmin

```
sudo apt-get install phpmyadmin

#For web-server question, select Apache2
#For dbconfig-common question, select yes
#Type password for root 2 times
```

### Step20: config phpmyadmin system

```
sudo a2enconf phpmyadmin.conf  

sudo systemctl reload apache2.service  
```

### Step21: config password for phpmyadmin

```
sudo mysql -u root

SELECT user,plugin,host FROM mysql.user WHERE user = 'root';
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('MyNewPass'); 
FLUSH PRIVILEGES;  
exit
```

### Step22: Login to phpmyadmin

```
http://192.168.1.106/phpmyadmin  # replace 192.168.1.106 with your ip address
```


### NAT access Internet via enp0s3(Virtualbox NAT)  from enp0s8(Virtualbox Bridge)   

```
iptables --table nat --append POSTROUTING --out-interface enp0s3 -j MASQUERADE
iptables --append FORWARD --in-interface enp0s8 -j ACCEPT
```

edit firwall rule 
```
sudo nano /etc/sysctl.conf
```
uncomment the line 
```
net.ipv4.ip_forward=1
```

### install webmin

```
sudo nano /etc/apt/sources.list
```

add this line 
```
deb http://download.webmin.com/download/repository sarge contrib
```

download the Webmin PGP key
```
wget -q -O- http://www.webmin.com/jcameron-key.asc | sudo apt-key add
```

```
sudo apt update
sudo apt install webmin
```

### config webmin for mariadb

```
bind 0.0.0.0
```

#### goto webmin --> Unused Moduled --> MySQL Database Server  --> module config --> System configuration

change MySQL configuration file	from   '/etc/mysql/mysql.cnf' to '/etc/mysql/mariadb.cnf'

#### enter root password  for mariadb 

save and refresh unused module




### install MQTT server
coming soon!
Bl0I786LtxJTxGjUkiFOr3XbiuMCxwwFI4QHPn6ZQzU
