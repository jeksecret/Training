# Insights on this Section
### Laravel Structure Overview:
`config folder`
- Where the configuration files are located.

`database folder`
1. migrations folder
    - Where the created tables are located for migration into database.
2. factories and seeds folder
    - Where factories and seeds folder are located.
    
`public folder`
- Where public files will be located _(e.g. css, js, index.php, htaccess for security)_.
1. resources folder
    - Where the files that need to be compiled are here using **webpack** configuration.
2. view folder
    - Where the html part is located _(e.g ContactPage)_.

`routes folder`
- Where the route files are located.

`.env file`
- Where the sensitive information is stored _(e.g. connecting to database)._
### Route Introduction:
###### Creating a route
```php
Route::get('/', function () {
    return view('welcome');
});
```
###### Passing parameters to a route
```php
Route::get('/users/{id}/{name}', function ($id, $name) {
    return "This is user " . $id . ", " . $name;
});
```
###### Naming a route
```php
Route::get('admin/posts/example', function () {
    $url = route('admin.home');

    return "This url is " . $url;
})->name('admin.home');
```
###### href example
`e.g. <a href="{{ route('admin.home') }}">Click</a>`
