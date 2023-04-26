# Insights on this Section Course
### Blade Template:
- Blade is a templating engine that is used in Laravel framework.
### Layout setup:
- Inside `views folder` create a file with directly as a master layout. `layouts/app.blade.php`

###### In `app.blade.php`
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Laravel</title>
</head>
<body>
    <div class="container">
        @yield('content')
    </div>

    @yield('footer')
</body>
</html>
```
###### In `contact.blade.php` extend the app file by using `@extends` and add each `@yields` as a `@section` inside it
```php
@extends('layouts/app')

@section('content')
    <h1>Contact Page {{$id}} {{$name}} {{$password}}</h1>
@endsection

@section('footer')
    <script>alert('Contact Page')</script>
@endsection
```
### Using for and foreach in blade template:
###### In `contact.blade.php`
```php
@extends('layouts/app')

@section('content')
    <h1>Contact Page</h1>
    @if (count($people))
        @foreach ($people as $person)
            <li> {{$person}} </li>
        @endforeach
    @endif
@endsection
```
