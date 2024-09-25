# New application Laravel 7
## Migration
- `php artisan make:mode Post --mc` :
  - `m`:`migration`,
  - `c`:`controller`.
- Add tables in your created migration:
```php
//2024_09_12_042041_create_posts_table.php -- created by: php artisan make:mode Post --mc
 public function up(): void
    {
        Schema::create('posts', function (Blueprint $table) {
            $table->id();
            $table->foreignId('user_id')->constrained()->onDelete('cascade');
            $table->string('title');
            $table->text('post_image')->nullable();
            $table->text('body');
            $table->timestamps();
        });
    }
```

- Add relationships to `Post` and `User Model`:
```php
//User Model
    public function posts(){        
        return $this->hasMany(Post::class);
    }
```
```php
//Post Model
   protected $guarded = [];
   public function user() {
        return $this->belongsTo('App\Models\User');
    }
```
- Instead of `$fillable`, use `$guarded` so you won't need to add each table category.
- `php artisan migrate` : Dont forget to run the migration.


## Displaying Post on Home View
```php
//HomeController
 public function index()
    {
        $posts = Post::all();

        return view('home', ['posts' => $posts]);
    }
```
- Add a `@foreach` to iterate through all the data in the database.
- Change the values you want to display accordingly.
```blade
{{-- home.blade.php Blog Post--}}
   @foreach ($posts as $post)
      <div class="card mb-4">
        <img class="card-img-top" src="{{$post->post_image}}" alt="Card image cap">
        <div class="card-body">
          <h2 class="card-title">{{$post->title}}</h2>
          <p class="card-text">{{Str::limit($post->body, '300', '...')}}</p>
          <a href="#" class="btn btn-primary">Read More &rarr;</a>
        </div>
        <div class="card-footer text-muted">
          Posted on {{$post->created_at->diffForHumans()}}
          <a href="#">Start Bootstrap</a>
        </div>
      </div>
      @endforeach

```

## Displaying Individual Post
```php
//web.php
Route::get('/post/{post}', [App\Http\Controllers\PostController::class, 'show'])->name('post');
```
```php
//PostController
  public function show(Post $post){
        return view('blog-post', ['post' => $post]);
    }
```
```blade
{{-- home.blade.php Blog Post -> READ MORE BTN--}}
<a href="{{route('post',$post->id)}}" class="btn btn-primary">Read More &rarr;</a>
```

## Creating a Post from Admin
- From the `admin-master` take a section you want to modify into a Create Option.
- Create post route. Add a middleware to `admin.index` and `admin.post`
```php
//web.php
Route::middleware('auth')->group(function(){
    Route::get('/admin', [App\Http\Controllers\AdminController::class, 'index'])->name('admin.index');
    Route::get('/admin/posts/create', [App\Http\Controllers\PostController::class, 'create'])->name('post.create');
});
```
- Add a `create` function in the `PostController`.
```php
//PostController
 public function create(Post $post){
        return view('admin.posts.create'); 
    }
```
- Add a form in the `create.blade.php`
```blade
{{--create.blade.php--}}
<x-admin-master>

    @section('content')

        <h1>Create</h1>

        <form method="post" action="" enctype="multipart/form-data">
            
                @csrf

                <div class="form-group">
                    <label for="title">Title</label>
                        <input  type="text"
                                name="title"
                                class="form-control"
                                id="title"
                                aria-describedby=""
                                placeholder="Enter title">
                </div>

                <div class="form-group">
                        <label for="file">File</label>
                        <input  type="file"
                                name="post_image"
                                class="form-control-file"
                                id="post_image">
                </div>

                <div class="form-group">
                    <textarea
                            name="body"
                            class="form-control"
                            id="body"
                            cols="30"
                            rows="10"></textarea>
                    </div>

                    <button type="submit" class="btn btn-primary">Submit</button>
        </form>

    @endsection

</x-admin-master>
```

## Storing Admin Post
- Add a `store` method in `PostController`
```php
//PostController
public function store(){
        $inputs = request()->validate([
            'title' => 'required|min:8|max:255',
            'post_image' => 'file',
            'body' => 'required'
        ]);
        if (request('post_image')){
            $inputs['post_image'] = request('post_image')->store('images');
        }
        auth()->user()->post()->create($inputs);

        return back();
        
    }
```
- Add it to your route and views
```php
//web.php inside Route::middleware('auth')->group(function()
    Route::post('/admin/posts', [App\Http\Controllers\PostController::class, 'store'])->name('post.store');
```
```blade
{{--create.blade.php--}}
 <form method="post" action="{{route('post.store')}}" enctype="multipart/form-data">
```

## Viewing Admin Post
- Add an `index` method in `PostController`
```php
//PostController
    public function index(){    
        $post = Post::all();
        return view ('admin.posts.index', ['post' => $post]);  
    }
```
- Add it to your routes
```php
//web.php inside Route::middleware('auth')->group(function()
   Route::get('/admin/posts', [App\Http\Controllers\PostController::class, 'index'])->name('post.index');
```
- For views, create an `index.blade.php` in `views/admin/posts`.
- Create a `section` for the copied `<!-- DataTales Example -->`
- Configure `<!-- DataTales Example -->` as follows:
```blade
{{--index.blade.php--}}
<table class="table table-bordered" id="dataTable" width="100%" cellspacing="0">
                  <thead>
                    <tr>
                      <th>Id</th>
                      <th>Title</th>
                      <th>Image</th>
                      <th>Created At</th>
                      <th>Updated At</th>
                    </tr>
                  </thead>
                  <tfoot>
                    <tr>
                      <th>Id</th>
                      <th>Title</th>
                      <th>Image</th>
                      <th>Created At</th>
                      <th>Updated At</th>
                    </tr>
                  </tfoot>
                  <tbody>
                    
                    @foreach ($post as $post)

                    <tr>
                        <td>{{$post->id}}</td>
                        <td>{{$post->title}}</td>
                        <td><img width = "100px" src="{{$post->post_image}}" alt=""></td>
                        <td>{{$post->created_at->diffForHumans()}}</td>
                        <td>{{$post->updated_at->diffForHumans()}}</td>
                    </tr>

                    @endforeach
                  </tbody>
                </table>
```
- Create a section for `Page level plugins` and name it `scripts`.
```blade
{{--index.blade.php--}}
    @section('scripts')

    <!-- Page level plugins -->
    <script src="{{asset('vendor/datatables/jquery.dataTables.min.js')}}"></script>
    <script src="{{asset('vendor/datatables/dataTables.bootstrap4.min.js')}}"></script>

    <!-- Page level custom scripts -->
    <script src="{{asset('js/demo/datatables-demo.js')}}"></script>

    @endSection
```
- Add an mutators to ensure local images are displayed:
```php
//User Model
    public function getPostImageAttribute($value) {
        if (strpos($value, 'https://') !== FALSE || strpos($value, 'http://') !== FALSE) {
            return $value;
        }
        return asset('storage/' . $value);
        }
```
