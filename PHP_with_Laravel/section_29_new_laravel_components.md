# Insights on this Section
#### Components:
- Laravel components are a small entity with an interface that is well defined. These serve as the building block for a large software system. All the related data is encapsulated in the reusable unit.
> ###### Returning the view in the controller@index:
```php
return view('components.latest-posts');
```
> ###### To display the component in your blade template we can call it using a custom <x-{component name}/> tag syntax.
```php
<x-latest-posts>

</x-latest-posts>
```
