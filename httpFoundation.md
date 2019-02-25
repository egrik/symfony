# The HttpFoundation Component

## Session

Для избежания автостарта сессий для анонимных пользоватлей, испозовать метод **hasPreviousSession**
```twig
{# this check prevents starting a session when there are no flash messages #}
{% if app.request.hasPreviousSession %}
    {% for message in app.flashes('notice') %}
        <div class="flash-notice">
            {{ message }}
        </div>
    {% endfor %}
{% endif %}
```

## Forward request to another controller
```php
$response = $this->forward('App\Controller\OtherController::fancy', [
    'name'  => $name,
    'color' => 'green',
]);
```
