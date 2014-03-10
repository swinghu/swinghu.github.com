
<html>

  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="http://netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css">
    <link href="http://netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap-theme.min.css" rel="stylesheet">
    <link href="theme.css" rel="stylesheet">   
      
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>
    <script src="http://netdna.bootstrapcdn.com/bootstrap/3.0.0/js/bootstrap.min.js"></script>
    <script src="http://cdn.bootcss.com/twitter-bootstrap/3.0.3/js/bootstrap.min.js"></script>
    <script> 
// Set the height of a carousel to the height of its maximum item, and
// vertically center all the items.
var setCarouselHeight = function(carousel) {
  var items = $('.item', carousel);
  var heights = items.get().map(function(item) { return $(item).height() });
  var maxHeight = Math.max.apply(null, heights);
  $('.carousel-inner', carousel).height(maxHeight);
  items.get().forEach(function(item) {
    var padding = (maxHeight - $(item).height())/2;
    $(item).css('padding-top', padding);
    $(item).css('padding-bottom', padding);
  });
};

// Randomly sort an element's children.
var shuffleChildren = function(el) {
  var shuffledChildren = el.children().sort(function() { return 0.5 - Math.random() });
  el.empty();
  el.append(shuffledChildren);
  return el;
}

$(function() {
  // Shuffle carousel items
  var carousel = $('#quotesCarousel');
  shuffleChildren($('.carousel-inner', carousel));
  $('.item:first', carousel).addClass('active');
  carousel.carousel(0);
  // don't want above line to animate, so defer adding the 'slide' class to the
  // carousel until now
  carousel.addClass('slide');

  // Set up quote ellision/expansion
  var expandQuote = function() {
     $(this).hide();
     $(this).next().fadeIn();
     setCarouselHeight(carousel);
     return false;
  }
  $('.ellide').before($('<a href="#">[...]</a>').click(expandQuote));
  $('.ellide').css('display', 'none');

  // Set carousel height
  $(window).resize(function() { setCarouselHeight(carousel) });
  setCarouselHeight(carousel);
});

// Reorder implementations based on github stars and last update.
$(function() {
  $.getScript('https://ramcloud.stanford.edu/~ongaro/raft/repos.jsonp',
                  function() {
    var repos = raft_repos();
    var impltable = $('#implementations');
    var implrows = $('tbody tr', impltable);
    implrows.each(function(i, row) {
      var url = $('td:first a', row).prop('href');
      if (url in repos) {
        repos[url].row = row;
      }
    });
    var repos_list = [];
    $.each(repos, function(url, repo) {
      repos_list.push({url: url, repo: repo});
    });
    repos_list.sort(function(i, j) { return i.repo.rank - j.repo.rank; })
    repos_list.forEach(function(repow) {
      impltable.prepend(repow.repo.row);
    });
  });
});
    </script>

<style>
blockquote p {
  font-size: inherit;
}
.carousel {
  margin-left: auto;
  margin-right: auto;
}
/* gray box around quotes */
.carousel .item blockquote {
  width: 70%;
  border-left: none;
  margin-left: auto;
  margin-right: auto;
  margin-top: 0;
  margin-bottom: 0;
  background-color: #f5f5f5;
  border-radius: 5px;
}
.carousel-control.left, .carousel-control.right {
  background: none;
  color: black;
}
/* get rid of ants in firefox */
a:active.carousel-control,
a:focus.carousel-control  {
  outline: none;
}
/* slide arrows up a bit so they're centered */
.carousel-control .glyphicon {
  margin-top: -13px;
}

#quotesCarousel {
  max-width: 800px;
}
#quotesCarousel blockquote a {
  color: inherit;
}
    </style>

    <title>Raft Consensus Algorithm</title>
  </head>

  <body>

    <!-- HEADER -->
    <div class="container page-header">
          <h1 >swinghu'english resume </h1>
    </div>
    <div class="container" style="border-bottom: 1px solid #eeeeee; padding-bottom: 20px; margin-bottom: 20px;">
<div id="quotesCarousel" class="carousel" data-interval="false">
    <div class="carousel-inner">

<!--
These are meant to be quotes of my resume

More quotes go here:
 - Copy a <div class="item">...</div> block below.
 - Newer quotes go on top.
 - Use <strong> for emphasis.
