---
layout: default
title: Red Team
---

<div id="blog-AD">

	{% for ad in site.categories.RT %}
		<article class="ad">
			{% if ad.external-url %}
				<h1>
					<a href="{{ ad.external-url }}">{{ ad.title }}</a> 
					<a class="anchor" href="{{ ad.url }}"></a>
				</h1>
			{% else %}
				<h1><a href="{{ ad.url }}">{{ ad.title }}</a></h1>
			{% endif %}
		</article>
	{% endfor %}

</div>
