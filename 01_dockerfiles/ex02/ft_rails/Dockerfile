FROM ruby

MAINTAINER umoff <umoff@student.21-school.ru>

RUN apt-get update && apt-get install -y nodejs
RUN gem install rails --version 5.2.0

RUN mkdir -p /opt/app
COPY ./app /opt/app

ONBUILD WORKDIR /opt/app
ONBUILD RUN bundle install
ONBUILD RUN rake db:create
ONBUILD RUN rake db:migrate
ONBUILD RUN rake db:seed

# Additionally:
# WORKDIR - приложение rails должно быть скопировано в папку /opt/app.
# ONBUILD RUN - добавляет к образу триггер-комманду, которая будет выполнена позже,
# когда образ будет использоваться в качестве основы для другой сборки.
# ONBUILD RUN rake - создает свою базу данных, переносит и размещает ее в общем доступе.# Развертывание контейнеров docker с помощью rake. Это особенно полезно для 
# докеризованных приложений Ruby

# How to buld:
# git clone https://github.com/RailsApps/rails-signup-thankyou.git app
# docker build -t ft-rails:on-build .
# docker build -t ex02 .
# docker run -it --rm -p 3000:3000 ex02
