---
layout: page
title: Thoughts on science and random things
tagline: 
---
{% include JB/setup %}

*If you're looking for my group's website, see the [GERMS lab](http://germslab.org).*

Recent posts:

<ul >
    {% for post in site.posts limit 4 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
        {{ post.content | strip_html | truncatewords:100}}<br>
            <a href="{{ post.url }}">Read more...</a><br><br>
    {% endfor %}
</ul>

<a href="feed.xml">Subscribe to RSS Feed</a>
