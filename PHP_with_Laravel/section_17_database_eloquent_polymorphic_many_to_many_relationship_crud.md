# Insights on this Section
`polymorphic many to many relationships`
> ###### in Post Model:
```php
protected $fillable = [
    'name'
];

public function tags() {
    return $this->morphToMany(Tag::class, 'taggable');
}
```
> ###### in Tag Model:
```php
protected $fillable = [
    'name'
];
```
> ###### in Taggable Model:
```php

```
> ###### in Video Model:
```php
protected $fillable = [
    'name'
];

public function tags() {
    return $this->morphToMany(Tag::class, 'taggable');
}
```
> ###### web.php
`create data`
```php
Route::get('create', function () {
    // post
    $post = Post::create([
        'name'=>'first post'
    ]);

    $post_tag = Tag::find(1);
    
    $post->tags()->save($post_tag);
    
    // video
    $video = Video::create([
        'name'=>'vid.mov'
    ]);

    $video_tag = Tag::find(1);

    $video->tags()->save($video_tag);
});
```
`read data`
```php
Route::get('read', function () {
    $post = Post::findOrFail(1);

    foreach($post->tags as $tag) {
        return $tag->name;
    }
});
```
`update data`
```php
Route::get('update', function () {
    // $post = Post::findOrFail(1);

    // foreach($post->tags as $tag) {
    //     $tag->where('id', 1)->update([
    //         'name'=>'PHP'
    //     ]);
    // }

    $post = Post::findOrFail(1);

    $tag = Tag::find(3);

    $post->tags()->save($tag);
    // $post->tags()->attach($tag);
    // $post->tags()->sync([2, 2]);
});
```
`delete data`
```php
Route::get('delete', function () {
    $post = Post::find(1);

    foreach($post->tags as $tag) {
        $tag->where('id', 1)->delete();
    }
});
```
