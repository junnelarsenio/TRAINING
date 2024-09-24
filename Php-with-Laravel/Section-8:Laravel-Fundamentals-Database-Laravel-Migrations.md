# DATABASE MIGRATIONS
`Migration` - allow to modify the application's database schema

**Creating Migration**
<br>
To create a migration, use the `make:migration` artisan command
<br>
`php artisan make:migration create_users_table`
<br>
**Running Migration**
<br>
`php artisan migrate`

**Migration Structure**
```php
<?php
 
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;
 
class CreateUsersTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->timestamps();
        });
    }
 
    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::drop('users');
    }
}
```

