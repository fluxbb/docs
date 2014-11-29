# Actions

Actions play a central role in FluxBB. They describe the use cases that FluxBB enables and are executed by the server.

When executed, actions have access to input parameters, and are expected to either throw an exception that inherits from `FluxBB\Server\Exception\Exception` or return an associative array of values. They are supposed to orchestrate FluxBB's core services to retrieve or manipulate data, and can also **raise events**.

Actions borrow concepts both from controllers in classical MVC architectures and from command handlers in Domain-Driven Design (DDD).

## Creating actions

To create an action, we need a subclass of `FluxBB\Core\Action`. As the base class is abstract, we must override the `run()` method - the right place to implement custom logic for our action:

```php
<?php namespace FluxBB\Actions;

use FluxBB\Core\Action;

class GetBooks extends Action
{
    protected function run()
    {
        //
    }
}
```

The `run()` method should do three things: Handle user input, pass it to the domain layer and return response data.

## Handling input

```php
$id = $this->get('id');
$sortBy = $this->get('sort_order', 'asc');
```

The `get()` method gives the developer access to any parameters passed to the action. It accepts two parameters: first, the key of the parameter to retrieve. The second, optional parameter allows for defining a default value.

## Raising events

After successful execution, actions should raise events, so that other parts of the system or extensions can be notified of what happened. This can be done using the convenient `raise()` method:

```php
$this->raise(new UserCreated($user));
```

## Returning data

To make results available to the caller, an associative array can be returned. For example, to return a newly created post instance:

```php
return [
    'post' => $post,
];
```
