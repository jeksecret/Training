# Insights on this Section
`creating routes`
```php
Route::get('/', [App\Http\Controllers\HomeController::class, 'index'])->name('home');
Route::get('/post/{post}', [App\Http\Controllers\PostController::class, 'show'])->name('blog.post');

Route::get('/', [HomeController::class, 'index'])->name('home');
Route::get('/post/{post}', [PostController::class, 'show'])->name('blog.post');

Route::middleware('auth')->group(function () {
    Route::get('/admin', [AdminController::class, 'index'])->name('admin.index');
    Route::get('/admin/posts', [PostController::class, 'index'])->name('posts.index');
    Route::get('/admin/posts/create', [PostController::class, 'create'])->name('posts.create');
    Route::post('/admin/posts', [PostController::class, 'store'])->name('posts.store');
    Route::get('/admin/posts/{post}/edit', [PostController::class, 'edit'])->name('posts.edit');
    Route::patch('/admin/posts/{post}/update', [PostController::class, 'update'])->name('posts.update');
    Route::delete('/admin/posts/{post}/destroy', [PostController::class, 'destroy'])->name('posts.destroy');
});
```
`Resources in PostController`
```php
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;
use Illuminate\Support\Facades\Session;
use App\Models\Post;
```
```php
<?php
public function index()
{
    $posts = Post::all();
    // $posts = auth()->user()->posts;

    // dd($posts);

    return view('admin.posts.index', ['posts' => $posts]);
}

public function show(Post $post)
{
    return view('blog-post', ['post' => $post]);
}

public function create()
{
    return view('admin.posts.create');
}

public function store(Request $request)
{
    $inputs = request()->validate([
        'title' => 'required',
        'post_image' => 'file',
        'body' => 'required'
    ]);

    if(request('post_image'))
    {
        $inputs['post_image']=request('post_image')->store('images');
    }

    auth()->user()->posts()->create($inputs);

    Session::flash('created-message', 'Post was created');

    return redirect()->route('posts.index');
}

public function edit(Post $post)
{
    $this->authorize('view', $post);

    return view('admin.posts.edit', ['post' => $post]);

    // another way
    // if(auth()->user()->can('view', $post))
    // {
    //     return view('admin.posts.edit', ['post' => $post]);
    // }
}

public function update(Post $post)
{
    $inputs = request()->validate([
        'title' => 'required',
        'post_image' => 'file',
        'body' => 'required'
    ]);

    if(request('post_image'))
    {
        $inputs['post_image'] = request('post_image')->store('images');
        $post->post_image = $inputs['post_image'];
    }
    $post->title = $inputs['title'];
    $post->body = $inputs['body'];

    // auth()->user()->posts()->save($post);
    $this->authorize('update', $post);
    $post->update();

    Session::flash('updated-message', 'Post was updated');

    return redirect()->route('posts.index');
}

public function destroy(Post $post)
{
    $post->delete();

    Session::flash('deleted-message', 'Post was deleted');

    return back();
}
```
`displaying session message`
```blade
@if (session('created-message'))
  <div class="alert alert-success">{{session('created-message')}}</div>
@elseif(session('updated-message'))
  <div class="alert alert-info">{{session('updated-message')}}</div>
@elseif (session('deleted-message'))
  <div class="alert alert-danger">{{session('deleted-message')}}</div>
@endif
```
`making a PostPolicy for authorization`
```
php artisan make:policy PostPolicy --model=Post
```
```php
public function view(User $user, Post $post): bool
{
    //
    return $user->id === $post->user_id;
}
public function update(User $user, Post $post): bool
{
    //
    return $user->id === $post->user_id;
}
```
`prevent display for delete button if not authorize user`
```blade
@can('view', $post)
<form action="{{route('posts.destroy', $post->id)}}" method="POST">
  @csrf
  @method("DELETE")
  <button type="submit" class="btn btn-sm btn-danger">Delete</button>
</form>
@endcan
```
