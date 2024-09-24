# Running Raw SQL Queries
- Once you have configured your database connection, you may run queries using the DB facade.
  The DB facade provides methods for each type of query: `select`, `update`, `insert`, `delete`, and `statement`.
<br>
**To run a basic query, you may use the select method on the DB facade:**
  <br>

```php
<?php
 
namespace App\Http\Controllers;
 
use App\Http\Controllers\Controller;
use Illuminate\Support\Facades\DB;
 
class UserController extends Controller
{
    /**
     * Show a list of all of the application's users.
     *
     * @return Response
     */
    public function index()
    {
        $users = DB::select('select * from users where active = ?', [1]);
 
        return view('user.index', ['users' => $users]);
    }
}
```

