# Insights on this Section
`one to many relationship`
- A single model is the parent to one or more child models.
> ###### in User Model:
```php
public function posts() {
    return $this->hasMany(Post::class);
}
```
> ###### in Post Model:
```php
protected $fillable = [
    'title',
    'body'
];
```
> ###### web.php
`create data`
```php
Route::get('create', function () {
    $user = User::findOrFail(1);

    $post = new Post(["title"=>"crud", "body"=>"one to many relation"]);

    $user->posts()->save($post);
});
```
`read data`
```php
Route::get('read', function () {
    $user = User::findOrFail(1);

    foreach($user->posts as $post):
        echo $post->title;
    endforeach;
});
```
`delete data`
```php
Route::get('delete', function () {
    $user = User::findOrFail(1);

    $user->posts()->where('id', 1)->delete();
});
```
