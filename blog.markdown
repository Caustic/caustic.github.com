---
layout: default
---

I'm going to be using this blog to track my personal projects.  Less for the readers and more for myself to reference back to when I get stuck on something I've encountered before.  If you ended up here because you were having a similar issue, I hope you can find the help you need!  Cheers!

### Posts

<ul class="post-list">
  {% for post in site.posts %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a> <span>{{ post.date | date: "%B %e, %Y" }}</span>
  </li>
  {% endfor %}
</ul>
