# 9-02hw
# Система мониторинга Zabbix - Дрибноход Давид

## Задание 1.
![Скриншот 1](https://github.com/DrDavidN/9-02hw/blob/main/z1img/9-02z1_1.JPG)
```bash
### Установка postgresql
apt update
apt install postgresql
### Установка репозитория zabbix
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
dpkg -i zabbix-release_6.0-4+debian11_all.deb
apt update
### Установrf Zabbix сервера и веб-интерфейса
apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts
### Создание пользователя и базы данных
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
### Импорт схемы и данных в базу
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
### Конфигурирование сервера указываем пароль на базу DBPassword=****
nano /etc/zabbix/zabbix_server.conf
### Перезапуск служб и установка автозапуска
systemctl restart zabbix-server apache2
systemctl enable zabbix-server apache2
```

## Задание 2.
![Скриншот 1](https://github.com/DrDavidN/9-02hw/blob/main/z2img/9-02z2_1.JPG)
![Скриншот 1](https://github.com/DrDavidN/9-02hw/blob/main/z2img/9-02z2_2.JPG)
![Скриншот 1](https://github.com/DrDavidN/9-02hw/blob/main/z2img/9-02z2_3.JPG)
```bash
### Установка репозитория zabbix
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
dpkg -i zabbix-release_6.0-4+debian11_all.deb
apt update
### Установка zabbix-agent
apt install zabbix-agent
### Конфигурирование zabbix-agent указываем адрес сервера Server=84.201.162.14
nano /etc/zabbix/zabbix_agentd.conf
#### Перезапуск службы и устуановка автозапуска
systemctl restart zabbix-agent
systemctl enable zabbix-agent
```

