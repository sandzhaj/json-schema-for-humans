**Пример{% if examples|length > 1 %}ы{% endif %}:**{{ " " }}

{% for example in examples %}
{% set example_id = schema.html_id ~ "_ex" ~ loop.index %}
```json
{{ example }}
```
{% endfor %}