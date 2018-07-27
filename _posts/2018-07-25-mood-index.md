---
layout: display
title:  "mood全部文章"
date:   2018-07-25 20:24:50 
categories: index
excerpt: "111"
---
<ul class="posts-ul">
{% for category in site.categories %}
        {% if category[0]=='mood' %}
            {% for post in category[1] %}
            <li><a href="{{post.url}}">{{post.title}}</a>
            <br>{{page.excerpt}}
            </li>
            {% endfor %}
        {% endif%}
{% endfor %}
</ul>




