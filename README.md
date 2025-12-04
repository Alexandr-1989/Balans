Задание 1
Запустите два simple python сервера на своей виртуальной машине на разных портах
Установите и настройте HAProxy, воспользуйтесь материалами к лекции по ссылке
Настройте балансировку Round-robin на 4 уровне.
На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy.

Решение

haproxy.cfg

```
global
        log /dev/log    local0                                                                       
        log /dev/log    local1 notice
        chroot /var/lib/haproxy                                                                      
        stats socket /run/haproxy/admin.sock mode 660 level admin
        stats timeout 30s                                                                            
        user haproxy
        group haproxy                                                                                
        daemon
                                                                                                     
        # Default SSL material locations
        ca-base /etc/ssl/certs                                                                       
        crt-base /etc/ssl/private
                                                                                                     
        # See: https://ssl-config.mozilla.org/
        #server=haproxy&server-version=2.0.3&config=intermedia>
        ssl-default-bind-ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECD>
        ssl-default-bind-ciphersuites TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POL>
        ssl-default-bind-options ssl-min-ver TLSv1.2 no-tls-tickets                                  

defaults                                                                                             
        log     global
        mode    http                                                                                 
        #option httplog
        option  dontlognull
        timeout connect 5s
        timeout client  50s
        timeout server  50s
        errorfile 400 /etc/haproxy/errors/400.http
        errorfile 403 /etc/haproxy/errors/403.http
        errorfile 408 /etc/haproxy/errors/408.http
        errorfile 500 /etc/haproxy/errors/500.http
        errorfile 502 /etc/haproxy/errors/502.http
        errorfile 503 /etc/haproxy/errors/503.http
        errorfile 504 /etc/haproxy/errors/504.http

listen stats  #
        bind *:888
        mode http
        option httplog
         stats enable                                                                                 
        stats uri /stats
        stats refresh 5s                                                                              
        stats realm Haproxy\ Statistics
        
frontend example                                                                        
        mode http
        bind :8088                                                                                    
        option httplog
        default_backend web_servers                                                                   
        #acl ACL_example.com hdr(host) -i example.com
        #use_backend web_servers if ACL_example.com                                                   

backend web_servers    
        mode http
        balance roundrobin
        option httpchk
        http-check send meth GET uri /index.html
        server s1 127.0.0.1:8888 check
        server s2 127.0.0.1:9999 check

listen web_tcp
        mode tcp
        bind *:1325
        balance roundrobin
        option tcplog
        server s1 127.0.0.1:8888 check inter 3s
        server s2 127.0.0.1:9999 check inter 3s
```
<img width="509" height="310" alt="Screenshot_11" src="https://github.com/user-attachments/assets/af8a2121-198e-4180-8493-0d8fbcfaa8c9" />
<img width="3159" height="778" alt="Screenshot_12" src="https://github.com/user-attachments/assets/1d93142c-6444-4454-b761-808036ae0076" />

Задание 2
Запустите три simple python сервера на своей виртуальной машине на разных портах
Настройте балансировку Weighted Round Robin на 7 уровне, чтобы первый сервер имел вес 2, второй - 3, а третий - 4
HAproxy должен балансировать только тот http-трафик, который адресован домену example.local
На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy c использованием домена example.local и без него.

Решение

haproxy.cfg
```
global
        log /dev/log    local0
        log /dev/log    local1 notice
        chroot /var/lib/haproxy
        stats socket /run/haproxy/admin.sock mode 660 level admin
        stats timeout 30s
        user haproxy
        group haproxy
        daemon

        # Default SSL material locations
        ca-base /etc/ssl/certs
        crt-base /etc/ssl/private

        # See: https://ssl-config.mozilla.org/#server=haproxy&server-version=2.0.3&config=intermedia>
        ssl-default-bind-ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECD>
        ssl-default-bind-ciphersuites TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POL>
        ssl-default-bind-options ssl-min-ver TLSv1.2 no-tls-tickets

defaults
        log     global
        mode    http
        option  httplog
        option  dontlognull
        timeout connect 5s
        timeout client  50s
        timeout server  50s
        errorfile 400 /etc/haproxy/errors/400.http
        errorfile 403 /etc/haproxy/errors/403.http
        errorfile 408 /etc/haproxy/errors/408.http
        errorfile 500 /etc/haproxy/errors/500.http
        errorfile 502 /etc/haproxy/errors/502.http
        errorfile 503 /etc/haproxy/errors/503.http
        errorfile 504 /etc/haproxy/errors/504.http

listen stats   
        bind *:888
        mode http
        option httplog
        stats enable
        stats uri /stats
        stats refresh 5s
        stats realm Haproxy\ Statistics
        #stats auth admin:admin

frontend example   
        mode http
        bind :8088
        option httplog
        acl ACL_example hdr_beg(host) -i example.local
        use_backend web_cluster if ACL_example
        default_backend reject_all

backend web_cluster # backend for example.local
        mode http
        balance roundrobin
        ### Weighted Round Robin ###
        server s1 127.0.0.1:8888 weight 2 check
        server s2 127.0.0.1:9999 weight 3 check
        server s3 127.0.0.1:7777 weight 4 check

backend reject_all # backend by default
        mode http
        http-request deny deny_status 403
```
<img width="552" height="527" alt="Screenshot_13" src="https://github.com/user-attachments/assets/733b2c87-0ff8-4fc3-85ac-afa74edd724d" />
<img width="3160" height="668" alt="Screenshot_14" src="https://github.com/user-attachments/assets/11fd349d-13af-4f35-982e-d2104f340b02" />
