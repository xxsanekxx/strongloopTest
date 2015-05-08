#!/usr/bin/env bash

echo "Installing nodejs 0.12.0"
curl -sL https://deb.nodesource.com/setup_0.12 | sudo bash -
sudo apt-get -y install nodejs
sudo echo 'NODE_ENV="development"' >> /etc/environment

echo "Installing global tools"
sudo npm install -g strongloop

echo "Installing mysql"
sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password 963852741'
sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password 963852741'
sudo apt-get install -y mysql-server
sed -i "s/^bind-address/#bind-address/" /etc/mysql/my.cnf
mysql -u root -p963852741 -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '963852741' WITH GRANT OPTION; FLUSH PRIVILEGES;"
sudo echo "[mysqld]" > /etc/mysql/conf.d/utf8_charset.cnf
sudo echo "collation-server = utf8_unicode_ci" >> /etc/mysql/conf.d/utf8_charset.cnf
sudo echo "character-set-server = utf8" >> /etc/mysql/conf.d/utf8_charset.cnf
sudo service mysql restart

echo "Preparing database"
cd /vagrant

echo "Installing project dependencies"
npm install

echo 'cd /vagrant' >> ~/.bashrc
