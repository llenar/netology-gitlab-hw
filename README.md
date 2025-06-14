# Решение 1

![alt text](https://github.com/llenar/netology-gitlab-hw/blob/main/Scr1-1.png)

``` bash
ssh -l admin 84.252.132.202
sudo apt update
sudo apt install postgresql
sudo wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb
sudo dpkg -i zabbix-release_6.4-1+debian11_all.deb
sudo apt update
sudo apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts
sudo su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'13579\'';"'
sudo su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'
sudo zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
sudo sed -i 's/# DBPassword=/DBPassword=13579/g' /etc/zabbix/zabbix_server.conf
sudo systemctl restart zabbix-server apache2
sudo systemctl enable zabbix-server apache2

```
