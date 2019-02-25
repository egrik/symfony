# Bundles

## How to Override any Part of a Bundle

###Templates
Шаблоны с бандла _<bundle>/Resources/views/_ копируем в _<your-project>/templates/bundles/<bundle-name>/_.
Так же необязательно полностью копировать шаблон, в некоторых иногда будет достаточно его расширить:
```yaml
{# templates/bundles/FOSUserBundle/Registration/confirmed.html.twig #}
{# the special '!' prefix avoids errors when extending from an overridden template #}
{% extends "@!FOSUserBundle/Registration/confirmed.html.twig" %}

{% block some_block %}
    ...
{% endblock %}
``` 