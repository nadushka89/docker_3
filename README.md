# Контейнеризация семинары №3


![](https://github.com/nadushka89/docker_3/blob/main/source/docker.jpg?raw=true)

## Урок 3. Введение в Docker

Задание:
1. Запустить контейнер с БД mariaDB, используя инструкции на сайте hub.docker.com.
2. Слинковать папку с базой данных с контейнера с mariaDB в папку на хосте (как на семинаре /var/lib/mysql). Заполнить БД данными или добавить запись и проверить, что файлы базы данных появились на хостовой машине. - Если выполняете этот пункт то оценка . Хорошо
3. Запустить phpmyadmin (в контейнере) и через веб проверить, что все введенные данные доступны. http://localhost:8081/ Отлично
4. *(не обязательно) Запустить контейнер с postgeSQL и подсоеденить к этому контейнеру adminer (графическое управдение базой данных) Отлично
Формат сдачи ДЗ: предоставить доказательства выполнения задания посредством ссылки на google-документ с правами на комментирование/редактирование.
Результатом работы будет: текст объяснения, логи выполнения, история команд и скриншоты (важно придерживаться такой последовательности).
В названии работы должны быть указаны ФИ, номер группы и номер урока

**Задание:**

Запускаем образ с помощью команды:
```
sudo docker run -it ubuntu:22.10 bash
ls -l
```
Выводим список запущенных контейнеров:
```
docker ps
```
Слинкуем локальную папку с папкой /var/lib/mysql, передадим пароль и запустить контейнер mariadb:10.10.2 командой:

```
docker run --name test-mariadb-gb-5 -v ./mydb:/var/lib/mysql -e MARIADB_ROOT_PASSWORD=nadi123 -d mariadb:10.10.2
```
Заходим в этот контейнер командой:
```
docker exec -it b258c7dda708 bash
```
![](https://github.com/nadushka89/docker_3/blob/main/source/1.png?raw=true)

Заходим внутрь базы данных
```
mysql -u root -p
```
Создаем базу данных:
```
CREATE DATABASE GB ;
```
![](https://github.com/nadushka89/docker_3/blob/main/source/2.png?raw=true)

Мы видим,что эта база данных появилась на хостовой машине:

![](https://github.com/nadushka89/docker_3/blob/main/source/3.png?raw=true)

Связываем 2 контейнера:
```
docker run --name my-phpmyadmin-gb-4 -d --link test-mariadb-gb-5:db -p 8081:80 phpmyadmin/phpmyadmin
```
И смотрим у нас запустился на порт 8081 phpmyadmin
![](https://github.com/nadushka89/docker_3/blob/main/source/4.png?raw=true)

Заходим в браузер и вводим localhost:8081, вводим данные root и пароль и создаем базу данных новую. Смотрим,что она появилась у нас в терминале.

![](https://github.com/nadushka89/docker_3/blob/main/source/5.png?raw=true)

![](https://github.com/nadushka89/docker_3/blob/main/source/6.png?raw=true)
