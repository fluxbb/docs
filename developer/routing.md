# Routing

The fancy URLs that users see when browsing a FluxBB forum do not reflect in the structure of the forum core. Enter routing. The `FluxBB\Web\Router` class parses pretty URLs such as `/conversations/24` to find out which controller should be executed consequently.

An instance of the router class is bound to the IoC container under the name `FluxBB\Web\Router`. The router class exposes four important methods, named after the four HTTP methods GET, POST, PUT and DELETE. They can be used to register handlers for any combination of URL and HTTP method.

All four methods accept three parameters: a **path**, a **route name** and a **controller action**. The path can contain any number of parameters. The route name is used to quickly generate URLs. The given controller class will be instantiated and the specified action method executed if the route matches a request.

## Creating routes

### Registration

#### Registering a GET route

```php
$router->get('/conversations/{id}', 'conversation', 'FluxBB\ConversationsController@view');
```

#### Registering a POST route

```php
$router->post('/conversations', 'create_conversation', 'FluxBB\ConversationsController@create');
```

#### Registering a PUT route

```php
$router->put('/conversations/{id}', 'edit_conversation', 'FluxBB\ConversationsController@update');
```

#### Registering a DELETE route

```php
$router->delete('/conversations/{id}', 'delete_conversation', 'FluxBB\ConversationsController@delete');
```

### Route parameters

For dynamic content, routes can contain parameters - placeholders for values, such as identifiers. A route path `/post/{id}` will therefore match any request to "/post/42" or "/post/1234/". Normal parameters will match to any alpha-numeric character, except for slashes.

To create more advanced routes, it is possible to define **regular expressions** for a parameter. For example, a route path `/files/{path:.+}` will match any route such as "/files/images/foo.png" or "/files/offer.txt", but not "/files/".

## URL generation

When displaying links, e.g. in views, route names can be used to easily generate full URLs. The `FluxBB\Web\UrlGeneratorInterface` defines the `toRoute()` method. This method is available as `$route` in the views, and can be used like this:

```php
echo $route('conversation', ['id' => $post->conversation_id]);
```

The first parameter refers to a route name, the second parameter is an array of parameters that should be replaced in the URL.
