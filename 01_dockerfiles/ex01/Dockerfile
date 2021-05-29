# Exercise 01: BYOTSS. Из образа debian вы добавите соответствующие источники для
# создания сервера TeamSpeak, который будет запущен вместе с вашим контейнером. 
# Он будет считаться действительным, если хотя бы один пользователь сможет подключиться 
# к нему и участвовать в обычном обсуждении (без надуманной установки), поэтому 
# обязательно создайте свой Dockerfile с правильными опциями. Ваша программа должна
# получить исходники при сборке, они не могут быть в вашем репозитории

FROM debian

MAINTAINER umoff <umoff@student.21-school.ru>

ENV TS3SERVER_LICENSE=accept

WORKDIR /home/teamspeak

EXPOSE 9987/udp 10011 30033

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y wget bzip2 && \
    wget http://dl.4players.de/ts/releases/3.8.0/teamspeak3-server_linux_amd64-3.8.0.tar.bz2 && \
    tar -xvf teamspeak3-server_linux_amd64-3.8.0.tar.bz2

WORKDIR teamspeak3-server_linux_amd64

ENTRYPOINT sh ts3server_minimal_runscript.sh

# Additionally:
# ENV TS3SERVER_LICENSE=accept - нужно для переопределения переменной env TS3SERVER 
# с доступом accept, иначе сервер просто выдаст информацию о том, что лицензия 
# не принята, и не запустится.

# WORKDIR - задает рабочий каталог для RUN, CMD, ENTRYPOINT, COPY и ADD инструкций, которые следуют за ним.

# EXPOSE - говорит докеру, что контейнер прослушивает указаные сетевые порты во время выполнения. Открытые используемые порты для TeamSpeak:
# 9987-9999: порты UDP голосового/виртуального сервера
# 10011: запрос TCP-порта
# 30033: TCP-порт передачи файлов

# RUN - для запуска установки debian и обновления до последней версии, потом мы 
# получаем bzip2 компрессор (утилита командной строки для сжатия данных), чтобы 
# открыть сервер teamspeak и получить сервер ts от 4Players. 
# Последнии версии здесь: http://dl.4players.de/ts/releases/

# How to build:
# docker build -t ex01 .

# How to run:
# docker run --rm -p 9987:9987/udp -p 10011:10011 -p 30033:30033 ex01

# Additionally:
# https://docs.docker.com/samples/library/teamspeak/#container-shell-access 
# https://www.vultr.com/docs/how-to-install-teamspeak-3-server-on-ubuntu-16-04-64-bit
# https://disk.yandex.ru/i/Ph5SqRM_qiUXUw
