# Домашнее задание к занятию   
**"`Система мониторинга Zabbix. Часть 1`"** - `Воскобойников Арсений Петрович`
   
**Задание 1**  
Установите Zabbix Server с веб-интерфейсом.  
Процесс выполнения
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.
Требования к результатам  
- Прикрепите в файл README.md скриншот авторизации в админке.
- Приложите в файл README.md текст использованных команд в GitHub.

# **Ответ**

Окно авторизации в админке Забикс  <img src = "img/HW1_task1_screen3_залогинился в систему.jpg" width = 100%>

**Текст использованные команд**:  
1. В формате скриншота:

<img src = "img/HW1_task1_screen1_ip address системы и команды для устанвоки забикса.jpg" width = 100%>
 
<img src = "img/HW1_task1_screen2_команды в всистеме.jpg" width = 100%>  

# **В формате текста:**

**Ставлю PostgreSQL**
```
# sudo apt install postgresql
``` 
**Ставлю  репозиторий Zabbix**
```
# wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_6.0+debian11_all.deb
# dpkg -i zabbix-release_latest_6.0+debian11_all.deb
# apt update
``` 
**Ставлю  Zabbix сервер, веб-интерфейс и агент**

```
# apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```
**Создаю базу данных**
```
# sudo -u postgres createuser --pwprompt zabbix
# sudo -u postgres createdb -O zabbix zabbix
``` 
**Импортирую начальную схему**
```
# zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
```
**Настраиваю пароль для базы данных**
```
Редактирую  файл /etc/zabbix/zabbix_server.conf
DBPassword=password
``` 
**Запускаю процессы Zabbix сервера и агента**
```
# systemctl restart zabbix-server zabbix-agent apache2
# systemctl enable zabbix-server zabbix-agent apache2
```

**Открываю веб интерфейс**
```
http://192.168.8.137/zabbix/
``` 

# **Задание 2**  
Установите Zabbix Agent на два хоста.

Процесс выполнения
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.  
**Требования к результатам:**  
- Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу.  
- Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером.  
- Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.  
- Приложите в файл README.md текст использованных команд в GitHub.  

# **Ответ**
# **В формате скриншотов:**
- cкриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу:  <img src = "img/HW1_task2_screen1_Configuration _Hosts.jpg" width = 100%>

- cкриншот лога zabbix agent, где видно, что он работает с сервером:  <img src = "img/HW1_task2_screen1_zabbix agent log.jpg" width = 100%>

- cкриншот (часть1) раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные:  <img src = "img/HW1_task2_screen1_Monitoring_Latest data_1.jpg" width = 100%>

- cкриншот (часть2) раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные:  <img src = "img/HW1_task2_screen1_Monitoring_Latest data_2.jpg" width = 100%>

- cкриншот (часть3) раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные:  <img src = "img/HW1_task2_screen1_Monitoring_Latest data_3.jpg" width = 100%>

# **В формате текста:**
**Добавляю репозиторий Zabbix:**
```
# wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/
zabbix-release_6.0-4%2Bdebian11_all.deb
dpkg -i zabbix-release_6.0-4+debian11_all.deb
apt update
```

**Устонавливаю Zabbix agent и компоненты::**
```
# sudo apt install zabbix-agent -y
```
**Запусскаю Zabbix agent:**
```
# sudo systemctl restart zabbix-agent
# sudo systemctl enable zabbix-agent
```
**Добавляю адрес сервера на Zabbix agent:**
```
sudo nano /etc/zabbix/zabbix_agentd.conf
```

# **Задание 3 со звёздочкой***  
Установите Zabbix Agent на Windows (компьютер) и подключите его к серверу Zabbix.

**Требования к результатам**  
- Приложите в файл README.md скриншот раздела Latest Data, где видно свободное место на диске C:


# **Ответ**

Cкриншот раздела Latest Data, где видно свободное место на диске C:  <img src = "img/HW1_task3_windows_mashine_disk.jpg" width = 100%>
