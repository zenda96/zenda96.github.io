---
layout: display
title:  "mood全部文章"
categories: index
excerpt: "111"
---
<ul class="posts-ul">
{% for category in site.categories %}
        {% if category[0]=='mood' %}
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




