# Insights on this Section
### Raw SQL Quiries:
`insert data`
```php
Route::get('/insert', function () {
    $param = array('new title', 'new content');

    DB::insert('insert into posts(title, content) values(?, ?)', $param);
});
```
`read data`
```php
Route::get('/read', function () {
    $results = DB::select('select * from posts where id = ?', [1]);

    //results in array
    var_dump($results);

    // foreach($results as $post):
    //     echo $post->title;
    // endforeach;
});
```
`update data`
```php
Route::get('/update', function () {
    DB::update('update posts set title = "updated title", content = "updated content" where id = ?', [1]);
});
```
`delete data`
```php
Route::get('/delete', function () {
    DB::delete('delete from posts where id = ?', [1]);
});
```
