[readme.md](https://github.com/user-attachments/files/26470035/readme.md)# Домашнее задание к занятию "`Название занятия`" - `Фамилия и имя студента`



---

### Задание 1

![photo_5361781999636519544_y](https://github.com/user-attachments/assets/72d2007f-0739-4927-b0e0-8fadcc8c3dec)

# wget https://repo.zabbix.com/zabbix/7.4/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.4+ubuntu24.04_all.deb
# dpkg -i zabbix-release_latest_7.4+ubuntu24.04_all.deb
# apt update
# apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
d. Create initial database
Documentation
Make sure you have database server up and running.

Run the following on your database host.

# sudo -u postgres createuser --pwprompt zabbix
# sudo -u postgres createdb -O zabbix zabbix
On Zabbix server host import initial schema and data. You will be prompted to enter your newly created password.

# zcat /usr/share/zabbix/sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
e. Configure the database for Zabbix server
Edit file /etc/zabbix/zabbix_server.conf

DBPassword=password
f. Start Zabbix server and agent processes
Start Zabbix server and agent processes and make it start at system boot.

# systemctl restart zabbix-server zabbix-agent apache2
# systemctl enable zabbix-server zabbix-agent apache2

---

### Задание 2
![photo_5361781999636519577_y](https://github.com/user-attachments/assets/4c0233de-bbb5-4f82-8b98-6dbc2fb5c0dd)
![photo_5361781999636519581_y](https://github.com/user-attachments/assets/865a12f9-593e-4ecd-a25d-3b5d97d9a901)
![photo_5361781999636519585_y](https://github.com/user-attachments/assets/03a14720-7e37-4783-a502-531338167f65)

wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest+ubuntu22.04_all.deb
sudo dpkg -i zabbix-release_latest+ubuntu22.04_all.deb
sudo apt update
sudo apt install -y zabbix-agent
sudo nano /etc/zabbix/zabbix_agentd.conf
sudo systemctl restart zabbix-agent
sudo systemctl enable zabbix-agent




