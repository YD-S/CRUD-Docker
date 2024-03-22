FROM nginx:latest

ENV BACKEND_HOST=backend
ENV BACKEND_PORT=your_backend_port

RUN apt-get update && apt-get install -y \
	curl git

RUN echo "worker_processes 1;" > /etc/nginx/nginx.conf && \
    echo "events { worker_connections 1024; }" >> /etc/nginx/nginx.conf && \
    echo "http {" >> /etc/nginx/nginx.conf && \
    echo "    server {" >> /etc/nginx/nginx.conf && \
    echo "        listen 80;" >> /etc/nginx/nginx.conf && \
    echo "        location / {" >> /etc/nginx/nginx.conf && \
    echo "            root /usr/share/nginx/html;" >> /etc/nginx/nginx.conf && \
    echo "            index index.html;" >> /etc/nginx/nginx.conf && \
    echo "        }" >> /etc/nginx/nginx.conf && \
    echo "        location /api {" >> /etc/nginx/nginx.conf && \
    echo "            proxy_pass http://\$BACKEND_HOST:\$BACKEND_PORT;" >> /etc/nginx/nginx.conf && \
    echo "            proxy_set_header Host \$host;" >> /etc/nginx/nginx.conf && \
    echo "            proxy_set_header X-Real-IP \$remote_addr;" >> /etc/nginx/nginx.conf && \
    echo "            proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;" >> /etc/nginx/nginx.conf && \
    echo "            proxy_set_header X-Forwarded-Proto \$scheme;" >> /etc/nginx/nginx.conf && \
    echo "        }" >> /etc/nginx/nginx.conf && \
    echo "    }" >> /etc/nginx/nginx.conf && \
    echo "}" >> /etc/nginx/nginx.conf

RUN git clone https://github.com/YD-S/CRUD.git /app

RUN cd /app

RUN git checkout frontend

RUN npm run build

RUN cp -r /app/dist/* /usr/share/nginx/html

EXPOSE 80

# Start Nginx
RUN nginx -g 'daemon off;'
