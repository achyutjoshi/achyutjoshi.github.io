---
layout: page
title : Travel
permalink : /travel/
---
<!--
<div class="post-list">
    <ul>
        {% for post in  site.categories['travel'] %}
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
  
    {% for post in site.categories['travel'] %}

    <article class="post">
      <h4 class="post-title"><a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h4>

      <time datetime="{{ post.date | date_to_xmlschema }}" class="post-date">{{ post.date | date: '%B %d, %Y' }}</time>

      {{ post.content }}

      <hr>
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