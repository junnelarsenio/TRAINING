# Laravel Components
To create a class based component, you may use the `make:component` Artisan command: <br>
`php artisan make:component Alert`

The `make:component` command will also create a view template for the component. <br>
The view will be placed in the `resources/views/components` directory.

- **Displaying component** <br>
To display a component, you may use a Blade component tag within one of your Blade templates.
```
<x-alert/>
 
<x-user-profile/>
```
