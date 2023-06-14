---
layout: default
---

{% assign tag = "network" %}
{% assign tagged_posts = "" | split: "" %}
{% for post in site.posts %}
  {% if post.tags contains tag %}
    {% assign tagged_posts = tagged_posts | push: post %}
  {% endif %}
{% endfor %}


<article>
    {% include header.html %}
    <main>
      <h1 class="post-title">Tagged #{{ tag }}</h1>
      {% assign postsByYearMonth = tagged_posts | group_by_exp: "post", "post.date | date: '%B %Y'" %}

        <div class="archive">
        {% for yearMonth in postsByYearMonth %}
        <h2>{{ yearMonth.name }}</h2>
        <ul>
            {% for post in yearMonth.items %}
            <li><a href="{{ post.url }}">{{ post.title }}.</a> <span class="lead">{{ post.lead }}</span></li>
            {% endfor %}
        </ul>
        {% endfor %}
        </div>
    </main>
    {% include tagcloud.html %}
    {% include footer.html %}
  </article>
