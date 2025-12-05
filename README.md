Задание 1
Запустите два simple python сервера на своей виртуальной машине на разных портах
Установите и настройте HAProxy, воспользуйтесь материалами к лекции по ссылке
Настройте балансировку Round-robin на 4 уровне.
На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy.

Решение

[haproxy.cfg](https://github.com/Alexandr-1989/Balans/blob/main/files/haproxy_1.cfg)

<img width="475" height="346" alt="1" src="https://github.com/user-attachments/assets/d738b2df-9163-4575-8368-191120063422" />
<img width="3114" height="793" alt="stats1" src="https://github.com/user-attachments/assets/bba831fa-55d8-42e3-8b86-51242cdde529" />


Задание 2
Запустите три simple python сервера на своей виртуальной машине на разных портах
Настройте балансировку Weighted Round Robin на 7 уровне, чтобы первый сервер имел вес 2, второй - 3, а третий - 4
HAproxy должен балансировать только тот http-трафик, который адресован домену example.local
На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy c использованием домена example.local и без него.

Решение

[haproxy.cfg](https://github.com/Alexandr-1989/Balans/blob/main/files/haproxy_2.cfg)

<img width="452" height="802" alt="2" src="https://github.com/user-attachments/assets/cdeacef2-10dd-40f0-ba98-32997fb50b00" />
<img width="3104" height="689" alt="stats2" src="https://github.com/user-attachments/assets/f5d3acf3-7f59-4361-ab95-ce02b8c2cc98" />

