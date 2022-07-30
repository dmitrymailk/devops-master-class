# Docker Commands

1. Проверить версию докера

   docker --version

2. Создать и запустить контейнер по имени "in28min/hello-world-python:0.0.1.RELEASE, пробросить порты из контейнера на реальную машину, в данном случае мы откроем на реальной машине 5000 порт и будем обращаться к 5000 в докер контейнере. Далее все аналогично только для других образов.

   docker run -p 5000:5000 in28min/hello-world-python:0.0.1.RELEASE

   docker run -p 5000:5000 in28min/hello-world-java:0.0.1.RELEASE

   docker run -p 5000:5000 in28min/hello-world-nodejs:0.0.1.RELEASE

3. Создать и запустить контейнер, но сделать это в фоне

   docker run -d -p 5000:5000 in28min/hello-world-nodejs:0.0.1.RELEASE

4. Создать и запустить контейнер в фоне, только теперь на настоящей машине он будет доступен по порту 5001

   docker run -d -p 5001:5000 in28min/hello-world-python:0.0.1.RELEASE

5. Получить логи конкретного контейнера по его ID

   docker logs 04e52ff9270f5810eefe1f77222852dc1461c22440d4ecd6228b5c38f09d838e

   docker logs c2ba

6. Показать список всех локально доступных образов(образ это типа класса в языках программирования) на машине

   docker images

7. Показать список работающих контейнеров

   docker container ls

8. Показать все контейнеры

   docker container ls -a

9. Остановить какой-то контейнер по его ID

   docker container stop f708b7ee1a8b

10. Скачать образ под названием "mysql"

    docker pull mysql

11. Найти на dockerhub образ с названием "mysql"

    docker search mysql

12. Посмотреть историю изменений какого-то образа, в данном случае образа под названием "in28min/hello-world-java:0.0.1.RELEASE" или с ID 100229ba687e

    docker image history in28min/hello-world-java:0.0.1.RELEASE

    docker image history 100229ba687e

13. Посмотреть метаданные которые идут вместе с образом. В данном случае нас интересует образ с ID 100229ba687e

    docker image inspect 100229ba687e

14. Удалить образ локально, чтобы он не занимал место на диске.

    docker image remove mysql

    docker image remove in28min/hello-world-java:0.0.1.RELEASE

15. Удалить локально контейнер, по его ID.

    docker container rm 3e657ae9bd16

16. Поставить контейнер по, по его ID. После того как мы поставим его на паузу, он не будет принимать ни каких запросов. Стейт запущенного приложения сохранится.

    docker container pause 832

17. Снять с паузы контейнер

    docker container unpause 832

18. Остановить контейнер. Стейт приложения сбросится.

    docker container stop 832

19. Удалить все остановленные контейнеры.

    docker container prune

20. Узнать общую информацию о занимаемом пространстве образов и контейнеров

    docker system df

21. Узнать подробную информацию о самом докере

    docker system info

22. Удалит все остановленные контейнеры, все networks которые нигде не используются, все образы без контейнеров, очистит кеш

    docker system prune -a

23. Показать информацию о потреблении CPU, оперативки, памяти, использование сети

    docker stats 9009722eac4d

24. Создать и запустить контейнер с ограничением по памяти в 512 mb и ограничением в использование CPU в 50к, это значит что если машина имеет 8 ядер она задействует из них только 5. Если бы было 15к тогда только 1.5 ядра и тд.

    docker container run -p 5000:5000 -d -m 512m --cpu-quota=50000 in28min/hello-world-java:0.0.1.RELEASE

25. Собрать образ из Dockerfile и назвать его "in28min/hello-world-python:0.0.2.RELEASE"

    docker build -t in28min/hello-world-python:0.0.2.RELEASE .

26. Запушить образ с именем "in28min/hello-world-python:0.0.2.RELEASE" на dockerhub

    docker push in28min/hello-world-python:0.0.2.RELEASE

27. Создать и запустить контейнер, заменив у него начальную команду из CMD на "ping google.com". Именно поэтому желательно использовать ENTRYPOINT, если мы хотим чтобы эта команда точно исполнилась.

    docker run -d -p 5001:5000 in28min/hello-world-nodejs:0.0.3.RELEASE ping google.com

28. Создать и запустить контейнер с именем "currency-exchange"

    docker run -d -p 8000:8000 --name=currency-exchange in28min/currency-exchange:0.0.1-RELEASE

29. Проверить все доступные networks.

    docker network ls

30. Проверить информацию о сетевом драйвере по умолчанию.

    docker network inspect bridge

31. Создать bridge с названием "currency-network". Более подробно про эту команду можно прочитать [тут](https://docs.docker.com/engine/reference/commandline/network_create/)

    docker network create currency-network

32. Остановить сеть с названием "currency-exchange"

    docker container stop currency-exchange

33. docker-compose это оркестратор докер контейнеров. Если раньше мы передавали параметры через специальные параметры, когда запускали контейнер или создавали сеть. То теперь все эти параметры можно прописать в yml файле и передать его в docker-compose. Он автоматически создаст все нужные микросервисы

    docker-compose --version

34. Запустит и начнет сборку микросервисов. Изначально он ищет файл с названием docker-compose.yml в дирректории где была запущена данная команда. Второй вариант аналогично docker. Он запустит сборку в фоне.

    docker-compose up

    docker-compose up -d

35. Оставновить все связанные микросервисы

    docker-compose down
