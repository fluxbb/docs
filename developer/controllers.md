# Controllers

Here be the explainin'.

## Response types

Responses are usually HTML responses. FluxBB uses a view system for assembling and rendering HTML templates. For transactional actions (login, posting etc.), the user often needs to be redirected.

### HTML responses
Views can be returned using the `view()` method, which accepts a view name and optionally an array of data that should be available in the template.

### Redirects
Both after successful and failing actions, we may want to direct the user to another place in our application. Two methods exist to do so: `redirect()` and `errorRedirect()`. Both have similar signatures: a route name, an array of parameters to pass to the route, and either a redirection message or a bag of error messages.
