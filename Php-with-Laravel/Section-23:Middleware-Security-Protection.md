# Middleware
Middleware provide a convenient mechanism for filtering HTTP requests entering your application. <br>
To create a new middleware, use the `make:middleware `Artisan command: <br>
`php artisan make:middleware MiddlewareName`

**Middleware in routes**
```php
//web.php
use App\Http\Middleware\RoleMiddleware;
use Illuminate\Support\Facades\Auth;

Auth::routes();

//new syntax for Assigning Middleware to Routes
Route::get('/middleware', function(){

    return"Middleware Role";

})->middleware(RoleMiddleware::class);

```

**RoleMiddleware file**
```php
  public function handle(Request $request, Closure $next): Response
    {
        return redirect('/');
        return $next($request);
    }
```
