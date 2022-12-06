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

# Add PHP Repository #
```
sudo apt install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt update
```

# Install PHP 8.1 #
```
sudo apt -y install php8.1
sudo apt install php8.1-common php8.1-mysql php8.1-xml php8.1-xmlrpc php8.1-curl php8.1-gd php8.1-imagick php8.1-cli php8.1-dev php8.1-imap php8.1-mbstring php8.1-opcache php8.1-soap php8.1-zip php8.1-intl
```

# Install PHP 8.0 #
```
sudo apt -y install php8.0
sudo apt install php8.0-common php8.0-mysql php8.0-xml php8.0-xmlrpc php8.0-curl php8.0-gd php8.0-imagick php8.0-cli php8.0-dev php8.0-imap php8.0-mbstring php8.0-opcache php8.0-soap php8.0-zip php8.0-intl
```

# Install PHP 7.4 #
```
sudo apt -y install php7.4
sudo apt install php7.4-common php7.4-mysql php7.4-xml php7.4-xmlrpc php7.4-curl php7.4-gd php7.4-imagick php7.4-cli php7.4-dev php7.4-imap php7.4-mbstring php7.4-opcache php7.4-soap php7.4-zip php7.4-intl
```

# Install PHP 7.3 #
```
sudo apt install php7.3
sudo apt install php7.3-common php7.3-mysql php7.3-xml php7.3-xmlrpc php7.3-curl php7.3-gd php7.3-imagick php7.3-cli php7.3-dev php7.3-imap php7.3-mbstring php7.3-opcache php7.3-soap php7.3-zip php7.3-intl
```

# Install PHP 7.2 #
```
sudo apt install php7.2
sudo apt install php7.2-common php7.2-mysql php7.2-xml php7.2-xmlrpc php7.2-curl php7.2-gd php7.2-imagick php7.2-cli php7.2-dev php7.2-imap php7.2-mbstring php7.2-opcache php7.2-soap php7.2-zip php7.2-intl
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
sudo mysql
sudo apt install mysql-server
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
mysql> exit
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
mysql> exit
rm mysql-apt-config_0.8.10-1_all.deb
```

# Update mysql my.cnf to remove sql_mode ONLY_FULL_GROUP_BY #
```
sudo vim /etc/mysql/my.cnf
```
Add this to the file
```
[mysqld]
sql_mode = "STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"
```


# Create base vhost dir #
```
sudo mkdir /var/www/vhosts
sudo chown vagrant:www-data /var/www/vhosts -R
```

# Activate SSL and HTTPS (Port 443) #
```
sudo a2enmod ssl
```
Create self signed key (replace domain.tld with your local domain)
```
cd /root/
mkdir ssl
cd ssl
openssl genrsa -out domain.tld.test.key 1024
openssl req -new -key domain.tld.test.key -out domain.tld.test.csr
openssl req -noout -text -in domain.tld.test.csr
openssl x509 -req -days 365 -in domain.tld.test.csr -signkey domain.tld.test.key -out domain.tld.test.crt
```

Edit vhost conf and add new vhost for port 443
```
<VirtualHost *:443>
        SSLEngine on
        SSLCertificateFile /root/ssl/domain.tld.test.crt
        SSLCertificateKeyFile /root/ssl/domain.tld.test.key
        ServerName domain.tld.test
        ServerAlias www.domain.tld.test
        DocumentRoot /var/www/vhosts/domain.tld.test/public
        ErrorLog ${APACHE_LOG_DIR}/domain.tld.test_error.log
        CustomLog ${APACHE_LOG_DIR}/domain.tld.test_access.log combined
        <Directory /var/www/vhosts/domain.tld.test>
                Options FollowSymLinks
                AllowOverride All
        </Directory>
</VirtualHost>
```

```
sudo service apache2 restart
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
# Install Imagick #
`sudo apt install php-imagick`

# Install GraphicsMagick #
`sudo apt install graphicsmagick`

# Install ghostscript #
`sudo apt install ghostscript`

# Install Sendmail #
`sudo apt install sendmail`

# Install Mailhog #
```
wget https://github.com/mailhog/MailHog/releases/download/v1.0.0/MailHog_linux_amd64
sudo cp MailHog_linux_amd64 /usr/local/bin/mailhog
sudo chmod +x /usr/local/bin/mailhog
```
```
sudo tee /etc/systemd/system/mailhog.service <<EOL
[Unit]
Description=Mailhog
After=network.target
[Service]
User=vagrant
ExecStart=/usr/bin/env /usr/local/bin/mailhog > /dev/null 2>&1 &
[Install]
WantedBy=multi-user.target
EOL
```
```
systemctl daemon-reload
#### Password: vagrant [RETURN]
systemctl enable mailhog
#### Password: vagrant [RETURN]
#### Mailhog is running on port 8025
```

# Install mhsendmail #
```
cd ~
sudo apt-get install golang-go
mkdir gocode
echo "export GOPATH=$HOME/gocode" >> ~/.profile
source ~/.profile
go get github.com/mailhog/mhsendmail
sudo cp gocode/bin/mhsendmail /usr/local/bin/mhsendmail
sudo sed -i "s/;sendmail_path.*/sendmail_path='\/usr\/local\/bin\/mhsendmail'/" /etc/php/7.2/apache2/php.ini
sudo sed -i "s/;sendmail_path.*/sendmail_path='\/usr\/local\/bin\/mhsendmail'/" /etc/php/7.3/apache2/php.ini
sudo sed -i "s/;sendmail_path.*/sendmail_path='\/usr\/local\/bin\/mhsendmail'/" /etc/php/7.4/apache2/php.ini
sudo service apache2 restart
```

# Add .gitignore and .gitconfig files to home dir #
Copy the content or the files from this repository to your vagrant home dir (`/~`).

# Add global git username and email #
```
git config --global user.name "FIRST_NAME LAST_NAME"
git config --global user.email "mail@example.com"
```

# Enable bash-it git alias #
`bash-it enable alias git`

# History autocompletion #
`vim ~/.inputrc`

#### Paste in the following
```
"\e[1~": beginning-of-line
"\e[4~": end-of-line
"\e[A": history-search-backward
"\e[B": history-search-forward
set show-all-if-ambiguous on
set completion-ignore-case on
```

Bind edited .inputrc
```
bind -f ~/.inputrc
```

# Change apache default user and group
```
sudo vi /etc/apache2/envvars
```
Search for following lines and change both to `vagrant`
```
export APACHE_RUN_USER=vagrant
export APACHE_RUN_GROUP=vagrant
```

# xdebug
Install xdebug
`sudo apt-get install php-xdebug`

Add php module
`sudo vim /etc/php/7.4/mods-available/xdebug.ini`

Paste in the following code
```
zend_extension=/usr/lib/php/20190902/xdebug.so
xdebug.mode=debug
xdebug.start_with_request=yes
xdebug.idekey=netbeans-xdebug
xdebug.client_host=YOUR_MACHINE_IP
xdebug.client_port=9003
xdebug.remote_handler=dbgp
xdebug.discover_client_host=1
```

Create symlinks to activate the modules
`sudo ln -s /etc/php/7.4/mods-available/xdebug.ini /etc/php/7.4/apache2/conf.d/20-xdebug.ini`
`sudo ln -s /etc/php/7.4/mods-available/xdebug.ini /etc/php/7.4/cli/conf.d/20-xdebug.ini`

Restart apache
`sudo service apache2 restart`

#### Connect via sftp IP and user vagrant password vagrant ####
