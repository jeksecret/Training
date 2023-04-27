# Insights on this Section Course
`.env file`
- Where you store the sensitive credentials in your code.

###### Migrations:
```php
php artisan migrate
```
###### Create and dropping migrations:
```php
php artisan make:migration create_posts_table --create=posts
```
###### Adding columns to existing table:
```php
php artisan make:migration add_is_admin_column_to_posts_table --table=posts
```
###### Some more migration commands:
```php
php artisan migrate:rollback
php artisan migrate:refresh
php column amigrate:reset
```

#### Schema Builder Link:

https://laravel.com/docs/5.0/schema
