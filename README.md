# Домашнее задание к занятию «Система мониторинга Zabbix» -Белов Антон

### Задание 1 

Установите Zabbix Server с веб-интерфейсом.


1.Установите PostgreSQL.
```bash
sudo apt update
```
```bash
sudo apt install postgresql
```
2. Устанавливаю репозиторий Zabbix:
```bash
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4%2Bubuntu22.04_all.deb
```
```bash
dpkg -i zabbix-release_6.0-4+ubuntu22.04_all.deb
```
```bash
apt update
```
3. Устанавливаю Zabbix сервер, веб-интерфейс и агент:
```bash
sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.1-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```
4. Создаю пользователя и БД:
```bash
sudo -u postgres createuser --pwprompt zabbix
```
```bash
sudo -u postgres createdb -O zabbix zabbix
```
5. Импортирую начальную схему и данные:
```bash
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
```
6. Редактирую файл файл /etc/zabbix/zabbix_server.conf :
```
DBPassword=password
```
7. Запускаю процессы Zabbix сервера и агента и настраиваю их запуск при загрузке ОС:
```bash
systemctl restart zabbix-server zabbix-agent apache2
```
```bash
systemctl enable zabbix-server zabbix-agent apache2
```
![tz_1.1](scrshts/tz_1.1.png?raw=true "Optional Title")

### Задание 2 

Установите Zabbix Agent на два хоста.
1. Устанавливаю репозиторий Zabbix на оба хоста:
```bash
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4%2Bubuntu22.04_all.deb
```
```bash
dpkg -i zabbix-release_6.0-4+ubuntu22.04_all.deb
```
```bash
apt update
```
2. Устанавливаю Zabbix-agent на оба хоста:
```bash
apt install zabbix-agent
```
3. Добавляю адрес zabbix-server в zabbix_agent.conf на обоих хостах:
```bash
sudo nano /etc/zabbix/zabbix_agent.conf
```
4. Рестарт и автозапуск Zabbix-agent на обоих хостах:
```bash
sudo systemctl restart zabbix-agent
```
```bash
sudo systemctl enable zabbix-agent
```

![tz_2.1](scrshts/tz_2.1.png?raw=true "Optional Title")
![tz_2.2](scrshts/tz_2.2.png?raw=true "Optional Title")
![tz_2.3](scrshts/tz_2.3.png?raw=true "Optional Title")
![tz_2.4](scrshts/tz_2.4.png?raw=true "Optional Title")
