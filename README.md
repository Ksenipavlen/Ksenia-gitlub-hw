# Домашнее задание к занятию "`Zabbix`"
**Ксения Павленко**

---

## Задание 1

### a. Установка репозитория Zabbix

```bash
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_6.0+debian11_all.deb
dpkg -i zabbix-release_latest_6.0+debian11_all.deb
apt update
```

---

### b. Установка Zabbix Server, Web-интерфейса и агента

```bash
apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```

---

### c. Создание базы данных

Установите и запустите сервер базы данных.

```bash
mysql -uroot -p
```

```sql
CREATE DATABASE zabbix CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;
CREATE USER 'zabbix'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'localhost';
SET GLOBAL log_bin_trust_function_creators = 1;
QUIT;
```

Импорт начальной схемы:

```bash
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | \
mysql --default-character-set=utf8mb4 -uzabbix -p zabbix
```

Отключение опции после импорта:

```bash
mysql -uroot -p
```

```sql
SET GLOBAL log_bin_trust_function_creators = 0;
QUIT;
```

---

### d. Настройка базы данных для Zabbix Server

Отредактируйте файл:

```
/etc/zabbix/zabbix_server.conf
```

Добавьте параметр:

```
DBPassword=password
```

---

### e. Запуск сервисов

```bash
systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2
```

---

### Скриншот

![Zabbix Server](https://github.com/user-attachments/assets/72d2007f-0739-4927-b0e0-8fadcc8c3dec)

---

## Задание 2

### Установка Zabbix Agent

```bash
wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest+ubuntu22.04_all.deb
dpkg -i zabbix-release_latest+ubuntu22.04_all.deb
apt update
apt install -y zabbix-agent
```

---

### Настройка агента

```bash
nano /etc/zabbix/zabbix_agentd.conf
```

---

### Запуск агента

```bash
systemctl restart zabbix-agent
systemctl enable zabbix-agent
```

---

### Скриншоты

![Agent 1](https://github.com/user-attachments/assets/4c0233de-bbb5-4f82-8b98-6dbc2fb5c0dd)

![Agent 2](https://github.com/user-attachments/assets/865a12f9-593e-4ecd-a25d-3b5d97d9a901)

![Agent 3](https://github.com/user-attachments/assets/03a14720-7e37-4783-a502-531338167f65)
