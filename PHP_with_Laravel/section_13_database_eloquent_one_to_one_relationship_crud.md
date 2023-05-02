# Insights on this Section
`one to one relationship`
- A one model can be associated with another one model.
> ###### in User Model:
```php
public function address() {
    return $this->hasOne(Address::class);
}
```
> ###### web.php
`create data`
```php
Route::get('insert', function () {
    $user = User::findOrFail(1);

    // instantiate address class
    $address = new Address([
        'name' => '123 Address'
    ]);

    $user->address()->save($address);
});
```
`update data`
```php
Route::get('update', function () {
    // first() will returns the object
    $address = Address::where('user_id', 1)->first();

    $address->name = "Updated 123 Address";

    $address->save();
});
```
`read data`
```php
Route::get('read', function () {
    $user = User::findOrFail(1);

    return $user->address->name;
});
```
`delete data`
```php
Route::get('delete', function () {
    $user = User::findOrFail(1);

    $user->address()->delete();
});
```
