[readme.md](https://github.com/user-attachments/files/26470035/readme.md)# Домашнее задание к занятию "`Название занятия`" - `Фамилия и имя студента`



---

### Задание 1
a. Установите репозиторий Zabbix
# wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_6.0+debian11_all.deb
# dpkg -i zabbix-release_latest_6.0+debian11_all.deb
# apt update
b. Установите Zabbix сервер, веб-интерфейс и агент
# apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
c. Создайте базу данных
Документация
Установите и запустите сервер базы данных.

Выполните следующие комманды на хосте, где будет распологаться база данных.

# mysql -uroot -p
password
mysql> create database zabbix character set utf8mb4 collate utf8mb4_bin;
mysql> create user zabbix@localhost identified by 'password';
mysql> grant all privileges on zabbix.* to zabbix@localhost;
mysql> set global log_bin_trust_function_creators = 1;
mysql> quit;
На хосте Zabbix сервера импортируйте начальную схему и данные. Вам будет предложено ввести недавно созданный пароль.

# zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix
Выключите опцию log_bin_trust_function_creators после импорта схемы базы данных.

# mysql -uroot -p
password
mysql> set global log_bin_trust_function_creators = 0;
mysql> quit;
d. Настройте базу данных для Zabbix сервера
Отредактируйте файл /etc/zabbix/zabbix_server.conf

DBPassword=password
e. Запустите процессы Zabbix сервера и агента
Запустите процессы Zabbix сервера и агента и настройте их запуск при загрузке ОС.

# systemctl restart zabbix-server zabbix-agent apache2
# systemctl enable zabbix-server zabbix-agent apache2
![photo_5361781999636519544_y](https://github.com/user-attachments/assets/72d2007f-0739-4927-b0e0-8fadcc8c3dec)


### Задание 2
wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest+ubuntu22.04_all.deb
sudo dpkg -i zabbix-release_latest+ubuntu22.04_all.deb
sudo apt update
sudo apt install -y zabbix-agent
sudo nano /etc/zabbix/zabbix_agentd.conf
sudo systemctl restart zabbix-agent
sudo systemctl enable zabbix-agent
![photo_5361781999636519577_y](https://github.com/user-attachments/assets/4c0233de-bbb5-4f82-8b98-6dbc2fb5c0dd)
![photo_5361781999636519581_y](https://github.com/user-attachments/assets/865a12f9-593e-4ecd-a25d-3b5d97d9a901)
![photo_5361781999636519585_y](https://github.com/user-attachments/assets/03a14720-7e37-4783-a502-531338167f65)





