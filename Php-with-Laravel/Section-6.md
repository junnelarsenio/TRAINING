# Views
### Views contain the HTML served by your application

#### Creating views
- you will create a file in resources/view folder
  
- example code
```html
<!-- View stored in resources/views/greeting.blade.php -->
 
<html>
    <body>
        <h1>Hello, {{ $name }}</h1>
    </body>
</html>
```

- example route for the view
```php
Route::get('/', function () {
    return view('greeting', ['name' => 'James']);
});
```
