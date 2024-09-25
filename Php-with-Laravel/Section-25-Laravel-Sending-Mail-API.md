# Sending Mail
Package that require

`composer require guzzlehttp/guzzle`

**Sample mail through routes**
```php
use Illuminat\Support\Facades\Mail;

Route::get('/', function(){

$data = [
      'title' => 'Hi student I hope you like the course',
      'content' => 'The Laravel course was created with a lot of love and dedication for you'
];

Mail::send('emails.test', $data, function(message){
  
    $message->to('edwin@edwindiaz.com', 'edwin')->subject('Hello student how are you?')
});
```
