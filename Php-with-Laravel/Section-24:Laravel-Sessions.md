# SESSIONS
- sessions allow you to store user data across requests.
  <br>
  <br>
  
**Sample code for sessions:**
```php

 public function index(Request $request)
    {
        //Setting up sessions
        $request->session()->put(['name'=>'aj']);
        
        //Updating sessions
        session(['more sessions'=>'replaced session']);
        
        // Deleting sessions
        request->session()->forget('more sessions');
        
        // Delete all sessions
         $request->session()->flush();
        
        //Reading sessions
        return $request->session()->all();
        
    }
```

```php

public function destroy(Post $post){

        $this->authorize('update');

        $post->delete();

        Session::flash('message', 'Post was deleted!');
        return back();
    }

```
