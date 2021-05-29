# Exercise 03: ... and bacon strips ... and bacon strips. Docker может быть полезен для 
# тестирования приложения, которое все еще разрабатывается, не загрязняя ваши библиотеки. 
# Вам нужно будет создать Dockerfile, который получит версию разработки 
# Gitlab - Community Edition, установит ее со всеми зависимостями и необходимыми 
# конфигурациями и запустит приложение по мере его сборки. Контейнер будет считаться 
# действительным, если вы можете получить доступ к веб-клиенту, создать пользователей 
# и взаимодействовать с этим контейнером через GIT (HTTPS и SSH). Очевидно, что вам 
# не разрешается использовать официальный контейнер от Gitlab, это было бы позором...

FROM ubuntu:16.04

MAINTAINER umoff <umoff@student.21-school.ru>

ENV TERM=xterm

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y xterm ca-certificates openssh-server wget postfix

RUN wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh && chmod 777 script.deb.sh && ./script.deb.sh && apt-get install -y gitlab-ce

RUN apt update && apt install -y tzdata && \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN sed -i "s/# grafana\['enable'\] = true/grafana['enable'] = false/g" /etc/gitlab/gitlab.rb

EXPOSE 443 80 22

ENTRYPOINT (/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl reconfigure && tail -f /dev/null

# Additionally:
# Доументация на сайте: https://about.gitlab.com/install/ или https://about.gitlab.com/install/# (ubuntu).
# ENV TERM=xterm - необходимо для установки переменной среды оболочку терминала (иначе 
# ошибка Environment variable: TERM has not been set).
# postfix - необходим для того чтобы отправлять уведомления на электронную почту.
# RUN wget - получаем пакет с официального сайта, настриваем ему разрешения и запускаем установочный файл с Gitlab COMMUNITY EDITION.

# RUN apt update - необходимо, чтобы не возникало ошибки: "gitlab-rails recipe fails with TZInfo::DataSourceNotFound". Обновляем, устанавливаем tzdata и чистим всё старое

# RUN sed - для редактирования потоков фильтраци и преобразования текста, 
# i - редактировать файл в определенном месте. Нам нужно отредактировать 
# файл /etc/gitlab/gitlab.rb и установить значение на false, чтобы не было ошибки
# "Error executing action `run` on resource 'ruby_block[authorize Grafana with GitLab]'".
# Это нужно потому что Grafana используется для мониторинга событий, происходящих в GitLab, но
# для авторизации может потребоваться вечность, и иногда просто отказывается 
# инициализироваться должным образом. Подробнее:
# https://gitlab.com/gitlab-org/omnibus-gitlab/-/issues/5044

# EXPOSE - необходимые порты. Стандартно 443 - HTTPS, 80 - HTTP, 22 - SSH:
# https://about.gitlab.com/blog/2016/02/18/gitlab-dot-com-now-supports-an-alternate-git-plus-ssh-port/ 
#  Подробнее и другие компонеты:
# https://docs.gitlab.com/omnibus/package-information/defaults.html

# ENTRYPOINT /opt/gitlab/embedded/bin/runsvdir-start & - чтобы не выходила ошибка "Freeze on
# ruby_block[supervise_redis_sleep] action run". 
# tail -f /dev/null - чтобы Gitlab повис и не закрывался. 

# How to build:
# docker build -t ex03 .
# docker run -it --shm-size=4g --rm -p 8080:80 -p 8022:22 -p 8443:443 --privileged ex03
# http://192.168.99.107:8080
