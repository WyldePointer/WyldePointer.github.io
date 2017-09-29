#### C programming language tutorials
<ul>
{% for post in site.categories.c-language-tutorials reversed %}
  <li>
    <a href="{{ site.baseurl }}{{ post.url }}">Part
 {% increment counter %}: {{ post.title }}</a>
  </li>
{% endfor %}
</ul>
<br />
#### All blog posts
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

Contact:
```sh
$ echo "moc.liamg@derafnom.barhos" | rev
```
