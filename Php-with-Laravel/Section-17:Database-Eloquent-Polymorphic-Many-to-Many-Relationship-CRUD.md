# POLYMORPHIC RELATIONSHIP CRUD
Many to Many relationship

- **Table structure**
```
posts
    id - integer
    name - string
 
videos
    id - integer
    name - string
 
tags
    id - integer
    name - string
 
taggables
    tag_id - integer
    taggable_id - integer
    taggable_type - string

```

- **Creating Data**
```php
use App\Post;
use App\Tag;
use App\Video;

Route::get('/create', function(){

    $post = Post::create(['name'=>'My first post.']);
    
    $tag1 = Tag::find(1);
    $post->tags()->save($tag1);

    $video = Video::create(['name'=>'firstVideo.mov']);

    $tag2 = Tag::find(1);
    $video->tags()->save($tag2);

});
```

- **Reading Data**
```php
use App\Post;
use App\Tag;
use App\Video;

Route::get('/read', function(){

    $post = Post::findOrFail(1);

    foreach($post->tags as $tag){

        echo $tag;
    }
});
```

- **Updating Data**
```php
use App\Post;
use App\Tag;
use App\Video;

Route::get('/update', function(){

    $post = Post::findOrFail(1);

    foreach($post->tags as $tag){

        return $tag->whereName('safe')->update(['name'=>'updated tag.']);
    }
});
```

- **Deleting Data**
```php
use App\Post;
use App\Tag;
use App\Video;

Route::get('/delete', function(){

    $post = Post::findOrFail(1);

    foreach($post->tags as $tag){

        $tag->whereId(1)->delete();
    }
});
```
