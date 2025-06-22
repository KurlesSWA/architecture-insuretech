## Задание 6

Для реализации Rate Limiter'а будем использовать модуль nginx 
[ngx_http_limit_req_module](https://nginx.org/en/docs/http/ngx_http_limit_req_module.html)

Доработанная конфигурация:

```nginx
http {
    # Настройка лимита запросов - 10 запросов в минуту
    limit_req_zone $binary_remote_addr zone=one:10m rate=10r/m;

    # Настройка upstream для балансировки нагрузки
    upstream backend_servers {
        server backend1.example.com;
        server backend2.example.com;
        server backend3.example.com;
    }

    server {
        listen 80;

        location / {
            # Применяем ограничение запросов
            limit_req zone=one burst=5 nodelay;
            # Устанавливаем код ошибки при превышении лимита
            limit_req_status 429;
            
            proxy_pass http://backend_servers;
        }
    }
}
```

[Ссылка](nginx.conf) на файл конфигурации.