---
layout: post
title: "Jekyll+github page搭建静态博客"
author: "ShiHaoyang"
---
<a name="icDfr"></a>

# 1 使用chripy模版搭建基本博客雏形

通过项目 [https://github.com/cotes2020/jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy) 搭建静态博客。直接在github应用模版创建github page。不过为了方便修改和调试，还是在本地对应clone。

1. 应用模版创建github page，按照getting startted执行即可
2. 将使用chirpy模版创建的github page项目git clone到本地
3. 安装所有需要的依赖

```bash
cd HaoyangShi.github.io
sudo bundle #因为安装bundle和jekyll使用sudo命令，后续在使用bundle和jekyll也需要使用sudo命令
```

4. 在本地运行

```bash
sudo bundle exec jekyll s
```

<a name="gL03Q"></a>

# 2 修改博客图标以及头像

按照 [https://chirpy.cotes.page/posts/customize-the-favicon/](https://chirpy.cotes.page/posts/customize-the-favicon/) 修改博客图标<br />但是博客home页的头像需要另外配置<br />通过分析官方网页源代码发现，头像配置在_config.yml，设置avatar为对应头像路径即可
<a name="LFfTt"></a>

# 3 修改博客文章作者显示

chripy项目将基本的配置[cotes2020](https://github.com/cotes2020)/[jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy)封装成一个包，在博客模版中import这个项目。所以在使用模版创建的静态博客项目中没有layout网页的具体内容，需要到jekyll-theme-chirpy项目中进行分析。<br />layout/post.html中关于作者部分如下：

```html
<!-- author(s) -->
    <span>
      {% if page.author %}
        {% assign authors = page.author %}
      {% elsif page.authors %}
        {% assign authors = page.authors %}
      {% endif %}

      {{ site.data.locales[site.lang].post.written_by }}

      <em>
      {% if authors %}
        {% for author in authors %}
          <a href="{{ site.data.authors[author].url }}">{{ site.data.authors[author].name }}</a>
          {% unless forloop.last %}</em>, <em>{% endunless %}
        {% endfor %}
      {% else %}
        <a href="{{ site.social.links[0] }}">{{ site.social.name }}</a>
      {% endif %}
      </em>
    </span>
```

表示每个博客页面解析当前是否定义作者。如果有说明，则显示在_data/authors.yml中记录的对应author的name，并链接到相应url；如果没有说明，则显示第一个社交链接的名字和对应url<br />所以在创建博客时，说明作者名。并创建_data/authors.yml文件，在其中添加相应记录
<a name="jD9I8"></a>

# 4 使用jekyll-compose发布博客

按照安装教程安装[https://github.com/jekyll/jekyll-compose](https://github.com/jekyll/jekyll-compose)，配置_config.yml