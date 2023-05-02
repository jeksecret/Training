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
