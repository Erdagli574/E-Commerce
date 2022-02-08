## Introduction
Hi! This project implements an E-Commerce shopping system where people can view items from various shops, order items, and review products based on their delivery experience. The system planned to be used by three user types:
- **_Customers_** who will make the ordering and reviewing processes.
- **_Stores_** who can make orders, manage and display data related to the received orders, make modifications on shop items, etc.
- **_Admin_** who will be in charge of all processes and website activities.

## Outline
1. Laravel Project Setup on Linux
2. Laravel Project Setup on Windows
3. DB E-R Diagram

## Project Setup on Linux
(_Assuming you installed **Php**, **Apache**, and **MySQL Server** to your machine._)
> Clone the project under <samp>/var/www</samp> directory.
```
$ git clone git@github.com:Erdagli574/E-Commerce.git
```
> Check **composer.json** file in the project directory to see if the php version of the project and your machine are the same.
```
$ php -v
```
> Create the .env file from .env.example file by running the below command on the project path, and enter the database and other necessary information.
```
cp .env.example .env
```
> Run the below command on the project path to install vendor files.
```
$ composer install
```
> Run the below commands on the project path to change owner.
```
$ sudo chmod -R 775 .
```
```
$ sudo chown -R www-data:<USER_NAME> .
```
> Run migrations to create DB tables.
```
$ php artisan migrate
```
> Run below command on the project path to start the project or skip this part and check **Creating Symbolic Link** section to create a shortcut.
```
$ php artisan serve
```
#### Creating Symbolic Link
> Create a symbolic link by running the below command.
```
$ ln -s /var/www/<PROJECT_DIRECTORY_NAME>/public /var/www/html/ecommerce
```
> Open the **hosts** file in **etc** directroy.
```
$ sudo nano /etc/hosts 
```
> Add the below line to the file and save it. Note that you can write anything instead of **_ecommerce.test_**.
```
127.0.0.1   ecommerce.test
```
> Run the below command to create a .conf file. Note that you can give a different name to your .conf file.
```
$ sudo nano /etc/apache2/sites-available/ecommerce.conf
```
> Add the below lines to the .conf file.
```
<VirtualHost *:80>
        ServerName ecommerce.test

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html/ecommerce

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        <FilesMatch \.php>
            # Apache 2.4.10+ can proxy to unix socket 
            SetHandler "proxy:unix:/var/run/php/php7.3-fpm.sock|fcgi://localhost/"
        </FilesMatch>

</VirtualHost>
```
> Enable it.
```
$ a2ensite ecommerce.conf 
```
> Restart your apache server.
```
$ sudo service apache2 reload
```
> Now go to your browser and enter the servername (for our example it is **_ecommerce.test_**) to the search area to start the project.

## Project Setup on Windows
(_Assuming you installed **Xampp** to your machine._)
> Run **Xampp** and start **Apache** and **MySQL** servers
> Go to the **Xampp** file location and open the **htdocs** folder. Then run the command prompt on the **htdoc** folder path and run below command to clone the project.
```
> git clone git@github.com:Erdagli574/E-Commerce.git
```
> Open the project folder and copy and rename the **.env.example** file as **.env**. Then open the .env file and enter the database and other necessary information.
> Run the below command to install vendor files and packages.
```
> composer install
```
> Run migrations to create DB tables.
```
> php artisan migrate
```
> Then start the project by running the below command.
```
> php artisan serve
```
> Now open your browser and go to the below address.
```
http://127.0.0.1:8000
```

## DB E-R Diagram
![DB-diagram for Ecommerce](https://user-images.githubusercontent.com/70316787/153058809-8e7085ef-14c3-4f6e-8be0-6d64627a103f.png)
