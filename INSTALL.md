# General update and upgrade #
```
sudo apt update
sudo apt upgrade
```

# Install Apache #
```
sudo apt install apache2
sudo a2enmod rewrite
sudo a2enmod actions
sudo systemctl restart apache2
```

# Install PHP 7.3 #
```
sudo apt install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt install php7.3
sudo apt install php7.3-common php7.3-mysql php7.3-xml php7.3-xmlrpc php7.3-curl php7.3-gd php7.3-imagick php7.3-cli php7.3-dev php7.3-imap php7.3-mbstring php7.3-opcache php7.3-soap php7.3-zip php7.3-intl
```

# Install composer #
```
sudo apt install curl php-cli php-mbstring git unzip
cd ~
curl -sS https://getcomposer.org/installer -o composer-setup.php
HASH=(Current HASH from https://composer.github.io/pubkeys.html)
php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
rm composer-setup.php
```

# Install mysql server #
```
wget http://repo.mysql.com/mysql-apt-config_0.8.10-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.10-1_all.deb
#### 1. Select "MySQL Server & Cluster (Currently selected: mysql-8.0)"
#### 2. mysql-5.7
#### 3. MySQL Server & Cluster (Currently selected: mysql-5.7)
#### 4. OK
sudo apt update
sudo apt install mysql-server
sudo mysql_secure_installation
#### NO [RETURN]
#### root [RETURN]
#### root [RETURN]
#### y [RETURN]
#### y [RETURN]
#### y [RETURN]
#### y [RETURN]
sudo mysql
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
rm mysql-apt-config_0.8.10-1_all.deb
```

# Create base vhost dir #
```
sudo mkdir /var/www/vhosts
sudo chown vagrant:www-data /var/www/vhosts -R
```

# Install bash it #
```
cd ~
git clone --depth=1 https://github.com/Bash-it/bash-it.git ~/.bash_it
~/.bash_it/install.sh
y [RETURN]
source /home/vagrant/.bashrc
```

# Install git autocomplete #
```
sudo apt-get install git bash-completion
```

# Install php cs fixer #
```
cd ~
wget https://cs.symfony.com/download/php-cs-fixer-v2.phar -O php-cs-fixer
sudo chmod a+x php-cs-fixer
sudo mv php-cs-fixer /usr/local/bin/php-cs-fixer
```

# Install PhpMyAdmin #
```
sudo apt install phpmyadmin php-mbstring php-gettext
#### [*] Apache [RETURN]
#### Yes  [RETURN]
#### Enter some password [RETURN]
#### Repeat some password [RETURN]
sudo vim /etc/apache2/apache2.conf
#### Add this line to the end of the file
Include /etc/phpmyadmin/apache.conf
sudo systemctl restart apache2
```

# History autocompletion #
`vim ~/.inputrc`
#### Paste in the following
```
"\e[A": history-search-backward
"\e[B": history-search-forward
set show-all-if-ambiguous on
set completion-ignore-case on
```
Reconnect SSH

#### Connect via sftp IP and user vagrant password vagrant ####