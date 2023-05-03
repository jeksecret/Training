# Insights on this Section
> ###### make a request file CreatePostsRequest.php`
```php
php artisan make:request CreatePostsRequest
```
> ###### in ResourcePostsController:
```php
use App\Http\Requests\CreatePostsRequest;
use App\Models\Post;
use Illuminate\Http\Request;
```
`Display a listing of the resource.`
```php
public function index()
{
  //
  // $posts = Post::all();
  // $posts = Post::latest()->get();
  $posts = Post::list();
  return view('posts.index', compact('posts'));
}
```
`Show the form for creating a new resource.`
```php
public function create()
{
  //
  return view('posts.create');
}
```
`Store a newly created resource in storage.`
```php
// public function store(Request $request)
public function store(CreatePostsRequest $request)
{
    //
    // Basic Validation
    // $this->validate($request, [
    //     'title'=>'required|max:4',
    //     'content'=>'required'
    // ]);

    // Post::create($request->all());

    // $input = $request->all();
    // $input['title'] = $request->title;
    // Post::create($request->all());

    // $post = new Post;
    // $post->user_id = 0;
    // $post->title = $request->title;
    // $post->content = $request->content;
    // $post->save();

    // return redirect('/posts');

    // $file = $request->file('file');
    // echo $file->getClientOriginalName();
    // echo "<br/>";
    // echo $file->getClientSize();

    $input = $request->all();

    if($file = $request->file('file')) {
        $name = $file->getClientOriginalName();
        $file->move('images', $name);
        $input['path'] = $name;
    }
    Post::create($input);
}
```
`Display the specified resource.`
```php
public function show(string $id)
{
    //
    $post = Post::findOrFail($id);
    return view('posts.show', compact('post'));
}
```
`Show the form for editing the specified resource.`
```php
public function edit(string $id)
{
    //
    $post = Post::findOrFail($id);
    return view('posts.edit', compact('post'));
}
```
`Update the specified resource in storage.`
```php
public function update(Request $request, string $id)
{
    //
    $post = Post::findOrFail($id)->update($request->all());

    return redirect('/posts');
}
```
`Remove the specified resource from storage.`
```php
public function destroy(string $id)
{
    //
    $post = Post::findOrFail($id)->delete();

    return redirect('/posts');
}
```
