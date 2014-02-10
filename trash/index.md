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
                <h2><a href="http://swinghu.github.com/ES6/" itemprop="url">ECMAScript 6系列</a><sup class="stick-top">TOP</sup></h2>
                <div class="title-desc" itemprop="description">
                    ECMAScript 6 是JavaScript的下一个标准，正处在快速开发之中，大部分已经完成了，预计将在2014年正式发布。
                </div>
        </li>
        <li itemtype="http://schema.org/Article">
                <h2><a href="http://swinghu.github.com/node/" itemprop="url">NodeJS 系列</a><sup class="stick-top">TOP</sup></h2>
                <div class="title-desc" itemprop="description">
                    JavaScript 在服务器端大放光彩，有必要花点功夫去研究。
                </div>
        </li>
		
		<li itemtype="http://schema.org/Article">
                <h2><a href="http://swinghu.github.com/ST/" itemprop="url">技术文档</a></h2>
                <div class="title-desc" itemprop="description">
                    技术规范文档清单
                </div>
        </li>
		
		<li itemtype="http://schema.org/Article">
                <h2><a href="http://swinghu.github.com/wiki.html" itemprop="url">Wiki - 知识库</a></h2>
                <div class="title-desc" itemprop="description">
                    Javascript,HTML & CSS,HTML5 & CSS3,前端相关,Python,正则表达式,开发相关,版本控制,系统相关,设计相关,VIM,其他
                </div>
        </li>
		
        </ul>
    </div>
    <div class="aside">
    </div>
</div>
