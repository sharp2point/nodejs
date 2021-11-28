

# Пример запуска FlutterWeb приложения на nodejs/express платформе.

## Инструменты:
  * node.js,
  * express.js,
  * express-handlebars.js, 
  * pm2,
  * flutter web,
  * NGINX,

## Запуск:

За запуск сервера отвечает файл index.js сервер стартует на порту 3000 коммандой:  ***_pm2 start index.js_***

Приложение Flutter лежит в папке public/flutter, встраивается в шаблон main.handlebars с помощью iframe: ***_<iframe src="/flutter/index.html"></iframe>_***

## Пример настройки сервера NGINX:



 server{
 
          listen 80;
          
          server_name you_server_name;

          root /home/sharp/apps/nodejs;


          location /  {
                  proxy_pass    http://localhost:3000;
                  proxy_http_version 1.1;
                  proxy_set_header Upgrade $http_upgrade;
                  proxy_set_header Connection 'upgrade';
                  proxy_set_header Host $host;
                  proxy_cache_bypass $http_upgrade;
          }
  }
