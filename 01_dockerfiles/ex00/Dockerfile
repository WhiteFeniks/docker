# Exercise 00. Из alpine образа вы добавите в свой контейнер свой любимый текстовый 
# редактор vim или emacs тот, который запустится вместе с вашим контейнером.

FROM alpine

MAINTAINER umoff <umoff@student.21-school.ru>

RUN apk update && \
	apk upgrade && \
	apk add vim

ENTRYPOINT vim

# How to build:
# Установить docker и его окружение
# Проверить нахожусь ли я в папке с Dockerfile
# docker build -t ex00 .

# How to run:
# docker run --rm -ti ex00

