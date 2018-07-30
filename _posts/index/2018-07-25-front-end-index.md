---
layout: display
title:  "js全部文章"
date:   2018-07-25 20:24:50 
categories: index
excerpt: "摘要摘要222"
---
<ul class="posts-ul">
{% for category in site.categories %}
        {% if category[0]=='front-end' %}
            {% for post in category[1] %}
            <li>
                <div>
                     <a href="{{post.url}}">{{post.title}}</a>
                </div>
                {{post.digest}}
                <span class="post-date">{{ post.date | date_to_string }}</span>
            </li>
            {% endfor %}
        {% endif%}
{% endfor %}
</ul>



