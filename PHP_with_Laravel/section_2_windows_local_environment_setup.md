# Insights on this Section
### Setting up Tools:
- Download `XAMPP` installer for PHP and install.
- Download `Git` installer and install.
- Download `Composer` installer for creating a project in laravel and install.
- Download `Visual Studio Code` installer for code editor and install.
- Download Node.js installer and install.

###### command
```
php -v
```
`php -v` - _displays the php version_.
### Using MySQL through command line:
```
C:\xampp\mysql\bin\mysql -uroot -p
show databases;
create database "dbname";
use "dbname";
```
`C:\xampp\mysql\bin\mysql -uroot -p` - _Logged in through command line_.

`show databases;` - _Displays databases in command line_.

`create database;` - _Create a database through command line_.

`use;` - _Use the created database_.

### Installing Laravel:
```
composer create-project laravel/laravel "project-name"
php artisan serve
```
`composer create-project laravel/laravel` - _Create a new laravel project via the Composer command_.

`php artisan serve` - _Run applications on the PHP development server.
