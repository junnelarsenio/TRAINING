# Some More Model Manipulation

### Dates
```php
use Illuminate\Support\Carbon;
Route::get('/dates', function(){

    $date = new DateTime('+1 week');
    echo $date->format('m-d-y');

    echo '<br>';
    echo Carbon::now();
    echo '<br>';
    echo Carbon::now()->diffForHumans();
    echo '<br>';
    echo Carbon::now()->addDays(15)->diffForHumans();
    echo '<br>';
    echo Carbon::now()->yesterday()->diffForHumans();
});

```

### Accessor and Mutator

```php
//User Model
  public function getNameAttribute($value){
        return strtoupper($value);
    }

 public function setNameAttribute($value){
        $this->attributes['name'] = strtoupper($value);
    }
```

```php
//web.php
Route::get('/setname', function(){

    $user = User::findOrfail(1);
    $user->name = "Jean";
    $user->save();

});

Route::get('/getname', function(){

    $user = User::findOrfail(1);
    return $user;
    
});
```
