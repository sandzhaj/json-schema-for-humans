{% for sub_property in schema.iterate_properties %}
  {%- if sub_property.is_additional_properties and not sub_property.is_additional_properties_schema -%}
    {% continue %}
  {% endif %}

  {% set html_id = sub_property.html_id %}

  {% set description = sub_property | get_description %}
<details>
<summary>
    {% filter md_heading(depth + 1, html_id, True) -%}
      {%- filter replace('\n', '') -%}
    {%- if sub_property is deprecated  -%}~~{%- endif -%}
    {%- if sub_property.is_pattern_property %}Паттерн{% endif %} {% with schema=sub_property %}{%- include "breadcrumbs.md" %}{% endwith %}
    {%- if sub_property is deprecated -%}~~{%- endif -%}
    {%- endfilter %}
  {%- endfilter %}
  
  {% if sub_property.is_pattern_property %}
> Вложенные объекты могут иметь любое имя, которое соответствует
```{{ sub_property.property_name }}```
  {% endif %}

</summary>
<blockquote>

  {% with schema=sub_property, skip_headers=False, depth=depth+1 %}
    {% include "content.md" %}
  {% endwith %}

</blockquote>
</details>

{% endfor %}