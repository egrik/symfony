# Templating

## Linking to Assets

Ссылки на ассеты
```twig
<img src="{{ asset('images/logo.png') }}" alt="Symfony!" />
<link href="{{ asset('css/blog.css') }}" rel="stylesheet" />
```

Абсолютные ссылки
```twig
<img src="{{ absolute_url(asset('images/logo.png')) }}" alt="Symfony!" />
```

Подключение encore ассетов
```twig
{% block stylesheets %}
    {{ encore_entry_link_tags('app') }}
{% endblock %}

{% block javascripts %}
    {{ encore_entry_script_tags('app') }}
{% endblock %}
```