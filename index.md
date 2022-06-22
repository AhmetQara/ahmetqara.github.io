{% for tag in site.tags %}
  <h1>Posts</h1>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.date | date: "%B %d, %Y" }} - {{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}

[Blog - All in One](https://ahmetqara.github.io/blog/index.html)
