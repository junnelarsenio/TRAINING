# ELOQUENT ONE TO ONE RELATIONSHIP CRUD
- **Creating Data**
```php
use App\User;
use App\Address;

Route::get('/insert', function(){
    $user = User::findOrFail(1);
    $address = new Address(['address'=>'Mahawak Medellin Cebu']);
    $user -> address()->save($address);
});
```

- **Reading Data**
```php
use App\User;
use App\Address;

Route::get('/read', function(){
    $user = User::findOrFail(1);
    echo $user->address()->address;
});
```

- **Updating Data**
```php
use App\User;
use App\Address;

Route::get('/update', function(){
    $address = Address::whereUserId(1)->first();
    $address->address="New Address";
    $address->save();
});
```

- **Deleting Data**
```php
use App\User;
use App\Address;

Route::get('/delete', function(){
    $user = User::find(1);
    $user->address()->whereId(5)->delete();
});
```
