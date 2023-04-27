# Insights on this Section
### Eloquent Relationships:
- Allows to relay tables in a very easy format using functions.

`one to one relationship`
- A one model can be associated with another one model.
> ###### in User Model:
```php
public function post() {
    return $this->hasOne(Post::class);
}
```
```php
Route::get('user/{id}/post', function ($id) {
    $user = User::find($id);

    return $user->post->title;
});
```
`one to one relationship inverse`
> ###### in Post Model:
```php
public function user() {
    return $this->belongsTo(User::class);
}
```
```php
Route::get('post/{id}/user', function ($id) {
    $post = Post::find($id);

    return $post->user;
});
```
`one to many relationship`
- A single model is the parent to one or more child models.
> ###### in User Model:
```php
public function posts() {
    return $this->hasMany(Post::class);
}
```
```php
Route::get('user/{id}/posts', function ($id) {
    $user = User::find($id);

    foreach($user->posts as $post):
        echo $post->title . "<br/>";
    endforeach;
});
```
`many to many relationship`
> ###### in User Model:
```php
public function roles() {
    return $this->belongsToMany(Role::class);
}
```
```php
Route::get('user/{id}/role', function ($id) {
    // $user = User::find($id)->roles()->orderBy('id', 'desc')->get();

    // return $user;

    $user = User::find($id);

    foreach($user->roles as $role):
        echo $role->name;
    endforeach;
});
```
> ###### Intermidiate/Pivot Table:
- Is a middle table that is used in many to many relationship. It holds the foreign keys that are used to associate two models (two different tables).
> ###### in User Model:
```php
public function roles() {
    return $this->belongsToMany(Role::class)->withPivot('created_at');
}
```
`retrieving intermidiate/pivot table`
```php
Route::get('user/pivot', function () {
    $user = User::find(1);

    foreach($user->roles as $role):
        echo $role->pivot->created_at;
    endforeach;
});
```
