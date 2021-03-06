# jekyll-theme-codes
Code collection of jekyll theme used! (Jekyll模板定制时可能用到的一些代码)


# all posts style archive（时间倒序年份+文章列表输出）
```
<ul>
{% for post in site.posts %}
  {% capture y %}{{post.date | date:"%Y"}}{% endcapture %}
  {% if year != y %}
    {% assign year = y %}
    <h2>{{ post.date | date: '%Y' }}</h2> 
  {% endif %}
  <li>
	<h4><span>{{ post.date | date:"%Y-%m-%d" }}</span>&raquo;
	<a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></h4>
  </li> 
{% endfor %}
</ul>
```

# tags style archive（标签+文章列表输出）
```
{% for tag in site.tags %} 
	<a name="{{ tag[0] }}"></a><h3>{{ tag[0] }}({{ tag[1].size }})</h3>
	<ul>
	{% for post in tag[1] %}
		<li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
	{% endfor %}
	</ul>
{% endfor %}
```

# categories style archive（标目+文章列表输出）
```
<ul>
{% for cat in site.categories %} 
	{% if cat[0] != 'blog' %} 
   <a name="{{ cat[0] }}"></a>
   <h2>{{ cat[0] }}({{ cat[1].size }})</h2> 
     {% for post in cat[1] %} 
    <li><h4><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></h4></li>
	{% endfor %} 
   {% endif %} 
{% endfor %} 
</ul>
```

# posts of some catetory archive（特定栏目下所有文章列表）
```
<ul>
{% for post in site.categories.XXX %}
  {% capture y %}{{post.date | date:"%Y"}}{% endcapture %}
  {% if year != y %}
    {% assign year = y %}
    <h2>{{ post.date | date: '%Y' }}</h2> 
  {% endif %}
  <li>
	<h4><span>{{ post.date | date:"%Y-%m-%d" }}</span>&raquo;
	<a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></h4>
  </li> 
{% endfor %}
</ul>
```

# recent posts list（最近文章列表）
```
<ul>
{% for post in site.posts limit:10 %}
  <li>
	<a href="{{ post.url }}">
	  {{ post.title }}
	</a>
  </li>
{% endfor %}  
</ul>
```

# related posts of some one post（某文章的相关文章列表）
```
<ul>
{% for post in site.related_posts limit:10 %}
  <li>
	<a href="{{ post.url }}">
	  {{ post.title }}
	</a>
  </li>
{% endfor %}  
</ul>
```

# atom.xml rss文件生成代码(site用到的字段需要在_config.yaml中配置下)
```
---
layout: nil
title : Atom Feed
---
<?xml version="1.0" encoding="utf-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
 
 <title>{{ site.title }}</title>
 <link href="http://{{ site.domain }}/atom.xml" rel="self"/>
 <link href="http://{{ site.domain }}"/>
 <updated>{{ site.time | date_to_xmlschema }}</updated>
 <author>
   <name>{{ site.author }}</name>
   <email>{{ site.email }}</email>
 </author>

 {% for post in site.posts %}
 <entry>
   <title>{{ post.title }}</title>
   <link href="http://{{ site.domain }}{{ post.url }}"/>
   <updated>{{ post.date | date_to_xmlschema }}</updated>
   <id>{{ site.production_url }}{{ post.id }}</id>
   <content type="html">{{ post.content | xml_escape }}</content>
 </entry>
 {% endfor %}

</feed>
```
