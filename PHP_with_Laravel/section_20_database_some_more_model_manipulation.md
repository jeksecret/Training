# Insights on this Section
#### Date Mutators:
- Eloquent will convert the created_at and updated_at columns to instances of Carbon, which provides an assortment of helpful methods, and extends the native PHP DateTime class.

`Carbon`
```php
Route::get('/dates', function () {
    $date = new DateTime();
    echo $date->format('m-d-Y');

    echo "<br/>";
    
    echo Carbon::now()->addDays(10)->diffForHumans();

    echo "<br/>";
    
    echo Carbon::now()->subMonths(10)->diffForHumans();

    echo "<br/>";
    
    echo Carbon::now()->yesterday();
});
```
#### Accessors & Mutators
- A accessor, create a `getFooAttribute` method on your model where Foo is the "studly" cased name of the column you wish to access. In this example, we'll define an accessor for the first_name attribute. A mutator, define a `setFooAttribute` method on your model where Foo is the "studly" cased name of the column you wish to access. So, again, let's define a mutator for the first_name attribute.
```php
// Accessor gets the data
public function getNameAttribute($value) {
    return ucfirst($value);
}

// Mutator mutates the data
public function setNameAttribute($value) {
    $this->attributes['name'] = ucfirst($value);
}
```
