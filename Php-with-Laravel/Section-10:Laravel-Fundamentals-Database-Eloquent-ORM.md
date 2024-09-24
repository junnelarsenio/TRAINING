# Database - Eloquent ORM

- **Reading Data**
  ```php
  Route::get('/find', function(){
  
  $post = Post::find(1);
  return $post->title;
  
  });
  
  ```
- **Inserting/Saving Data**
  ```php
  Route::get('/basicinsert', function(){
  
  $post = Post::find(1);

  $post->title = 'New Eloquent title insert';
  $post->content = 'Wow eloquent is really cool, look at this content';

  $post->save();
  });
  ```
- **Updating Data**
  ```php
  Route::get('/update', function(){
  
  Post::where('id', 2)->where('is_admin', 0)->update(['title'=>'NEW PHP TITLE', 'content'=>'I love my Instructor Edwin']);
  
  });
  ```
  
