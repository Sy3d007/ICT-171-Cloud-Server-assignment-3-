# Web Server Setup

## System Update

Before installing anything, update the package list and upgrade existing packages:

```bash
sudo apt update && sudo apt upgrade -y
```

## LAMP Stack Installation

WordPress requires a LAMP stack Linux, Apache, MySQL, and PHP.

### Apache

Apache was chosen over Nginx for better native WordPress compatibility, particularly for URL rewriting via .htaccess. It is also unaffected by CVE-2026-42945 which impacts Nginx servers.

Install Apache:

```bash
sudo apt install apache2 -y
```

Verify Apache is running:

```bash
sudo systemctl status apache2
```

Confirm by visiting `http://20.213.8.117` in a browser the default Ubuntu Apache page should appear.

### MySQL

MySQL stores all WordPress data including posts, users, and settings:

```bash
sudo apt install mysql-server -y
```

Secure the MySQL installation:

```bash
sudo mysql_secure_installation
```

When prompted:
- VALIDATE PASSWORD component → `n`
- Remove anonymous users → `y`
- Disallow root login remotely → `y`
- Remove test database → `y`
- Reload privilege tables → `y`

### PHP

PHP is the programming language WordPress is built on:

```bash
sudo apt install php libapache2-mod-php php-mysql -y
```

Verify PHP installed correctly:

```bash
php -v
```

Expected output: `PHP 8.3.x`

## Database Setup

Log into MySQL:

```bash
sudo mysql
```

Create a database and user for WordPress:

```sql
CREATE DATABASE wordpress_db;
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'your_password_here';
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wp_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

## WordPress Installation

Download and extract WordPress:

```bash
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar -xvzf latest.tar.gz
sudo mv wordpress /var/www/html/
```

Set correct permissions so Apache can serve the files:

```bash
sudo chown -R www-data:www-data /var/www/html/wordpress
sudo chmod -R 755 /var/www/html/wordpress
```

## Apache Configuration

Create a new Apache config file for WordPress:

```bash
sudo nano /etc/apache2/sites-available/wordpress.conf
```

Add the following:

```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/wordpress
    ServerName 20.213.8.117

    <Directory /var/www/html/wordpress>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Enable the site and restart Apache:

```bash
sudo a2ensite wordpress.conf
sudo a2enmod rewrite
sudo a2dissite 000-default.conf
sudo systemctl restart apache2
```
