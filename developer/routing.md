# Routing

The fancy URLs that users see when browsing a FluxBB forum do not reflect in the structure of the forum core. Enter routing. The `FluxBB\Web\Router` class parses pretty URLs such as `/conversations/24` to find out which controller should be executed consequently.

An instance of the router class is bound to the IoC container under the name `FluxBB\Web\Router`. The router class exposes four important methods, named after the four HTTP methods GET, POST, PUT and DELETE. They can be used to register handlers for any combination of URL and HTTP method.

All four methods accept three parameters: a **path**, a **route name** and a **controller action**. The path can contain any number of parameters. The route name is used to quickly generate URLs. The given controller class will be instantiated and the specified action method executed if the route matches a request.

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


TODO: Parameters. With regular expressions. URL generation.

