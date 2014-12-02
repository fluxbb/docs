# Request validators

By registering validators, we can validate input that is passed to [actions](actions.md).

## Creating validators

To create a new validator, extend the `FluxBB\Core\Validator` class and overwrite its abstract methods:

```php
class MessageValidator extends Validator
{
    protected function rules()
    {
        return [
            'title' => 'required|between:2,50',
            'text'  => 'required|min:20',
        ];
    }

    public function validate(Request $request)
    {
        $this->ensureValid($request->getParameters());
    }
}
```

The `rules()` method should return an array of validation rules.
Behind the scenes, this uses Laravel's validation component.
What you can do with these rules is thoroughly explained in the [Laravel documentation](http://laravel.com/docs/master/validation).

The `validate()` method receives a request object as an argument.
It should make sure the given request object contains valid data.
If the validation fails, it should throw an `Illuminate\Server\Exception\ValidationFailed` exception.

As validators will usually simply check an array of input data against a set of rules, the `ensureValid()` helper method exists to make this use-case super simple.
Just pass it an array, and it will validate it and throw an exception if the validation failed.

## Registering validators

Validators are small, reusable classes.
As such, they need to be registered with the request validator, which is implemented in `FluxBB\Server\RequestValidator`.
This class wraps the FluxBB server instance and, before passing on requests to their corresponding actions, makes sure they are valid.

Validators are registered in the server's service provider, `FluxBB\Server\ServerServiceProvider`.
In the `registerValidators()` method, validator classes are registered to be run before certain actions:

```php
$validator->registerValidator('edit.post', 'FluxBB\Validation\PostValidator');
```
