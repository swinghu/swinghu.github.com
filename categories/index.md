---
title: Categories
layout: single
NotLoadComment: true
---

<div class="categories">
	<div class="cate-title">
	{% for cat in site.categories %}
		<a href="#{{ cat[0] }}" title="{{ cat[0] }}" rel="{{ cat[1].size }}">{{ cat[0] | capitalize }} <sup>({{ cat[1].size }})</sup></a>
	{% endfor %}
	</div>

	<ul class="cate-list">
	{% for cat in site.categories %}
	  <h3 id="{{ cat[0] }}">{{ cat[0] | capitalize  }}</h3>
		{% for post in cat[1] %}
			<li>
				<time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date_to_string }}</time> » 
				<a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
			</li>
		{% endfor %}
	{% endfor %}
	</ul>
</div>