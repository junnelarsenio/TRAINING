# Package and Validation
**Writing The Validation Logic**
```php
public function store(Request $request): RedirectResponse
{
    $validated = $request->validate([
        'title' => 'required|unique:posts|max:255',
        'body' => 'required',
    ]); 
    // The blog post is valid...
     return redirect('/posts');
}
```
