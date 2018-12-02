[Docker Hub](https://hub.docker.com/)

# Команды
1. Список контейнеров `docker ps -a -s --no-trunc`
1. Список образов `docker images`
1. Загрузить контейнер `docker pull pocket_name`
1. Следить за логами контейнера `docker logs --follow my_container`
1. Удаление контейнера `docker rm my_container`
1. Удаление образа `docker rmi`
1. Остановить контейнер `docker stop my_container`, all - `docker stop $(docker ps -a -q)`, грубый - `docker kill my_container`
1. Запустить контейнер `docker run my_container`
1. Именованные `docker run --name hello-world my_container`
1. Перезапуск `docker run -dit --restart always`
1. Переименовать образ `docker tag <existing image name> <new image name>`
1. Пауза `docker pause nginx //unpause`
1. Подключение к контейнеру `docker attach nginx`
1. Информация по контейнеру `docker inspect infinite`, `docker inspect --format '{{ .NetworkSettings.IPAddress }}' $(docker ps -q)`
1. События по контейнеру `docker events infinite`
1. Публичные порты `docker port infinite`
1. Выполняющиеся процессы `docker top infinite`
1. Использование ресурсов `docker stats infinite`
1. Передача переменных среды в контейнер `docker run --rm -it -e ENV_FROM_HOST="123" busybox`
1. Монтаж каталогов хоста `docker run --rm -v ~/data:/data busybox cat /data/1.txt`
1. Предоставление портов хосту `-p <host port>: <открытый порт контейнера>`
    `docker run --name nginx --rm -d -p 9000:80 nginx`
1. Выполнение команды внутри исполняемого контейнера `docker exec nginx cat /etc/nginx/nginx.conf | grep worker_processes`
`docker exec -it nginx bash`

[Статья](https://habr.com/company/flant/blog/336654/)