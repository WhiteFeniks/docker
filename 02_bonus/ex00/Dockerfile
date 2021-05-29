FROM gcc:4.9

MAINTAINER umoff <umoff@student.21-school.ru>

COPY . /usr/src/myapp

WORKDIR /usr/src/myapp

RUN gcc -o myapp hello.c

CMD ["./myapp"]

# How to build and run:
# docker build -t my-gcc-app .
# docker run -it --rm --name my-running-app my-gcc-app
