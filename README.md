# D3.4_praktik
Minikube, kubectl, auth-basic, secret, configmap, Deployment <br>
<h2>Задание</h2>
1) Создать Deployment со свойствами ниже: <br>
- образ — nginx:1.21.1-alpine; <br>
- имя — nginx-sf; <br>
- количество реплик — 3. <br>
<b> Ресультат: </b><br>

Создать конфигурационный файл для нашего приложения и поместить его в наш Pod со следующими свойствами:
путь до файла в Pod’е — /etc/nginx/nginx.conf;
содержимое файла:
user nginx;
worker_processes  1;
events {
  worker_connections  10240;
}
http {
  server {
      listen       80;
      server_name  localhost;
      location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }
  }
}
Создать service для того, чтобы можно было обращаться к любому из Pod’ов по единому имени:
имя сервиса sf-webserver;
внешний порт — 80.
Создать секрет со следующими данными:
имя секрета — auth_basic;
ключ объекта в секрете — user1;
значение объекта в секрете user1 — password1;
Подключить в наш контейнер эти секреты.
Обновить конфиг nginx таким образом, чтобы подключенные секреты использовались для авторизации для доступа к странице по умолчанию в nginx.
