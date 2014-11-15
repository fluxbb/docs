# Actions

Actions play a central role in FluxBB. They describe the use cases that FluxBB enables and are executed by the server.

When executed, actions have access to input parameters, and are expected to either throw an exception that inherits from `FluxBB\Server\Exception\Exception` or return an associative array of values. They are supposed to orchestrate FluxBB's core services to retrieve or manipulate data, and can also **raise events**.

Actions borrow concepts both from controllers in classical MVC architectures and from command handlers in Domain-Driven Design (DDD).

## Creating actions

To create an action, we need a subclass of `FluxBB\Core\Action`. As the base class is abstract, we must override the `run()` method - the right place to implement custom logic for our action:

```
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

The `run()` method should do three things: Handle user input, pass it to the domain layer and return a response.

## Response types

Responses are usually HTML responses. FluxBB uses a view system for assembling and rendering HTML templates. For transactional actions (login, posting etc.), the user often needs to be redirected.

### HTML responses
Views can be returned using the `view()` method, which accepts a view name and optionally an array of data that should be available in the template.

### Redirects
Both after successful and failing actions, we may want to direct the user to another place in our application. Two methods exist to do so: `redirect()` and `errorRedirect()`. Both have similar signatures: a route name, an array of parameters to pass to the route, and either a redirection message or a bag of error messages.