-->

<div class="item">
<blockquote>

<p>
We built a key piece of <strong>InfluxDB, a distributed time series
database</strong>, on top of Raft. Specifically, the go-raft implementation,
which follows the paper very closely. We're using Raft for <strong>consensus
and replication of key cluster metadata</strong>. We're planning on using
Raft's leader model to make monitoring key database background processes
easier. InfluxDB is still an early project, but production deployments are
planning for January/February of 2014 and Raft is an essential part of the
architecture.
</p>

<small>
  <a href="https://twitter.com/pauldix">Paul Dix</a>,
  <a href="http://influxdb.org/">InfluxDB</a> and
  <a href="https://errplane.com/">Errplane</a>
</small>
<!-- Personal communications with Diego Ongaro, 2013. -->
</blockquote>
</div>

<div class="item">
<blockquote>

<p>
When I started looking for ways to distribute <strong><a href="http://skydb.io">Sky</a></strong>, my open source behavioral analytics database, Paxos was the standard.
I spent weeks trying to understand the protocol and how it applied to distributing a database log.
</p>

<p>
On the recommendation of a friend I checked out the Raft paper and <strong>it immediately made sense</strong>.
The central tenets of leader election and log replication fit perfectly with the needs of my project.
</p>

<p>
There were no Go implementations at the time so I wrote go-raft.
Sky is currently in the process of integrating go-raft for the purpose of managing the cluster configuration and database schema as well as replicating the raw data itself.
Not only has it helped tremendously in my project but I've seen a huge interest from other people who use it in their own projects.
</p>
<small>
  <a href="https://twitter.com/benbjohnson">Ben Johnson</a>,
  <a href="http://skydb.io">Sky</a>
</small>
<!-- Pull request from Ben Johnson, 2013. -->
</blockquote>
</div>

<div class="item">
<blockquote>

<p>
<strong>At 15below we use Raft as an central component in a distributed micro
service hosting and management platform.</strong> Micro services form an
essential part of our future architectural strategy and this 'platform' is our
approach for managing large numbers of small business services.
</p>

<p>
<strong>Raft's primary use is for distributing the cluster deployment state and
designating the cluster leader.</strong> The 'strong leader' properties of Raft
was one of our primary reasons for choosing it as it aligned nicely with our
requirement for allowing the hosting platform to make autonomous deployment
decisions.
</p>

<p>
We decided to create <strong>our own implementation of Raft</strong> as on the
.NET stack there were no mature options at the time. It is <strong>implemented
in the F# language</strong> and is pretty close to what is described in the
Raft paper. <span class="ellide"> Log replication, leader elections, cluster
configurations changes and log persistence are all fully implemented. The only
thing missing currently is log compaction but that is in the works. One notable
difference is that we chose to use asynchronous messaging instead of RPC which
meant we had to make a few smaller amendments to get the same behaviour as
described in the paper.</span>
</p>

<p>
It isn't open source yet but 15below has a good history of supporting open
source and we are confident that at least the Raft implementation will be made
open source in the near future once it has been proven in production.
</p>
<small>
  <a href="https://twitter.com/kjnilsson">Karl Nilsson</a>,
  <a href="http://15below.com">15below</a>
</small>
<!-- Personal communications with Diego Ongaro, 2013. -->
</blockquote>
</div>

<div class="item">
<blockquote>
<p>
We built a core piece of CoreOS, a service discovery and locking service called
etcd, on Raft. An etcd cluster will be <strong>essential to a full CoreOS
deploy</strong> and can be used for service discovery between application
containers and for organizing containers across machines. Etcd is a new project
but our customers and the open source community as a whole are excited about
the problems it can help solve for large server deployments.
</p>

<p>
Raft was used for etcd because it was easy to implement and straightforward to
explain. <strong>We built etcd on the go-raft library</strong> and contribute
significantly to the library. go-raft follows the Raft paper closely and aims
to be a feature complete implementation.
</p>
<small>
  <a href="https://twitter.com/BrandonPhilips">Brandon Philips</a>,
  <a href="http://coreos.com">CoreOS</a>
