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
