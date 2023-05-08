# Insights on this Section

#### Modify form:
```blade
{!! Form::open(['method'=>'POST', 'action'=>'App\Http\Controllers\ResourcePostsController@store', 'files'=>true]) !!}
    @csrf
    <div class="form-group">
        {!! Form::label('title', 'Title:') !!}
        {!! Form::text('title', null, ['class'=>'form-control']) !!}
    </div>
    <div class="form-group">
        {!! Form::label('content', 'Content:') !!}
        {!! Form::text('content', null, ['class'=>'form-control']) !!}
    </div>
    <div class="form-group">
        {!! Form::file('file', null, ['class'=>'form-control']) !!}
    </div>
    <div class="form-group">
        {!! Form::submit('Create', ['class'=>'btn btn-primary']) !!}
    </div>
{!! Form::close() !!}
```
`retrieve data`
```php
$file = $request->file('file');
echo $file->getClientOriginalName();
echo "<br/>";
echo $file->getClientSize();

Post::create($input);
```
`store data to db`
```php
$input = $request->all();

  if($file = $request->file('file')) {
  $name = $file->getClientOriginalName();
  $file->move('images', $name);
  $input['path'] = $name;
}
Post::create($input);
```
`display images using accessors`
```php
public function getPathAttribute($value) {
    return $this->directory . $value;
}
```
