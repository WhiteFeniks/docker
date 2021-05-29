FROM debian

MAINTAINER umoff <umoff@student.21-school.ru>

RUN apt-get update -y && apt-get install nsnake -y  

ENTRYPOINT /bin/bash

# Игра змейка
# How to build and run:
# docker build -t ex01 .
# docker run --rm -ti ex01
# в папке /usr/games run  command ./nsnake, to exit touch Control + C
