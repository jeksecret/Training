# Insights on this Section
### Eloquent ORM (Object-Relational Mapper):
- Query functionality mainly used in Laravel.

`read data`
```php
Route::get('read', function () {
    // retrieve all data and loop through it
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
`more ways to retrieve data`
```php
Route::get('findmore', function () {
    // displays 404 if data is not found
    $posts = Post::findOrFail(1);

    return $posts;

    // another example
    $posts = Post::where('users_count', '<', 50)->firstOrFail();
});
```
`basic insert data`
```php
Route::get('basicinsert', function () {
    // instantiate Post class
    $post = new Post;

    $post->title = 'new eloquent title';
    $post->content = 'new eloquent content';

    $post->save();
});
```
`create data with mass assigning`
```php
Route::get('create', function () {
    $param = array(
        'title' => 'insert data with create method',
        'content' => 'example content'
    );

    Post::create($param);
});
```
> In Post Model mass assign the properties.
```php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    use HasFactory;

    // mass assigning
    protected $fillable = [
        'title',
        'content'
    ];
}
```
`update data`
```php
Route::get('update', function () {
    $param = array(
        'title' => 'data with create method',
        'content' => 'example content'
    );
    
    Post::where('id', 5)->where('is_admin', 0)->update($param);
});
```
`delete data`
```php
Route::get('delete', function () {
    $post = Post::find(2);
    $post->delete();

    // deleting using key
    Post::destroy([3, 5]);
});
```
`soft delete data`
```php
Route::get('softdelete', function () {
    Post::find(2)->delete();
});
```
> In Post Model add the SoftDeletes.
```php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes;

class Post extends Model
{
    use HasFactory;
    use SOftDeletes;

    // mass assigning
    protected $fillable = [
        'title',
        'content'
    ];
}
```
`read soft deleted data`
```php
Route::get('readsoftdelete', function () {
    $post = Post::withTrashed()->where('is_admin', 0)->get();

    return $post;
});
```
`restore deleted data`
```php
Route::get('restoredelete', function () {
    Post::withTrashed()->where('is_admin', 0)->restore();
});
```
`force delete data`
```php
Route::get('forcedelete', function () {
    // delete the data completely from db
    Post::withTrashed()->where('is_admin', 0)->forceDelete();
});
```
