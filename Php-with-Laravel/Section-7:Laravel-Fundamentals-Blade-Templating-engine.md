# BLADE TEMPLATING ENGINE
### Master Layout
You can create a seprate file for your general layout which you can re-use when routing to different routes.

- `@extends` - This directive indicates that a Blade view inherits from a layout 
  <br>for example
  ```php
  @extends('layouts.app')
  ```
- `@section - @endsection` - After extending a layout, you can define sections to fill in specific areas of that layout.
  <br>for example
  ```php
  @section('content')
    <h1>Welcome to My Blog</h1>
  @endsection
  ```
- `@yield` - This directive indicates where the content of a section should be inserted in the layout.
    <br>for example
  ```php
  <body>
    @yield('content')
  </body>

  ```