</small>
<!-- Personal communications with Diego Ongaro, 2013. -->
</blockquote>
</div>
<a class="left carousel-control" href="#quotesCarousel" data-slide="prev">
<span class="glyphicon glyphicon-chevron-left"></span>
</a>
<a class="right carousel-control" href="#quotesCarousel" data-slide="next">
          <span class="glyphicon glyphicon-chevron-right"></span>
 </a>
      </div> <!-- end carousel -->
    </div> <!-- end carousel container -->
</div>
      
      
<div class="list-group">
        <a class="list-group-item active">
        <h4 class = "list-group-item-heading">PERSONAL DETAILS</h4>
        <p class="list-group-item-text"><strong>Name</strong>		: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	Hu si wen<br>
           <strong> Gender</strong>		:	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;male<br>
            <strong>Date of Birth</strong>	:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	11-9-1988<br>
            <strong>Cell Phone</strong>	:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 	13212776163<br>
            <strong>Email</strong>		:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 	ogrecpp@gmail.com<br>
            <strong>Location</strong>		:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	Hubei<br>
            <strong>Hukou</strong>		:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	Hubei<br>
            <strong>Degree</strong>	:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	Master(Now attending)<br>
            <strong>English</strong>		:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	CET6<br>
            </p>
        </a>
          
    </div>
      
    <div class="list-group">
        <a class="list-group-item active">
        <h4 class = "list-group-item-heading">TECHINIAL QUALIFIED SKILLS SUMMARY</h4>
        <p class="list-group-item-text"><strong>OS</strong> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  Windows, Linux<br>
            <strong>Languages and Skill</strong> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    Java, C/C++,win32,MFC,Lua,DirectX,CEGUI,OGRE,Matlab<br>
            <strong>Database</strong> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 			mysql,MongoDB<br>
            <strong>Network</strong> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 				TCP/IP, Socket<br>
            <strong>Tools</strong> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 		   		Visual Studio 2008, Flash Builder 4.5<br>

            </p>
            </a>
    </div>
      
      <div class="list-group">
       <a class="list-group-item active">
        <p>
            <h1 id="professional-experiences">PROFESSIONAL EXPERIENCES</h1>
<p><em>Shenzhen 8zgame Co. Ltd.<br>February.2012-May.2012<br>Main Role:     Software Engineer</em><br><strong>Project1</strong>            <em>Ling Jian Qing Yuan (3D mmorpg ,Chinese name:灵剑情缘)</em><br><strong>Period:</strong>            February.2012-May.2012<br><strong>Project Role:</strong>        Software Engineer<br><strong>Technical Platform:</strong>  C++, Lua, windows<br><strong>Tools:</strong>            Visual Studio 2005<br><strong>Project Info:</strong>Ling Jian Qing Yuan is a 2.5D mmorpg, turn_based online game,which developed by  Shenzhen 8zgame Co. Ltd.<br><strong>Responsibilities:</strong><br>Participate in the design and development coordination of the online game at the server-side,and to develop an OSS system, which mainly to ensure that the Virtual Money, resources in the game be well rencorded and stored in the MS SQL database.<br>Work at the server-side ,mainly write C++ and Lua script languages in platform Visual Studio 2008 </p>
<p><em>Shenzhen 7road Co. Ltd.<br>Jul.2012- Jun.2012<br>Main Role:     System Software Engineer</em><br><strong>Project            </strong>The Divine Comedy (web game,Chinese name: 神曲)<br><strong>Period:    </strong>        May.2012-October.2012<br><strong>Project Role:</strong>        System Software Engineer.<br><strong>Technical Platform:</strong>  Windows server 2008<br><strong>Tools:</strong>            Flash Builder 4.5, Flash ActionScript 3.0<br><strong>Project Info:</strong> &quot;The Divine Comedy&quot;, is a webpage game, which developed by 7road Co. Ltd.<br><strong>Responsibilities:</strong><br>Participate in developing and Optimizating the MapEditor,a map tool used in the Sheng Qu and Dangdang Tang web game.<br>Participate in developing and learning the main module of game engine the company </p>
<h1 id="education">EDUCATION</h1>
<p>Wuhan University      Sep.2013- now<br>Master in Computer Science and Technology (Now attending)</p>
<h1 id="award">Award</h1>
<p>The 2010 CUMCU Contest, our team(three member) won the national CUMCU contest second prize.</p>

           
           </p>
        </a>
      </div>
     
        
  </body>
</html>