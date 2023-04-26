# Insights on this Section Course
### Creating Controllers:
`namespace`
  - Allows to use the same names or class name in different part of application.

```php
namespace App\Http\function1;
namespace App\Http\function2;
```
`use`
  - to import specific class or namespace to this file.

###### Display help commands in laravel.
```php
php artisan
```
###### Creating a controller in terminal
```php
php artisan make:controller PostsController
```
###### Creating a controller with resource in terminal
```php
php artisan make:controller --resource ResourcePostsController
```
### Routing Controllers:
```php
Route::get('post', [ResourcePostsController::class, 'index']);
```
###### another way by prepending the controller name with full namespace path
```php
Route::get('post', 'App\Http\Controllers\ResourcePostsController@index');
```
### Passing parameters into Controller:
```php
Route::get('post/{id}', [ResourcePostsController::class, 'index']);
```
###### on ResourcePostsController inside index function
```php
public function index($id)
{
    //

    return "Hello World!" . $id;
}
```
### Resource:
- Gives access automatically to different types of routes.

```php
Route::resource('posts', ResourcePostsController::class);
```
