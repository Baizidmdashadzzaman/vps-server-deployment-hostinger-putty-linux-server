```bash
sudo apt install -y nginx
```
```bash
sudo ufw enable
```
```bash
sudo ufw status
```
```bash
sudo ufw allow 'Nginx Full'
```

To configure this on your VPS server, you can use Nginx or Apache as the web server. Here's a step-by-step guide using Nginx (a common choice for such tasks):

1. Ensure DNS Configuration
Update your DNS records to point the subdomains to your server's IP:
belivo.io -> <server IP>
admin.belivo.io -> <server IP>
api.belivo.io -> <server IP>

2. Install and Configure Nginx
If Nginx is not installed on your server, install it:

```bash
sudo apt update
```
```bash
sudo apt install nginx
```

3. Configure Nginx for Your Subdomains
Create a configuration file for each domain in /etc/nginx/sites-available.

Configuration for belivo.io
File: 
```bash
nano /etc/nginx/sites-available/belivo.io
```

```bash
server {
    listen 80;
    server_name belivo.io www.belivo.io;

    location / {
        proxy_pass http://localhost:5173;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

Configuration for admin.belivo.io
```bash
nano /etc/nginx/sites-available/admin.belivo.io
```

```bash
server {
    listen 80;
    server_name admin.belivo.io;

    location / {
        proxy_pass http://localhost:4000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

Configuration for api.belivo.io
```bash
nano /etc/nginx/sites-available/api.belivo.io
```

```bash
server {
    listen 80;
    server_name api.belivo.io;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

4. Enable the Configurations
Create symbolic links in /etc/nginx/sites-enabled for each configuration:

```bash
sudo ln -s /etc/nginx/sites-available/belivo.io /etc/nginx/sites-enabled/
```
```bash
sudo ln -s /etc/nginx/sites-available/admin.belivo.io /etc/nginx/sites-enabled/
```
```bash
sudo ln -s /etc/nginx/sites-available/api.belivo.io /etc/nginx/sites-enabled/
```

5. Test Nginx Configuration
Check for syntax errors in the configuration files:

```bash
sudo nginx -t
```

If no errors are reported, reload Nginx:

```bash
sudo systemctl reload nginx
```

6. Optional: Configure HTTPS
Install a Let's Encrypt SSL certificate for your domains using certbot:

bash
```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d belivo.io -d www.belivo.io -d admin.belivo.io -d api.belivo.io
```
Follow the prompts to set up HTTPS.

