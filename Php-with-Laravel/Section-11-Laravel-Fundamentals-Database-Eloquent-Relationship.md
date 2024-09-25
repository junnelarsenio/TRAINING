# ELOQUENT RELATIONSHIPS
- **One to One relationship** ( hasOne ) - it is the basic form of Eloquent Relationship where one record in table 1 is connected to another one record in table 2. <br>
  For example, a User model might be associated with one post. To define this relationship, we place a post method on the User model.
The post method should call the `hasOne()` method and return its result:
<br>

```php
<?php
 
namespace App;
 
use Illuminate\Database\Eloquent\Model;
 
class User extends Model
{
    /**
     * Get the post record associated with the user.
     */
    public function post()
    {
        return $this->hasOne('App\Post');
    }
}
```
<br>

- **One to One inverse relationship** ( belongsTo ) - this will let us access the User that owns the post. We can define the inverse of a `hasOne()` relationship using the `belongsTo()` method <br>
<br>

```php
<?php
 
namespace App;
 
use Illuminate\Database\Eloquent\Model;
 
class Post extends Model
{
    /**
     * Get the user that owns the phone.
     */
    public function user()
    {
        return $this->belongsTo('App\User');
    }
}
```

<br>

- **One to Many relationship** ( hasMany ) - this relationship gives one model to access many different kind of model using `hasmany()` method.
  <br>
  
- **Inverse One to Many relationship** - the inverse of one to many is the same as one to one relationship which uses the `belongsTo()` method.
  <br>

- **Many to many** - Many-to-many relations are slightly more complicated than hasOne and hasMany relationships. A user may have a many different roles, and the each role may be owned by many different users.
<br>
  
For example, many users may have the role of "Admin".

<br>

To define this relationship, three database tables are needed:` users`, `roles`, and `role_user`. The `role_user` table is derived from the alphabetical order of the related model names, and contains the `user_id` and `role_id` columns
<br>

**Table structure**

  ```php
  users
    id - integer
    name - string
 
  roles
    id - integer
    name - string
 
  role_user
    user_id - integer
    role_id - integer
  ```

**Model Structure**
  <br>
  This relationship can be defined by using `belongsToMany()` method.
  
```php
<?php
 
namespace App;
 
use Illuminate\Database\Eloquent\Model;
 
class User extends Model
{
    /**
     * The roles that belong to the user.
     */
    public function roles()
    {
        return $this->belongsToMany('App\Role');
    }
}

```

- **Inverse Many to many relationship** - This relationship can be defined by using `belongsToMany()` method.
  the method being use in many to many is the same when using inverse, but you typically use a pivot table that links the two entities
