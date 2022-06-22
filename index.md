## Posts


{% for tag in site.tags %}
  <h3>{{ tag[0] }}</h3>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.date | date: "%B %Y" }} - {{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}


[The Hacker Methodology](2022/04/11/The-Hacker-Methodology.html)

[Intro to Offensive Security](2022/04/12/Intro-to-Offensive-Security.html)

[Offensive Pentesting](2022/04/12/Offensive-Pentesting.html)

[Metasploit](2022/04/13/Metasploit.html)

[SQL Injection](2022/04/14/SQL-Injection.html)

[SQL Injection 2](2022/04/15/SQL-Injection-2.html)

