---
layout: default
---

So I guess I'm going to try to start a blog again.  We'll see how this goes.

### Posts

<ul class="post-list">
  {% for post in site.posts %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a> <span>{{ post.date | date: "%B %e, %Y" }}</span>
  </li>
  {% endfor %}
</ul>
