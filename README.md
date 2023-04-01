# D3.4_praktik
Minikube, kubectl, auth-basic, secret, configmap, Deployment <br>
<h2>Задание</h2>
1) Создать Deployment со свойствами ниже: <br>
- образ — nginx:1.21.1-alpine; <br>
- имя — nginx-sf; <br>
- количество реплик — 3. <br>
<b> Ресультат: </b><br>
<img src="https://github.com/Suirus777/D3.4_praktik/blob/main/screens/kubctl%20get%20all.JPG"> 
2) Создать конфигурационный файл для нашего приложения и поместить его в наш Pod со следующими свойствами: <br>
- путь до файла в Pod’е — /etc/nginx/nginx.conf; <br>
- содержимое файла: <br><br>
<code> user nginx;
- worker_processes  1;
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
} </code> <br>
<b> Ресультат: </b><br>
Можно посмотреть в https://github.com/Suirus777/D3.4_praktik/blob/main/configmap.yaml  <br><br>
3) Создать service для того, чтобы можно было обращаться к любому из Pod’ов по единому имени: <br>
- имя сервиса sf-webserver;<br>
- внешний порт — 80.<br>
- Создать секрет со следующими данными:<br>
- имя секрета — auth_basic;<br>
- ключ объекта в секрете — user1;<br>
- значение объекта в секрете user1 — password1;<br>
- Подключить в наш контейнер эти секреты.<br>
<b> Ресультат: </b><br>
<img src="https://github.com/Suirus777/D3.4_praktik/blob/main/screens/kubctl%20get%20all.JPG">
<img src="https://github.com/Suirus777/D3.4_praktik/blob/main/screens/kubctl%20get%20secrets.JPG">
Настройки для секретов хранятся в: https://github.com/Suirus777/D3.4_praktik/blob/main/secret.yaml <br> <br> 
4) Обновить конфиг nginx таким образом, чтобы подключенные секреты использовались для авторизации для доступа к странице по умолчанию в nginx. <br>  
<b> Ресультат: </b><br>
Был создан новый Volume: <br>
<code>         volumeMounts:
        - name: auth-basic
          mountPath: "/etc/nginx/conf.d/.htpasswd"
          readOnly: true </code> <br>
И <br>
<code>      - name: auth-basic
              secret:
              secretName: auth-basic  </code> <br>
Полный настройки можно посмотреть в: https://github.com/Suirus777/D3.4_praktik/blob/main/nginx.yaml <br>
