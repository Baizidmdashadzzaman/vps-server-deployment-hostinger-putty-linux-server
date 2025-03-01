nano /etc/nginx/sites-available/belivo.io.conf

 server {
    listen 80;
    server_name belivo.io www.belivo.io;

    location / {
        root /var/www/Bellivo_1.0/Bellivo/Bellivo-Web-App/dist;
        try_files $uri /index.html;
    }
}




nano /etc/nginx/sites-available/admin.belivo.io.conf

 server {
    listen 80;
    server_name admin.belivo.io www.admin.belivo.io;

    location / {
        root /var/www/Bellivo_1.0/Bellivo/Bellivo-Admin-Dashboard/build;
        try_files $uri /index.html;
    }
}

ln -s /etc/nginx/sites-available/belivo.io.conf /etc/nginx/sites-enabled/
ln -s /etc/nginx/sites-available/admin.belivo.io.conf /etc/nginx/sites-enabled/


nano /etc/nginx/sites-available/api.belivo.io.conf


server {
    listen 80;
    server_name api.belivo.io;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

ln -s /etc/nginx/sites-available/api.belivo.io.conf /etc/nginx/sites-enabled/


certbot --nginx -d belivo.io -d www.belivo.io -d admin.belivo.io -d api.belivo.io



nano /etc/nginx/sites-available/web.belivo.io.conf

server {
    listen 80;
    server_name web.belivo.io www.web.belivo.io;

    location / {
        root /var/www/Bellivo_1.0/Bellivo/Bellivo-Web-App/dist;
        try_files $uri /index.html;
    }
}

ln -s /etc/nginx/sites-available/web.belivo.io.conf /etc/nginx/sites-enabled/


certbot --nginx -d web.belivo.io

certbot renew --dry-run


