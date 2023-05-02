# Insights on this Section
> ###### in User Model:
```php
public function roles() {
    return $this->belongsToMany(Role::class);
}
```
> ###### in Role Model:
```php
protected $fillable = [
    'name'
];
```
`create data`
```php
Route::get('create', function () {
    $user = User::findOrFail(2);

    $role = new Role([
        'name'=>'subscriber'
    ]);

    $user->roles()->save($role);
});
```
`read data`
```php
Route::get('read', function () {
    $user = User::all();

    return $user;
    
    // find specific user id
    $user = User::findOrFail(1);

    foreach($user->roles as $role) {
        echo $role;
    }
});
```
`update data`
```php
Route::get('update', function () {
    $user = User::findOrFail(2);

    if($user->has('roles')) {
        foreach($user->roles as $role) {
            if($role->name == 'administrator') {
                $role->name = "Administrator";
                $role->save();
            }
            else if($role->name == 'subscriber') {
                $role->name = "Subscriber";
                $role->save();
            }
            else if($role->name == 'super administrator') {
                $role->name = "Super Administrator";
                $role->save();
            }
        }
    }
});
```
`delete data`
```php
Route::get('delete', function () {
    $user = User::findOrFail(3);

    // $user->roles()->delete();

    foreach($user->roles as $role) {
        $role->where('id', 3)->delete();
    }
});
```
`attach`
- inserts related models when working with many-to-many relations and no array parameter is expected.
```php
Route::get('attach', function () {
    $user = User::findOrFail(3);

    $user->roles()->attach(1);
});
```
`detach`
- remove a certain entity relationship from the pivot table.
```php
Route::get('detach', function () {
    $user = User::findOrFail(3);

    $user->roles()->detach(1);
});
```
`sync`
- this method synchronizes the database entries that means whatever you pass in this method, those records will be kept into the database and the rest will be removed from the intermediate(pivot) table.
```php
Route::get('sync', function () {
    $user = User::findOrFail(1);

    $user->roles()->sync([2, 1]);
});
```
