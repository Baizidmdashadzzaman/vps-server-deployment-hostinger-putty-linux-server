nano /etc/nginx/sites-available/admin.bellivo.dk.conf

server {
    listen 80;
    server_name admin.bellivo.dk www.admin.bellivo.dk;

    location / {
        root /var/www/Bellivo_1.0/Bellivo/Bellivo-Admin-Dashboard/build;
        try_files $uri /index.html;
    }
}

ln -s /etc/nginx/sites-available/admin.bellivo.dk.conf /etc/nginx/sites-enabled/

systemctl restart nginx


nano /etc/nginx/sites-available/web.bellivo.dk.conf

server {
    listen 80;
    server_name web.bellivo.dk www.web.bellivo.dk;

    location / {
        root /var/www/Bellivo_1.0/Bellivo/Bellivo-Web-App/dist;
        try_files $uri /index.html;
    }
}

ln -s /etc/nginx/sites-available/web.bellivo.dk.conf /etc/nginx/sites-enabled/

systemctl restart nginx


nano /etc/nginx/sites-available/api.bellivo.dk.conf

server {
    listen 80;
    server_name api.bellivo.dk;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

ln -s /etc/nginx/sites-available/api.bellivo.dk.conf /etc/nginx/sites-enabled/

systemctl restart nginx


nano /etc/nginx/sites-available/bellivo.dk.conf


sudo certbot --nginx -d web.bellivo.dk