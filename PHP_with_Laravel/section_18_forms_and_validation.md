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
#### views>layouts>app.blade.php
```blade
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Laravel</title>
</head>
<body>
    <div class="container">
        @yield('content')
    </div>

    @yield('footer')
</body>
</html>
```
#### views>posts>create.blade.php
```blade
@extends('layouts.app')

@section('content')

    <h1>Create Post</h1>

    <form action="/posts" method="post">
        {{ csrf_field() }}
        <input type="text" name="title">
        <input type="text" name="content">
        <input type="submit" name="submit">
    </form>

@endsection
```
#### views>posts>edit.blade.php
```blade
@extends('layouts.app')

@section('content')

    <h1>Edit Post</h1>

    <form action="/posts/{{$post->id}}" method="post">
        {{ csrf_field() }}
        <input type="hidden" name="_method" value="PUT">
        <input type="text" name="title" value="{{$post->title}}">
        <input type="text" name="content" value="{{$post->content}}">
        <input type="submit" name="submit">
    </form>

    <form action="/posts/{{$post->id}}" method="post">
        {{ csrf_field() }}
        <input type="hidden" name="_method" value="DELETE">
        <input type="submit" value="delete">
    </form>

@endsection
```
#### views>posts>index.blade.php
```blade
@extends('layouts.app')

@section('content')

    {{-- <h1>{{$post->title}}</h1> --}}

    <ul>
        @foreach ($posts as $post)
            <div class="img-container">
                <img height="100" src="{{$post->path}}" alt="">
            </div>
            <li><a href="{{route('posts.show', $post->id)}}">{{$post->title}}</a></li>
        @endforeach
    </ul>

@endsection
```
#### views>posts>show.blade.php
```blade
@extends('layouts.app')

@section('content')

    <h1><a href="{{route('posts.edit', $post->id)}}">{{$post->title}}</a></h1>

@endsection
```
#### views>contact.blade.php
```blade
@extends('layouts/app')

@section('content')
    <h1>Contact Page</h1>
    @if (count($people))
        @foreach ($people as $person)
            <li> {{$person}} </li>
        @endforeach
    @endif
@endsection
```
