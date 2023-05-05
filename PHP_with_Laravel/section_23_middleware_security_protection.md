# Insights on this Section
#### Middleware:
- acts as a bridge between a request and a reaction. It is a type of sifting component. Laravel incorporates a middleware that confirms whether or not the client of the application is verified. If the client is confirmed, it diverts to the home page otherwise, it diverts to the login page.

> ###### to create a middleware
```cmd
  php artisan make:middleware "RoleMiddleware"
  php artisan make:middleware "IsAdmin"
```
> ###### to registered the newly created middleware
`in kernel.php $middlewareAliases`
```php
  'role' => \App\Http\Middleware\RoleMiddleware::class,
  'isAdmin' => \App\Http\Middleware\IsAdmin::class,
```
`in RoleMiddleware.php Middleware`
```php
  return redirect('/');
```
`in User.php create a function`
```php
  public function isAdmin() {
      if($this->role->name == 'admin') {
          return true;
      }
      return false;
  }
```
`in IsAdmin.php Middleware`
```php
public function handle(Request $request, Closure $next): Response
  {
    // $user = Auth::user();

    // if(!$user->isAdmin()) {
    //     return redirect('/');
    // }
    // return $next($request);

    if(Auth::check()) {
        if (Auth::user()->isAdmin()) {
            return $next($request);
        }
    }
    return redirect('/');
  }
```
`in AdminController.php`
```php
public function __construct() {
    $this->middleware('isAdmin');
}

public function index() {
    return "Administrator Account.";
}
```
`in web.php`
```php
Route::get('/admin/user/roles', ['middleware'=>['role', 'auth', 'web'], function () {
    return "Middleware role";
}]);
Route::get('/admin', [AdminController::class, 'index']);
```
