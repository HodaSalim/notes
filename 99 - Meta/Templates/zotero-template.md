Title: {{title}}-{{date | format("YYYY")}}
Author: {{authors}}
Zotero Link: {{pdfZoteroLink}}

> [!NOTE]- Abstract
> {{abstractNote}}

{% persist "annotations" %}
{% set newAnnotations = annotations | filterby("date","dateafter", lastImportDate) %}
{% if newAnnotations.length > 0 %}
**Imported: {{importDate | format("YYYY-MM-DD")}}**
{% for a in newAnnotations %}
{% if a.comment %}{{a.comment}}{% endif %}{% if a.annotatedText %} "{{a.annotatedText}}" {% endif %}
{%- if a.imageRelativePath %} ![[{{a.imageRelativePath}}]] {%- endif %} [Page{{a.page}}]({{a.desktopURI}})
{% if a.hashTags %}{{a.hashTags}}{% endif %}

{% endfor %}
{% endif %}
{% endpersist %}