---
layout: home
---

<div class="index-content trash">
    <div class="section">
        <ul class="artical-cate">            
			<li><a href="/"><span>Blog</span></a></li>
            <li ><a href="/opinion"><span>Opinion</span></a></li>
            <li ><a href="/project"><span>Project</span></a></li>
			<li class="on" ><a href="/trash"><span>Trash</span></a></li>
		
        </ul>

        <div class="cate-bar"><span id="cateBar"></span></div>

        <ul class="artical-list">
        {% for post in site.categories.trash %}
            <li>
                <h2>
                    <a href="{{ post.url }}">{{ post.title }}</a>
                </h2>
                <div class="title-desc">{{ post.description }}</div>
            </li>
        {% endfor %}
		
		<li itemtype="http://schema.org/Article">
                <h2><a href="http://barretlee.com/wiki.html" itemprop="url">Wiki - 知识库</a></h2>
                <div class="title-desc" itemprop="description">
                    Javascript,HTML & CSS,HTML5 & CSS3,前端相关,Python,正则表达式,开发相关,版本控制,系统相关,设计相关,VIM,其他
                </div>
        </li>
		
        </ul>
    </div>
    <div class="aside">
    </div>
</div>
