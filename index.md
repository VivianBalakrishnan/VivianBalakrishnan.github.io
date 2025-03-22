---
layout: default
---

<html>
<body>
      <div class="wrap">
      <iframe src="https://www.facebook.com/plugins/page.php?href=https%3A%2F%2Fwww.facebook.com%2Fvivian.balakrishnan.sg&tabs=timeline&width=500&height=500&small_header=true&adapt_container_width=false&hide_cover=false&show_facepile=false&appId" width="500" height="500" style="border:none;overflow:hidden" scrolling="no" frameborder="0" allowTransparency="true"></iframe>
      </div>
      
      

      <div class="wrap">
      <a class="twitter-timeline" href="https://twitter.com/VivianBala" data-tweet-limit="3">Tweets by VivianBala</a> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
      </div>
</body>
</html> 

<div class="home">

  <h1>Posts</h1>

  <ul class="posts">
    {% for post in site.posts %}
      <li>
        <span class="post-date">{{ post.date | date: "%b %-d, %Y" }}</span>
        <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>

  <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | prepend: site.baseurl }}">via RSS</a></p>

</div>
