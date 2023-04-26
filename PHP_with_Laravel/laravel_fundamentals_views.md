# Insights on this Section Course
### Blade Template:
- Blade is a templating engine that is used in Laravel framework.

### Creating views and custom method:

##### Inside `views folder` create a file by naming it `contact.blade.php`

###### Create a custom contact method in PostsController
```php
public function contact()
{
    return view('contact');
}
```
###### Create a route for the contact page
```php
Route::get('contact', [PostsController::class, 'contact']);
```
### Passing parameters to views:
###### In PostsController, pass data by using chain method
```php
return view('contact')->with('id', $id);
```
###### Another way of passing data is by using compact method
```php
return view('contact', compact('id', 'name', 'password'));
```
###### For the route
```php
Route::get('contact/{id}/{name}/{password}', [PostsController::class, 'contact']);
```
###### In contact.blade.page, pass the parameters
```php
<h1>Contact Page {{$id}} {{$name}} {{$password}}</h1>
```
