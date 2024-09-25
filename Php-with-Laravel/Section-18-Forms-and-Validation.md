# FORMS AND VALIDATION
**CSRF Protections** - protect your application from cross-site request forgery (CSRF) attacks.

Anytime you define an HTML form in your application, you should include a hidden CSRF token field in the form so that the CSRF protection middleware can validate the request.

```php
<form method="POST" action="/profile">
    @csrf
    ...
</form>
```
**Validation Errors**

```php
<!-- /resources/views/post/create.blade.php -->
 
<label for="title">Post Title</label>
 
<input id="title" type="text" class="@error('title') is-invalid @enderror">
 
@error('title')
    <div class="alert alert-danger">{{ $message }}</div>
@enderror
```
