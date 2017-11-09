# TemplateX

A simple, micro template engine for PHP

## Getting Started

Loading your template:

```php
<?php

// Define your template paths
$templatePaths = [ __DIR__ . '/templates/' ];

// Create a new instance
$x = new wpscholar\TemplateX( $templatePaths );

// Set a template (relative to the template path)
$x->setTemplate( 'event.php' );

// Pass variables to your template
$x->setContext( [
    'title' => 'County Fair',
    'venue' => 'County Fairgrounds', 
] );

// Render the template
echo $x->render();
```

The template file:

```php
<?php
/**
 * @var \wpscholar\TemplateX $x
 */
?>
<div class="event">
    <h1><?php echo $x->get('title'); ?></h1>
    <div><strong>Venue</strong>: <?php echo $x->get('venue', 'To Be Determined'); ?></div>
</div>
```

## Documentation

### Is

>Check if a variable has a specific value.
>
>```php
>$x->is( $name, $value );
>```
>
>**Params**:
>
>* *string* - Name of the variable to check.
>* *mixed* - Value to check.
>
>**Return Value**: 
>
>*boolean*
>
>**Description**:
>
>The `is()` method allows you to check if a variable in the template's context contains a specific value.

### Has

>Check if a variable exists.
>
>```php
>$x->has( $name );
>```
>**Params**:
>
>* *string|array* - Name of the variable to check, or a path to a nested value.
>
>**Return Value**: 
>
>*boolean*
>
>**Description**:
>
>The `has()` method allows you to check if a variable exists in the template's context. You can pass in a variable name, or a path to a nested data structure. For example, you can pass in an array, or use dot notation (e.g. `var.0.title` will look for a variable named `var`, find the first item in the array, and then find the title property from the object).

### Has In

>Check if a value exists in an object or an array.
>
>```php
>$x->hasIn( $data, $name );
>```
>
>**Params**:
>
>* *object|array* - Data from which to locate value.
>* *string|array* - Name of variable, or nested path.
>
>**Return Value**: 
>
>*boolean*
>
>**Description**:
>
>The `hasIn()` method is the same as the `has()` method, except you can pass in your own data as opposed to defaulting to the template's context.

### Get

> Get a variable.
>
>```php
>$x->get( $name, $default );
>```
>
>**Params**:
>
>* *string|array* - Name (or path) of the variable to be fetched.
>* *string|array* - The default value to be returned if variable doesn't exist.
>
>**Return Value**: 
>
>*mixed*
>
>**Description**:
>
>The `get()` method allows you to fetch a value from the template's context. You can pass in a variable name, or a path to a nested data structure. For example, you can pass in an array, or use dot notation (e.g. `var.0.title` to get the title property from the first value in the array contained in the variable named `var`.) Optionally, you can pass in a default value to be returned if the variable you are asking for isn't defined.

### Get In

> Get a value from an object or an array.
>
>```php
>$x->getIn( $data, $name, $default );
>```
>
>**Params**:
>
>* *object|array* - Data from which to fetch value.
>* *string|array* - Name (or path) of the variable to be fetched.
>* *mixed* - The default value to be returned if variable doesn't exist.
>
>**Return Value**: 
>
>*mixed*
>
>**Description**:
>
> The `getIn()` method is the same as the `get()` method, except you can pass in your own data as opposed to defaulting to the template's context. 

### Set

>Set a variable.
>
>```php
>$x->set( $name, $value );
>```
>
>**Params**:
>
>* *string|array* - Name (or path) of the variable to be set.
>* *mixed* - The value to be assigned.
>
>**Return Value**: 
>
>*void*
>
>**Description**:
>
>The `set()` method allows you to set a value in the template's context. You can pass in a variable name, or a path to a nested data structure. For example, you can pass in an array, or use dot notation (e.g. `var.0.title` to set the title property from the first value in the array contained in the variable named `var`.) Optionally, you can pass in a default value to be returned if the variable you are asking for isn't defined.

### Set In

>Set a value in an object or an array.
>
>```php
>$x->setIn( $data, $name, $value );
>```
>
>**Params**:
>
>* *object|array* - Data in which to set value.
>* *string|array* - Name (or path) of the variable to be set.
>* *mixed* - The value to be assigned.
>
>**Return Value**: 
>
>*mixed* - Returns the updated data or original data on failure.
>
>**Description**:
>
> The `setIn()` method is the same as the `set()` method, except you can pass in your own data as opposed to defaulting to the template's context.

### Delete

>Unset a variable.
>
>```php
>$x->delete( $name );
>```
>
>**Params**:
>
>* *string|array* - Name of the variable to be deleted.
>
>**Return Value**: 
>
>*void*
>
>**Description**:
>
> The `delete()` method will remove a variable from the template's context.

### Load

> Loads a template from within an existing template.
>
>```php
>$x->load( $template, $vars, $withContext = true );
>```
>
>**Params**:
>
>* *string* - Relative path to the template to be loaded.
>* *array* - An associative array containing variable names and values to pass to the template.
>* *boolean* - Whether or not to keep the variables from the parent template's context.
>
>**Return Value**: 
>
>*void*
>
>**Description**:
>
> The `load()` method will output a child template within a template.

### Render

> Render a template to a string.
>
>```php
>$x->render();
>```
>
>**Params**:
>
> *none*
>
>**Return Value**: 
>
>*string*
>
>**Description**:
>
> The `render()` method will return a string containing the rendered template.

### Set Template

> Set the template to be rendered.
>
>```php
>$x->setTemplate( $template );
>```
>
>**Params**:
>
> *string* - Relative path to the template to be rendered.
>
>**Return Value**: 
>
>*void*
>
>**Description**:
>
> The `setTemplate()` method is how you set the template that you want to render. It will be the relative path to the template (e.g. `event.php`).

### Set Context

> Set the context.
>
>```php
>$x->setContext( $vars );
>```
>
>**Params**:
>
> *array* - An associative array containing variable names and values to pass to the template. 
>
>**Return Value**: 
>
>*void*
>
>**Description**:
>
> The `setContext()` method allows you to pass variables to the template's context. Any variables passed will be made available to the template being rendered.

### Set Template Paths

> Set the template paths.
>
>```php
>$x->setTemplatePaths( $templatePaths );
>```
>
>**Params**:
>
> *array* - An array of template paths.
>
>**Return Value**: 
>
>*void*
>
>**Description**:
>
> The `setTemplatePaths()` method allows you to define one or more template paths to check when attempting to load a template.

### Add Template Path

> Add a template path.
>```php
>$x->addTemplatePath( $templatePath );
>```
>
>**Params**:
>
> *string* - A template path to append to the list of template paths.
>
>**Return Value**: 
>
>*void*
>
>**Description**:
>
> The `addTemplatePath()` method allows you to append a template path to the list of template paths to check when attempting to load a template. 