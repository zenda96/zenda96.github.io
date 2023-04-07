---
layout: display
title:  "最新全部文章"
date:   2018-07-25 20:24:50 
categories: index
excerpt: "摘要摘要222"
---
<ul class="posts-ul">
{% for category in site.categories %}
        {% if category[0]=='newest' %}
            {% for post in category[1] %}
            <li><a href="{{post.url}}">{{post.title}}</a>
            <br>{{page.excerpt}}
            </li>
            {% endfor %}
        {% endif%}
{% endfor %}
</ul>




