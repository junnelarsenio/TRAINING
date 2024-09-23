# Controllers
### Controllers can group related request handling logic into a single class.
- Creating Controller - ```php artisan make:controller UserController```
- Routing Controller - ```Route::get('user/{id}', 'UserController@show');``` this is written in routes folder

### Example code of controller
```php
<?php
 
namespace App\Http\Controllers;
 
use App\Http\Controllers\Controller;
use App\User;
 
class UserController extends Controller
{
    /**
     * Show the profile for the given user.
     *
     * @param  int  $id
     * @return View
     */
    public function show($id)
    {
        return view('user.profile', ['user' => User::findOrFail($id)]);
    }
}
```
