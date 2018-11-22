1. Список контейнеров `docker ps -a`
2. Загрузить контейнер `docker pull pocket_name`
3. Следить за логами контейнера `docker logs --follow my_container`
4. Удаление контейнера `docker rm my_container`
5. Удаление образа `docker rmi`
6. Остановить контейнер `docker stop my_container`, all - `docker stop $(docker ps -a -q)`, грубый - `docker kill my_container`
7. Запустить контейнер `docker run my_container`