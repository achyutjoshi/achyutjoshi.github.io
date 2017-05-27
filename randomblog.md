---
layout: page
title : Random Scribblings
permalink : /randomblog/
---
<!--
<div class="post-list">
    <ul>
        {% for post in  site.categories['randomblog'] %}
            <li>
                <a href="{{ post.url }}">
                    {{ post.title }}
                </a>
                <time>{{ post.date | date: '%B %d, %Y' }}</time>
            </li>
        {% endfor %}
    </ul>
</div>
<br>
<br>

-->

<div class="home">

    {% for post in site.categories['randomblog'] %}

    <article class="post">
      <h4 class="post-title"><a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h4>
      <time datetime="{{ post.date | date_to_xmlschema }}" class="post-date">{{ post.date | date: '%B %d, %Y' }}</time>
      <br>

      {{ post.excerpt | remove: '<p>' | remove: '</p>' }}


    </article>
    {% endfor %}





    <!-- Pagination links -->
    <div class="pagination">
        {% if paginator.previous_page %}
            <a href="{{ paginator.previous_page_path }}" class="previous">Previous</a>
        {% else %}
            <span class="inactive previous">Previous</span>
        {% endif %}
        {% if paginator.next_page %}
            <a href="{{ paginator.next_page_path }}" class="next">Next</a>
        {% else %}
            <span class="inactive next">Next</span>
        {% endif %}
    </div>
</div>
