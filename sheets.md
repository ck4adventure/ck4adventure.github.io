<h2>Notes Sheets</h2>
<div class="row">

{% for page in site.sheets %}
<div class="cat-col">
	<ul>
    <li><a href="{{ page.url }}">{{ page.title }}</a></li>
	</ul>
</div>
{% endfor %}

</div>

