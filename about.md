## Создать свой кастомный образ nginx на базе alpine

Установть docker
sudo yum install -y yum-utils
sudo yum-config-manager \
	--add-repo \
	https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io

Запустить службу
systemctl start docker

Добавить службу в автозагрузку
systemctl enable docker

В новой директории создать три файла:
Dockerfile  index.html  nginx.conf

Перейти в суперпользователя
sudo su

Создаем новый образ находясь в директории с нашими файлами
docker build -t nginx:alpine .

Запускаем контейнер с пробросом порта
docker run -d -p 8080:80 nginx:alpine

Проверяем, что контейнер запущен
docker ps

Обращаемся к localhost для проверки (видим текст приветсвия)
curl localhost:8080

Логинимся на DockerHub
docker login

Указываем образ, который хотим залить на dockerhub
docker tag nginx:alpine remizov/nginx-on-alpine

И загружаем в репозитарий DockerHub
docker push remizov/nginx-on-alpine

Удаляем все ранее созданные контейнеры и образы, и проверяем новый образ
docker pull remizov/nginx-on-alpine

Проверить создание образа
docker images

Создать контейнер из нового образа
docker run -d -p 8080:80 remizov/nginx-on-alpine

Обращаемся к localhost для проверки (видим текст приветсвия)
curl localhost:8080

