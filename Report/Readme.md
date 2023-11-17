# Создадим docker image (образ)
Для этого напишем Dockerfile. Создаём пустой текстовый документ, где в первую очередь указываем, на основе какого образа будет работать наш.
```
FROM ubuntu:latest
```
Далее указываем, что мы хотим запустить. В нашем случае мы обновляем пакетный менеджер и устанавливаем необходимое нам ПО.
```
RUN apt-get update && apt-get install -y libaa-bin && apt-get install -it iputils-ping
```
![image](https://github.com/cs-itmo-2023/lab-4-Andrzakourcev/assets/144477949/fa516989-be77-4c82-923c-d640c5d6fd44)

На этом Dockerfile готов, закрываем и сохраняем его под этим названием. В терминале в папке с этим файлом запускаем команду сборки образа с тегом “aafire”.
```
docker build -t aafire .
```
Далее можем запустить контейнер и  подключиться к нему напрямую командой
```
docker run -it aafire
```
И уже напрямую в терминале контейнера запустить команду 
```
aafire
```
![image](https://github.com/cs-itmo-2023/lab-4-Andrzakourcev/assets/144477949/1b83e701-d5f7-44e6-8932-09b0a7e4dec2)

Видно, что контейнер запущен и все работает.

Теперь запустим 2 контейнера из нашего образа и настроим связь между ними.

![image](https://github.com/cs-itmo-2023/lab-4-Andrzakourcev/assets/144477949/54b89f8b-2105-47b3-b079-5fe28ba48c14)

Откроем ещё одно окно терминала и создадим сеть при помощи команды:
```
docker network create mynetwork
```
После этого нужно подключим контейнеры к нашей сети. Названия контейнеров можно увидеть при выводе списка действующих контейнеров.

![image](https://github.com/cs-itmo-2023/lab-4-Andrzakourcev/assets/144477949/acbc5c97-9d2a-410c-b67c-d868cc5db200)

Теперь при помощи следующей команды посмотрим настройки нашей сети.
```
docker network inspect mynetwork
```
![image](https://github.com/cs-itmo-2023/lab-4-Andrzakourcev/assets/144477949/f2f247cc-d6f4-410c-b0e9-1c95f590ad1a)

Контейнеры соединены. Теперь проверим соединение при помощи команды ping. Ip-адреса мы узнали из предыдущей команды.

![image](https://github.com/cs-itmo-2023/lab-4-Andrzakourcev/assets/144477949/43c2dab6-2c26-4968-9668-2d95f1cff399)

Все отлично работает!












