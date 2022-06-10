FROM nginx:1.15.0-alpine

#Remove o arquivo .conf padrão do neginx, e copia o meu
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d

#cria um arquivo index.php, mesmo que Não faça nada, pq senão vai dar error 404
RUN mkdir /var/www/html -p && touch /var/www/html/index.php
