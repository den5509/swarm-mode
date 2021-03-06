## Лабораторная работа
Исследование Swarm-mode Docker

Работу выполнил: А.И. Позняков, гр. 4645М 

### Цель работы

Исследовать технологию Swarm mode в Docker 

### Задание

В лабораторной работе необходимо выполнитьследующие действия:

- Запустить 3 Docker контейнера в режиме Docker Swarm-mode
- Проанализировать результаты и сделать выводы
- Отчетную документацию предоставить при помощи облачных технологий

### Содержание

Для работы с роем контейнеров использовался docker-machine. Для создания хостов с установленным на них Docker Engine использовался драйвер virtualbox.

Сначало были созданны будующие узлы роя при помощи команд:


```
docker-machine create -d virtualbox node1  
docker-machine create -d virtualbox node2  
docker-machine create -d virtualbox node3
```

Информацию о созданных узлах можно вывести при помощи команды:

```
docker-machine ls
```
![alt]({{ "/assets/images/docker-machine-ls.png" | absolute_url }})

Рисунок 1 - Информация о созданных узлах

Далее осуществлена инициализация роя с менеджером node1. Это было выполнено командой:

```
docker swarm init --advertise-addr 192.168.99.100:2377
```
![alt]({{ "/assets/images/docker-swarm-init.png" | absolute_url }})

Рисунок 2 - Инициализация роя с менеджером node1

При инициализации, на экран была выведена команда для присодинения к этому рою новых узлов в качестве рабочих.

При помощи этой команды к рою были присоединены node2 и node3


![alt]({{ "/assets/images/node2-join.png" | absolute_url }})

Рисунок 3 - Присоединение узла node2

![alt]({{ "/assets/images/node3-join.png" | absolute_url }})

Рисунок 4 - Присоединение узла node3

В итоге, получен рой из 3 контейнеров, информацию о котором можно вывести командой:

```
docker node ls
```
![alt]({{ "/assets/images/docker-node-ls.png" | absolute_url }})

Рисунок 5 - Информация о созданном рое из 3 контейнеров

### Выводы

1. Минимально рой контейнеров может состоять из 1 элемента
2. Масштабируемость может доступна при 2 контейнерах;
3. Высокая доступность обеспечивается при трех и более элементах

