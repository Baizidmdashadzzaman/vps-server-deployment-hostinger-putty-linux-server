# Laravel Deployment on Hostinger VPS using XAMPP

## Prerequisites
- Hostinger VPS with SSH access
- XAMPP installed on the VPS
- Laravel project ready for deployment
- Domain configured (optional)

## 1. Connect to VPS via SSH
```sh
ssh user@your-vps-ip
```

## 2. Update System
```sh
sudo apt update && sudo apt upgrade -y
```

## 3. Install XAMPP (if not installed)
```sh
wget https://www.apachefriends.org/xampp-files/8.2.4/xampp-linux-x64-8.2.4-0-installer.run
sudo chmod +x xampp-linux-x64-8.2.4-0-installer.run
sudo ./xampp-linux-x64-8.2.4-0-installer.run
sudo /opt/lampp/lampp start
```

## 4. Upload Laravel Project
Use SCP or FTP:
```sh
scp -r your-laravel-project user@your-vps-ip:/opt/lampp/htdocs/
```

## 5. Set Permissions
```sh
cd /opt/lampp/htdocs/your-laravel-project
sudo chmod -R 775 storage bootstrap/cache
sudo chown -R www-data:www-data storage bootstrap/cache
```

## 6. Configure Database
Edit `.env` file:
```sh
nano .env
```
Set database details:
```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=your_db_name
DB_USERNAME=root
DB_PASSWORD=
```
Run migrations:
```sh
php artisan migrate --force
```

## 7. Set Up Apache Virtual Host
```sh
sudo nano /etc/apache2/sites-available/laravel.conf
```
Add:
```
<VirtualHost *:80>
    ServerAdmin admin@yourdomain.com
    DocumentRoot "/opt/lampp/htdocs/your-laravel-project/public"
    ServerName yourdomain.com
    <Directory "/opt/lampp/htdocs/your-laravel-project">
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Enable the site and restart Apache:
```sh
sudo a2ensite laravel.conf
sudo systemctl restart apache2
```

## 8. Generate Application Key
```sh
php artisan key:generate
```

## 9. Set Up Cron Jobs (if needed)
```sh
crontab -e
```
Add:
```
* * * * * php /opt/lampp/htdocs/your-laravel-project/artisan schedule:run >> /dev/null 2>&1
```

## 10. Configure Firewall
```sh
sudo ufw allow OpenSSH
sudo ufw allow 'Apache Full'
sudo ufw enable
```

## 11. Access Your Site
Visit: `http://yourdomain.com` or `http://your-vps-ip`
