---
layout: default
title: about
---
<div id="content" class="aboutMe">
<form class="page-loc" method="GET" action="/search">
	<span style="float:right"><input type="text" class="web-search" name ="q" value="站内搜索" /><a href="http://swinghu.github.com/atom.xml" class="page-rss" style="margin-left: 20px;">订阅</a></span>
  	swinghu's博客 » 关于我
</form>
<dl class="aboutDl">
	<dt><img src="{{ site.repo }}/images/mine.jpg" />关于作者</dt>
	<dd><strong>swinghu，</strong>Barret Lee</dd>
	<dd><strong>weibo:</strong><a href="http://weibo.com/u/1680100140" target="_blank">@coding_husiwen</a></dd>
	<dd><strong>blog:</strong><a href="http://hustskyking.cnblogs.com" target="_blank">博客园-BarretLee</a>（本博客部分文章会同步至博客园）</dd>
	<dd><strong>email:</strong><a href="mailto:barret.china@gmail.com">barret.china@gmail.com</a></dd>
	<dd><strong>自述:</strong>whu 13 级，特别喜欢钻研新技术，喜欢深入底层相关的技术，对服务端以及数据库 (MongoDB) 知识很感兴趣。行动方式是深入底层，积极思考。</dd>

	<dt>关于博客</dt>
	<dd>所有文章遵循的协议为「<a href="http://creativecommons.org/licenses/by-nc-sa/3.0/deed.zh" target="_blank">署名-非商业性使用-相同方式共享</a>」，由于文章表述或者内容可能存在诸多错误，所以部分内容会作修改，为保证转载信息与源保持同步，转载请注明文章出处！谢谢合作 :）</dd>

	<dt>好友链接</dt>
	<dd>
        <div class="friend-link">
            <a href="http://http://ilovers.sinaapp.com/" title="http://http://ilovers.sinaapp.com/" target="_blank">李文琼</a>
            <a href="http://hrwang.me/" title="http://hrwang.me/" target="_blank">王浩然的Blog</a>
            <a href="http://winares.github.io" title="http://winares.github.io" target="_blank">刘晓的Blog</a>
			<a href="http://www.iteblog.com" title="http://www.iteblog.com" target="_blank">吴阳平的Blog</a>
        </div>
   </dd>
</dl>
{% include disqus.snippet %}
<div class="footer">
    <small>Powered by <a href="https://github.com/mojombo/jekyll">Jekyll</a> | Copyright 2013 - 2023 Designed by <a href="http://barretlee.com/about.html">Barret Lee</a> | <span class="label label-info">{{site.time | date:"%Y-%m-%d %H:%M:%S %Z"}}</span></small>
</div>
</div>
<script type="text/javascript">
$(function(){
	$('#disqus_container .comment').trigger('click');
});
</script>