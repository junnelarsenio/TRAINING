# ELOQUENT MANY TO MANY CRUD
Using `belongsToMany()` method:
- **Creating Data**
```php
use App\User;
use App\Role;

Route::get('/create', function(){
    $user = User::find(1);
    $user->roles()->save(new Role(['name'=>'Administrator']));
});
```
  
- **Reading Data**
```php
use App\User;
use App\Role;

Route::get('/read', function(){
    $user = User::findOrFail(1);
    foreach($user->roles as $role){
        echo $role->name;
    }
});
```

- **Updating Data**
```php
use App\User;
use App\Role;

Route::get('/update', function(){
    $user = User::findOrFail(1);
    if($user->has('roles')){
        foreach($user->roles as $role){
            if($role->name == 'Administrator'){
                $role->name = 'admin';
                $role->save();
            }
        }
    }
});
```
  
- **Deleting Data**
```php
use App\User;
use App\Role;

Route::get('/delete', function(){
    $user = User::findOrFail(1);    
    foreach($user->roles as $role){
        $role->whereId(1)->delete();
    }
});
```
  
