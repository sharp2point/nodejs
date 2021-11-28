

Пример запуска FlutterWeb приложения на nodejs/express платформе.

инструменты:
  node.js
  express.js
  express-handlebars.js 
  pm2
  flutter web
  NGINX

За запуск сервера отвечает файл index.js сервер стартует на порту 3000 коммандой pm2 start index.js

Приложение Flutter лежит в папке public/flutter, встраивается в шаблон main.handlebars с помощью iframe: <iframe src="/flutter/index.html"></iframe>

Пример настройки сервера NGINX:

  server {
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
