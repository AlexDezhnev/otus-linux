```
Вся лаба в vagrant файле. При запуске создается 7 vm с заданными именами
Прописывается адресация и маршрутизация
В файле 25.Network.jpg схема сети
```

# Архитектура

Сеть central
- 192.168.0.0/28   - directors
- 192.168.0.32/28  - office hardware
- 192.168.0.64/26  - wifi

Сеть office1
- 192.168.2.0/26    - dev
- 192.168.2.64/26   - test servers
- 192.168.2.128/26  - managers
- 192.168.2.192/26  - office hardware

Сеть office2
- 192.168.1.0/25    - dev
- 192.168.1.128/26  - test servers
- 192.168.1.192/26  - office hardware

```
Office1 ---\
       -----> Central --IRouter --> internet
Office2----/
```

# В задании не указано
- сети в office1 и office2, к которым подключены серверы. Будут использоваться сети test servers
- сети, через которые office1Router и office2Router подключены к centralRouter. Будет использоваться сеть office hardware

# Созданы сервера
- inetRouter
- centralRouter
- office1Router
- office2Router
- centralServer
- office1Server
- office2Server

# Теоретическая часть

# Найти свободные подсети

Сеть central
- 192.168.0.64/26 - wifi

Сеть office1
- 192.168.2.0/26 - dev
- 192.168.2.128/26 - managers
- 192.168.2.192/26 - office hardware

Сеть office2
- 192.168.1.0/25 - dev
- 192.168.1.192/26 - office hardware


# Посчитать сколько узлов в каждой подсети, включая свободные

Формат - общая емкость (включая адрес сети и броадкаст), количество доступных адресов хостов, использовано (включая маршрутизатор), количество свободных адресов

Сеть central
- 192.168.0.0/28   - directors          - емкость 16 (14 доступных), использовано 2, 12 свободно
- 192.168.0.32/28  - office hardware    - емкость 16 (14 доступных), использовано 3, 11 свободно
- 192.168.0.64/26  - wifi               - емкость 64 (62 доступных), использовано 1, 61 свободно

Сеть office1
- 192.168.2.0/26    - dev               - емкость 64 (62 доступных), использовано 1, 61 свободно
- 192.168.2.64/26   - test servers      - емкость 64 (62 доступных), использовано 2, 60 свободно
- 192.168.2.128/26  - managers          - емкость 64 (62 доступных), использовано 1, 61 свободно
- 192.168.2.192/26  - office hardware   - емкость 64 (62 доступных), использовано 1, 61 свободно

Сеть office2
- 192.168.1.0/25    - dev               - емкость 128 (126 доступных), использовано 1, 125 свободно
- 192.168.1.128/26  - test servers      - емкость 64 (62 доступных), использовано 2, 60 свободно
- 192.168.1.192/26  - office hardware   - емкость 64 (62 доступных), использовано 1, 61 свободно


# Указать broadcast адрес для каждой подсети

Сеть central
- 192.168.0.0/28   - directors          - 192.168.0.15
- 192.168.0.32/28  - office hardware    - 192.168.0.47
- 192.168.0.64/26  - wifi               - 192.168.0.127

Сеть office1
- 192.168.2.0/26    - dev               - 192.168.2.63
- 192.168.2.64/26   - test servers      - 192.168.2.127
- 192.168.2.128/26  - managers          - 192.168.2.191
- 192.168.2.192/26  - office hardware   - 192.168.2.255

Сеть office2
- 192.168.1.0/25    - dev               - 192.168.1.127
- 192.168.1.128/26  - test servers      - 192.168.1.191
- 192.168.1.192/26  - office hardware   - 192.168.1.255


# проверить нет ли ошибок при разбиении

Адреса сетей корректны, пересечений нет

# Практическая часть
- Соединить офисы в сеть согласно схеме и настроить роутинг
```
Сделано. Маршруты добавлены
```
- Все сервера и роутеры должны ходить в инет черз inetRouter
```
Сделано. У всех устройств за главным роутером основной маршрут - ближайший вышестоящий роутер. Обратные маршруты добавлены
```
- Все сервера должны видеть друг друга
```
Сделано. Маршруты добавлены
```
- у всех новых серверов отключить дефолт на нат (eth0), который вагрант поднимает для связи
```
Отключено
```
- при нехватке сетевых интерфейсов добавить по несколько адресов на интерфейс
```
Интерфейсов хватило
```



