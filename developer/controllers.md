# Controllers

Controllers handle HTTP requests, turn them into actions for the FluxBB server to execute, and return responses to the user.

## Response types

Responses are usually HTML responses. FluxBB uses a view system for assembling and rendering HTML templates. For transactional actions (login, posting etc.), the user often needs to be redirected.

### HTML responses
Views can be returned using the `view()` method, which accepts a view name and optionally an array of data that should be available in the template.

```php
return $this->view('single_post', ['post' => $post, 'author' => $user]);
```

This will render the view named "single_post" and make sure the post and user data are available in the template as `$post` and `$author`, respectively.

### Redirects
Both after successful and failing actions, we may want to direct the user to another place in our application. Two methods exist to do so: `redirectTo()` and `errorRedirectTo()`. Both have similar signatures: a route name, an array of parameters to pass to the route, and either a redirection message or a bag of error messages.

#### Redirect to a named route

You can redirect to any other FluxBB page using it's route name:

```php
return $this->redirectTo('conversation', ['id' => $post->conversation_id], 'Post created');
```

The second parameter is an array of parameters that should be filled into the route URL. The third parameter can be used to send a message along with the redirect. This will be stored in the session and can be retrieved to display success messages to the user.

#### Redirect with errors

In case of invalid input (such as a post failing validation), you can create a redirect response that stores the bag of error messages instead of a success message:

```php
return $this->errorRedirectTo('new_post', ['conversation' => $post->conversation_id], $errors);
```
