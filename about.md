---
layout: default
title: about
---
<div id="content" class="aboutMe">
<form class="page-loc" method="GET" action="/search">
	<span style="float:right"><input type="text" class="web-search" name ="q" value="站内搜索" /><a href="http://swinghu.github.com/atom.xml" class="page-rss" style="margin-left: 20px;">订阅</a></span>
  	swinghu的博客 » 关于我
</form>
<dl class="aboutDl">
	<dt><img src="/images/mine.jpg" />关于作者</dt>
	<dd><strong>swinghu，</strong>husiwen </dd>
	<dd><strong>weibo:</strong><a href="http://weibo.com/u/1680100140" target="_blank">@coding_husiwen</a></dd>
	<dd><strong>blog:</strong><a href="http://blog.csdn.net/jxusthusiwen" target="_blank">csdn博客园-</a>（本博客部分文章会同步至博客园）</dd>
	<dd><strong>email:</strong><a href="mailto:ogrecpp@gmail.com">ogrecpp@gmail.com</a></dd>
	<dd><strong>自述:</strong>WHUer,特别喜欢钻研新技术，对服务器端开发,linux,服务端 (NodeJS),Go,Lua,以及数据库 (MongoDB) 知识很感兴趣。行动方式是底层再底层思考，创新再创新实践。</dd>

	<dt>关于博客</dt>
	<dd>所有文章非特别说明皆为原创，遵循的协议为「<a href="http://creativecommons.org/licenses/by-nc-sa/3.0/deed.zh" target="_blank">署名-非商业性使用-相同方式共享</a>」，由于文章表述或者内容可能存在诸多错误，所以部分内容会作修改，为保证转载信息与源同步，转载请注明文章出处！谢谢合作 :）</dd>

	<dt>好友链接</dt>
	<dd>
        <div class="friend-link">
        	<a href="http://www.iteblog.com/" title="http://www.iteblog.com/" target="_blank">过往记忆'Blog||  </a>
            <a href="http://hrwang.cc/" title="http://hrwang.cc/" target="_blank">王浩然的Blog||  </a>
            <a href="http://winares.github.io/" title="http://winares.github.io/" target="_blank">刘晓的Blog||  </a>
            <a href="http://ilovers.sinaapp.com/" title="http://ilovers.sinaapp.com/" target="_blank">李文琼的Blog|| </a>
			<a href="http://blog.sina.com.cn/drpickup" title="http://blog.sina.com.cn/drpickup" target="_blank">郑匡宇-台湾型男|| </a>
			<a href="http://www.yangzhiping.com/" title="http://www.yangzhiping.com/" target="_blank"> 阳志平-心智实验室 </a>
        </div>
   </dd>
</dl>
{% include disqus.snippet %}
<div class="footer">
    <small>Powered by <a href="https://github.com/mojombo/jekyll">Jekyll</a> | Copyright 2013 - 2023 Designed by <a href="http://swinghu.github.com/about.html">swinghu</a> | <span class="label label-info">{{site.time | date:"%Y-%m-%d %H:%M:%S %Z"}}</span></small>
</div>
</div>
<script type="text/javascript">
$(function(){
	$('#disqus_container .comment').trigger('click');
});
</script>
