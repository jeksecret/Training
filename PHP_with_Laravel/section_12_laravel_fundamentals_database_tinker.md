# Insights on this Section
### Tinker:
- Allows you to interact with your entire Laravel application on the command line.

###### commands
```php
php artisan tinker
// create data using tinker
$post = App\Models\Post::create([‘title’=>’New title from this tinker’,’body’=>’New content from this tinker’])

// create date using object in tinker
$post = new App\Models\Post
$post->title = “title from this object”
$post->body = “content from this object”

// finding record using eloquent
$post = App\Models\Post::find(1)
$post = App\Models\Post::whereId(1)->first()

// update and delete data in tinker
$post = App\Models\Post::find(1);
$post->title = “updated title of id 1”
$post->body = “updated content of id 1”
$post->save()

// soft delete
$post->delete()
$post = App\Models\Post::onlyTrashed()

// force delete
$post->forceDelete()
```
