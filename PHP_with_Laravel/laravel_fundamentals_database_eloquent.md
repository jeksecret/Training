# Insights on this Section
### Eloquent ORM (Object-Relational Mapper):
- Functionality of Laravel.

`read data`
```php
Route::get('read', function () {
    // get all data and loop through it
    $posts = Post::all();

    foreach($posts as $post):
        echo $post->title;
    endforeach;

    // find the id of specific data
    $post = Post::find(2);

    return $post->title;
});
```
`reading data with constraints`
```php
Route::get('findwhere', function () {
    // find specific column in table e.g. is_admin
    $posts = Post::where('is_admin', 0)->orderBy('id', 'desc')->take(2)->get();

    return $posts;
});
```
