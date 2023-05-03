# Insights on this Section
`polymorphic relationships`
- Allows the child model to belong to more than one type of model using a single association.
> ###### in Staff Model:
```php
protected $fillable = [
    'path'
];
public function imageable() {
    return $this->morphTo();
}
```
> ###### in Product Model:
```php
protected $fillable = [
    'name'
];
public function photos() {
    return $this->morphMany(Photo::class, 'imageable');
}
```
> ###### in Photo Model:
```php
protected $fillable = [
    'name'
];
public function photos() {
    return $this->morphMany(Photo::class, 'imageable');
}
```
> ###### web.php:
`create data`
```php
Route::get('create', function () {
    $staff = Staff::find(1);

    $staff->photos()->create([
        'path'=>'example.jpg'
    ]);
});
```
`read data`
```php
Route::get('read', function () {
    $staff = Staff::findOrFail(1);

    foreach($staff->photos as $photo) {
        echo $photo->path;
    }
});
```
`update data`
```php
Route::get('update', function () {
    $staff = Staff::findOrFail(1);

    $photo = $staff->photos()->where('id', 1)->first();

    $photo->path = "jake.jpg";

    return $photo->save();
});
```
`delete data`
```php
Route::get('delete', function () {
    $staff = Staff::findOrFail(1);

    $staff->photos()->where('id', 1)->delete();
});
```
`assign`
```php
Route::get('assign', function () {
    $staff = Staff::findOrFail(2);

    $photo = Photo::findOrFail(3);

    $staff->photos()->save($photo);
});
```
`unassign`
```php
Route::get('unassign', function () {
    $staff = Staff::findOrFail(2);
    
    $staff->photos()->where('id', 3)->update([
        'imageable_id'=>0,
        'imageable_type'=>''
    ]);
});
```
