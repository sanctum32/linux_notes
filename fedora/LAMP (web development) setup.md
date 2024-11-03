Last update: 2024 august 27th

# INTRO

Before starting to use any of commands, please make extra settings, scripts and other important backups.

Also while making these notes, I (sanctum32) used official repositories and packages provided in default fedora repositories. Copr repository was not used

## Apache setup
***
    
```
sudo dnf install httpd
sudo systemctl enable httpd.service\
sudo systemctl start httpd.service
sudo systemctl status httpd.service
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo systemctl reload firewalld
```

## MariaDB setup
***

```
sudo dnf install mariadb-server
sudo systemctl enable mariadb.service
sudo systemctl start mariadb.service
sudo systemctl status mariadb.service
sudo mysql_secure_installation # tool configures mariadb via guided questions
```

## PHP setup
***

-- Packages to install:

```
sudo dnf install php php-common php-cli phpunit php-intl php-bcmath
```

Optional packages (common):
<ul>
    <li>php-bcmath       # A module for PHP applications for using the bcmath library</li>
    <li>php-dbg          # The interactive PHP debugger</li>
    <li>php-gd           # A module for PHP applications for using the gd graphics library</li>
    <li>php-mbstring     # A module for PHP applications which need multi-byte string handling</li>
    <li>php-pecl-xdebug3 # Provides functions for function traces and profiling</li>
    <li>php-pecl-pcov    # A self contained CodeCoverage compatible driver for PHP</li>
    <li>php-pecl-imagick # Provides a wrapper to the ImageMagick library</li>
    <li>php-pecl-apcu    # APC User Cache</li>
    <li>php-fpm          # FastCGI Process Manager</li>
    <li>php-xml          # XML support</li>
    <li>php-twig         # The flexible, fast, and secure template engine for PHP</li>
    <li>php-pdo          # A database access abstraction module for PHP applications</li>
    <li>php-odbc         # A module for PHP applications that use ODBC databases</li>
    <li>php-mysqlnd      # A module for PHP applications that use MySQL databases</li>
    <li>php-oauth        # PHP Authentication library for desktop to web applications</li>
    <li>phpunit          # The PHP Unit Testing framework version (package name may could be different)</li>
    <li>php-soap         # A module for PHP applications that use the SOAP protocol</li>
</ul>

More packages could be found by using command (without quates) "dnf search php-*"

This command will install listed optional packages (feel free to edit and add or remove package names in this command ("sudo dnf install " must be kept and packages should be sperated with space in syntax)

```
sudo dnf install php-bcmath php-dbg php-gd php-mbstring php-pecl-xdebug3 php-pecl-pcov php-pecl-imagick php-pecl-apcu php-fpm php-xml \
    php-twig php-pdo php-odbc php-mysqlnd php-oauth phpunit php-soap
```

## Optional additional software:
* composer         # Dependency Manager for PHP

-- after php install, do apache restart

```
sudo systemctl restart httpd
```

## Script to test php (remove script after test)

```
sudo vi /var/www/html/info.php # or sudo nano /var/www/html/info.php
```

info.php script text(without quates):
```php
    "<?php phpinfo(); ?>"
```

## Apache user permissions:
By default in fedora, apache http server uses "apache" user, some website scripts may can encounter issues and related permissions may should be set for "apache" user

```
sudo chown -R apache:apache /var/www/html
```

## File permissions
https://www.redhat.com/en/blog/linux-file-permissions-explained <- more information
-> change /var/www/html to your web path if different www directory than default is used

```
sudo find /var/www/html -type d -exec chmod 755 {} \; # for directories
sudo find /var/www/html -type f -exec chmod 644 {} \; # for files
```

If SELINUX is enabled 
-> change /var/www/html to your web path if different www directory than default is used

```
chcon -R -t httpd_sys_rw_content_t /var/www/html
chcon -R -t httpd_sys_rw_content_t /var/www/html
```

## Fedora docs

Tip: do not skip sections in official fedora docs! These articles has important information which is required for final secure apache http setup!
-----------------------------
<a href="https://docs.fedoraproject.org/en-US/quick-docs/getting-started-with-apache-http-server">Fedora docs - getting started with apache httpd server</a>
<a href="https://fedoraproject.org/wiki/Administration_Guide_Draft/Permissions">Fedora docs - managing file permissions</a>


