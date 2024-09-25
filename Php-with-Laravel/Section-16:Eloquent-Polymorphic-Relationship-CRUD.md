# POLYMORPHIC RELATIONSHIP CRUD
### One To One (Polymorphic)

**Table Structure**
```
products
    id - integer
    name - string
 
staff
    id - integer
    name - string
 
photos
    id - integer
    path - string
    imageable_id - integer
    imageable_type - string
```

**Model Structure**
```
<?php
 
namespace App;
 
use Illuminate\Database\Eloquent\Model;
 
class Photo extends Model
{
    /**
     * Get the owning imageable model.
     */
    public function imageable()
    {
        return $this->morphTo();
    }
}
 
class Product extends Model
{
    /**
     * Get the products's photo.
     */
    public function photos()
    {
        return $this->morphOne('App\Models\Photo', 'imageable');
    }
}
 
class Staff extends Model
{
    /**
     * Get the staff's photo.
     */
    public function photos()
    {
        return $this->morphOne('App\Models\Photo', 'imageable');
    }
}
```
<br>

- **Creating Data**
```php
use App\Staff;
use App\Photo;

Route::get('/create', function(){
    $staff = Staff::findOrFail(1);
    $staff->photos()->create(['path'=>'example.jpg']);
});
```

- **Reading Data**
```php
use App\Staff;
use App\Photo;

Route::get('/read', function(){
    $staff = Staff::findOrFail(1);
    foreach($staff->photos as $photo){
        return $photo->path;
    }
});
```

- **Updating Data**
```php
use App\Staff;
use App\Photo;

Route::get('/update', function(){
    $staff = Staff::findOrFail(1);
    $photo = $staff->photos()->whereId(1)->first();
    $photo->path = "Update photo.";
    $photo->save();
});
```

- **Deleting Data**
```php
use App\Staff;
use App\Photo;

Route::get('/delete', function(){
    $staff = Staff::findOrFail(1);
    $staff->photos()->delete();
});
```
