# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Гак Ярослав`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

#### Установите Zabbix Server с веб-интерфейсом.
#### Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов 
Требования к результатам
Прикрепите в файл README.md скриншот авторизации
Приложите в файл README.md текст использованных команд в GitHub.

```
-sudo apt update...
-wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.4-1+ubuntu22.04_all.deb
-dpkg -i zabbix-release_6.4-1+ubuntu22.04_all.deb
-apt update 
-apt install zabbix-server-pgsql zabbix-frontend-php php8.1-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
-sudo -u postgres createuser --pwprompt zabbix
-sudo -u postgres createdb -O zabbix zabbix
-zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
-nano /etc/zabbix/zabbix_server.conf
__CTRL+w: DBP__ DBPassword=password
-sudo systemctl restart zabbix-server zabbix-agent apache2
-sudo systemctl enable zabbix-server zabbix-agent apache2
```
Процесс установки Zabbix Server

![alt text](https://github.com/Anudora41/sys-pattern-homework/blob/main/баш.png)
![alt text](https://github.com/Anudora41/sys-pattern-homework/blob/main/установка.png)

Состояние сервера

![alt text](https://github.com/Anudora41/sys-pattern-homework/blob/main/сервер.png)

В самом Zabbix

![alt text](https://github.com/Anudora41/sys-pattern-homework/blob/main/вход.png)
![alt text](https://github.com/Anudora41/sys-pattern-homework/blob/main/как%20выглядид%20ссылка.jpg)

---

### Задание 2

#### Установите Zabbix Server с веб-интерфейсом.
#### Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов 
Требования к результатам
   
1.Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
![alt text](https://github.com/Anudora41/sys-pattern-homework/blob/main/хосты.png)
2.Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
![alt text](https://github.com/Anudora41/sys-pattern-homework/blob/main/агент%20работает.png)
3.Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
![alt text](https://github.com/Anudora41/sys-pattern-homework/blob/main/мониторинг.png)
4.Приложите в файл README.md текст использованных команд в GitHub
```
-sudo apt update
-wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.4-1+ubuntu22.04_all.deb
-dpkg -i zabbix-release_6.4-1+ubuntu22.04_all.deb
-apt update
-apt install zabbix-agent
-systemctl restart zabbix-agent
-systemctl enable zabbix-agent
-sudo nano /etc/zabbix/zabbix_agentd.conf
-systemctl restart zabbix-agent
```


---

