# ELOQUENT ONE TO MANY RELATIONSHIP CRUD
Using The `hasMany()` method:
- **Creating Data**
```php
use App\User;
use App\Post;

Route::get('/create', function(){
    $user = User::findOrFail(1);
    $post = new Post(['title'=>'First Post', 'body'=>'This is body']);
    $user->posts()->save($post);
});
```

- **Reading Data**
```php
use App\User;
use App\Post;

Route::get('/read', function(){
    $user = User::findOrFail(1);
    foreach($user->posts as $post){
        echo $post->title . "<br>";
    }
});
```

- **Updating Data**
```php
use App\User;
use App\Post;

Route::get('/update',function(){
    $user = User::find(1);
    $user->posts()->whereId(1)->update(['title'=>'I love laravel','body'=>'This is awesome']);
});
```

- **Deleting Data**
```php
use App\User;
use App\Post;

Route::get('/delete',function(){
    $user = User::find(1);
    $user->posts()->whereId(1)->delete();
});
```
