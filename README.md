# LAMP_UbuntuSERVER_20_04-Installation-Guide
# How to install Apache MariaDB php and phpmyadmin Server on Ubutu Server 20.04LTS

## By Tawan Phurat 15 June 2020

## Step0 Pre Installation

### Install Ubuntu 20.04 without any bundle package.

### Step1: Update Repository

```
 sudo apt-get update
```

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

### Step12: Install php

```
sudo apt-get install php libapache2-mod-php php-mysql
```

### Step13: check path of php

```
sudo apt-cache search php | grep php-	#show all php packages
```

### Step14: Install other module from Redis

```
sudo apt install php-redis php-zip
```

### Step15: Restart apache2

```
sudo systemctl restart apache2
```

### Step16: create info.php file

```
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
```

### Step17: test php on web

```
http://192.168.1.106/info.php      # replace 192.168.1.106 with your ip address
```

#### Step18: Install phpmyadmin

```
sudo apt-get install phpmyadmin

#For web-server question, select Apache2
#For dbconfig-common question, select yes
#Type password for root 2 times
```

### Step19: config phpmyadmin system

```
sudo a2enconf phpmyadmin.conf  

sudo systemctl reload apache2.service  
```

### Step20: config password for phpmyadmin

```
sudo mysql -u root

SELECT user,plugin,host FROM mysql.user WHERE user = 'root';
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('MyNewPass'); 
FLUSH PRIVILEGES;  
exit
```

### Step21: Login to phpmyadmin

```
http://192.168.1.106/phpmyadmin  # replace 192.168.1.106 with your ip address
```


### NAT access Internet via enp5s0  from enp9s0  

```
iptables --table nat --append POSTROUTING --out-interface enp5s0 -j MASQUERADE
iptables --append FORWARD --in-interface enp9s0 -j ACCEPT
```
