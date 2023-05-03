# Insights on this Section
### Laravel Collective:
- an html component which is used to build view elements instead of the simple html tags. It is used to make html forms with the help of shortcodes.
> ###### Installing Laravel Collective Package:
```php
composer require laravelcollective/html
```
`modify create form`
```php
@extends('layouts.app')

@section('content')

    <h1>Create Post</h1>

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

    {{-- Displaying validation errors --}}
    @if (count($errors) > 0)
        <div class="alert alert-danger">
            <ul>
                @foreach ($errors->all() as $error)
                    <li>{{ $error }}</li>
                @endforeach
            </ul>
        </div>
    @endif
@endsection
```
`modify edit and delete form`
```php
@extends('layouts.app')

@section('content')

    <h1>Edit Post</h1>

    {!! Form::model($post, ['method'=>'PATCH', 'action'=>['App\Http\Controllers\ResourcePostsController@update', $post->id]]) !!}
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
            {!! Form::submit('Update', ['class'=>'btn btn-primary']) !!}
        </div>
    {!! Form::close() !!}

    {!! Form::model($post, ['method'=>'DELETE', 'action'=>['App\Http\Controllers\ResourcePostsController@destroy', $post->id]]) !!}
    {!! Form::submit('Delete', ['class'=>'btn btn-danger']) !!}
    {!! Form::close() !!}
@endsection
```
