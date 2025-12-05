Задание 1
Запустите два simple python сервера на своей виртуальной машине на разных портах
Установите и настройте HAProxy, воспользуйтесь материалами к лекции по ссылке
Настройте балансировку Round-robin на 4 уровне.
На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy.

Решение

[haproxy.cfg](https://github.com/Alexandr-1989/Balans/blob/main/files/haproxy_1.cfg)


<img width="509" height="310" alt="Screenshot_11" src="https://github.com/user-attachments/assets/af8a2121-198e-4180-8493-0d8fbcfaa8c9" />
<img width="3159" height="778" alt="Screenshot_12" src="https://github.com/user-attachments/assets/1d93142c-6444-4454-b761-808036ae0076" />

Задание 2
Запустите три simple python сервера на своей виртуальной машине на разных портах
Настройте балансировку Weighted Round Robin на 7 уровне, чтобы первый сервер имел вес 2, второй - 3, а третий - 4
HAproxy должен балансировать только тот http-трафик, который адресован домену example.local
На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy c использованием домена example.local и без него.

Решение

[haproxy.cfg](https://github.com/Alexandr-1989/Balans/blob/main/files/haproxy_2.cfg)

<img width="552" height="527" alt="Screenshot_13" src="https://github.com/user-attachments/assets/733b2c87-0ff8-4fc3-85ac-afa74edd724d" />
<img width="3160" height="668" alt="Screenshot_14" src="https://github.com/user-attachments/assets/11fd349d-13af-4f35-982e-d2104f340b02" />
