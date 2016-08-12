---
layout: page
title: Blog
permalink: /bloglanding/
exclude : true
---

<div class="post-list">
    <ul>
        {% for post in site.posts %}
            <li>
                <a href="{{ post.url }}">
                    <title>{{ post.title }}</title>
                </a>
                <p>
                    {{ post.excerpt | remove: '<p>' | remove: '</p>' }}

                </p>
                
                <time>{{ post.date | date: '%B %d, %Y' }}</time>
            </li>
        {% endfor %}
    </ul>
</div> <!-- .post-list -->