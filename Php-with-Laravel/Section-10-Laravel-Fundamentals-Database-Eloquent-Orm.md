# Database - Eloquent ORM
- Eloquent makes managing and working with relationships easy, and supports several different types of relationships:
   - One to one
   - One to many
   - Many to many
   - Has one Through
   - Has many Through
   - One to one (Polymorphic)
   - One to many (Polymorphic)
   - Many to many (Polymorphic)
     
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
- **Deleting Data**
  ```php
  Route::get('/delete', function(){
  
  $post = Post::find(1);
  $post->delete();

  });
  ```

    ```php
  Route::get('/delete2', function(){
  
  Post::destroy(1);
  

  });
  ```
  
    
