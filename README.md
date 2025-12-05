Задание 1
Запустите два simple python сервера на своей виртуальной машине на разных портах
Установите и настройте HAProxy, воспользуйтесь материалами к лекции по ссылке
Настройте балансировку Round-robin на 4 уровне.
На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy.

Решение

[haproxy.cfg](https://github.com/Alexandr-1989/Balans/blob/main/files/haproxy_1.cfg)

<img width="418" height="402" alt="Screenshot_6" src="https://github.com/user-attachments/assets/7f0fc0ea-ef36-421c-bdcc-0f8dda2dbb97" />
<img width="3154" height="677" alt="Screenshot_5" src="https://github.com/user-attachments/assets/2cd57a4b-d608-4876-ae2a-512ea248af80" />





Задание 2
Запустите три simple python сервера на своей виртуальной машине на разных портах
Настройте балансировку Weighted Round Robin на 7 уровне, чтобы первый сервер имел вес 2, второй - 3, а третий - 4
HAproxy должен балансировать только тот http-трафик, который адресован домену example.local
На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy c использованием домена example.local и без него.

Решение

[haproxy.cfg](https://github.com/Alexandr-1989/Balans/blob/main/files/haproxy_2.cfg)

<img width="452" height="802" alt="2" src="https://github.com/user-attachments/assets/cdeacef2-10dd-40f0-ba98-32997fb50b00" />
<img width="3104" height="689" alt="stats2" src="https://github.com/user-attachments/assets/f5d3acf3-7f59-4361-ab95-ce02b8c2cc98" />

