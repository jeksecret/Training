# Insights on this Section
#### Sessions:
- used to store information about the user across the requests.
> ###### setting up sessions:
`setting and reading sessions`
```php
public function index(Request $request)
{
    // Setting and reading sessions
    $request->session()->put(['PHP'=>'PHP with Laravel']);
    session(['PHP'=>'PHP with Laravel']);
    return $request->session()->all();
    return $request->session()->get('PHP');
}
```
`global session function deleting`
```php
public function index(Request $request)
{
    // Global session function deleting
    session(['PHP2'=>'PHP with Laravel2']);
    return session('PHP2');
    $request->session()->flush();
    return $request->session()->all();
}
```
`flashing data`
```php

public function index(Request $request)
{
  // Flashing data
  // Flashing data will only stay for 1 request.
  $request->session()->flash('message', 'Post has been created.');
  return $request->session()->get('message');

  // Reflashing data
  $request->session()->reflash();
  $request->session()->keep('message');
}
```
