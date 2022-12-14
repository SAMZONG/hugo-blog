---
title: Awesome Hexo Plugin
toc: true
abbrlink: 52483
date: 2022-03-27 21:45:17
tags:
  - Hexo
categories:
  - Blog
  - Hexo
---

About my blog use hexo plugin

## hexo-tag-youtube-responsive

[hexo-tag-youtube-responsive](https://github.com/quocvu/hexo-tag-youtube-responsive) is Hexo tag plugin to embed a Youtube video that auto resizes with your responsive layout

### Install

```shell
npm install hexo-tag-youtube-responsive --save
```

### Embed a video

```
  {% youtuber video VIDEO_ID %}
  {% endyoutuber %}
```

For example

```
  {% youtuber video I07XMi7MHd4 %}
  {% endyoutuber %}
```

### Embed a playlist

```
  {% youtuber playlist PLAYLIST_ID %}
  {% endyoutuber %}
```

For example

```
  {% youtuber playlist PLC77007E23FF423C6 %}
  {% endyoutuber %}
```

Note that you need to prepend the playlist ID with the letters PL as shown above

### Demo

{% youtuber video I07XMi7MHd4 %}
{% endyoutuber %}


## hexo-hide-posts

[hexo-hide-posts](https://github.com/prinsss/hexo-hide-posts) is A plugin to hide specific posts from your Hexo blog and make them only accessible by links

### Installation

``` bash
$ npm install hexo-hide-posts --save
```

Usage

Add `hidden: true` to the [front-matter](https://hexo.io/docs/front-matter) of posts which you want to hide.

e.g. Edit `source/_posts/lorem-ipsum.md`:

```text
---
title: 'Lorem Ipsum'
date: '2019/8/10 11:45:14'
hidden: true
---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

This post will not be shown anywhere, but you can still access it by `https://hexo.test/lorem-ipsum/`. (If you want to completely prevent a post from rendering, just set it as a [draft](https://hexo.io/docs/writing.html#Drafts).)

To get a list of hidden posts, you can run `hexo hidden:list` from command line.

For developers, `all_posts` and `hidden_posts` added to [Local Variables](https://hexo.io/api/locals) may be useful.

### Config

In your site's `_config.yml`:

```yml
# hexo-hide-posts
hide_posts:
  enable: true
  # Change the filter name to fit your need
  filter: hidden
  # Generators which you want to expose all posts (include hidden ones) to.
  # Common generators: index, tag, category, archive, sitemap, feed, etc.
  public_generators: []
  # Add "noindex" meta tag to prevent hidden posts from being indexed by search engines
  noindex: true
```


## hexo-generator-restful

[hexo-generator-restful](https://github.com/yscoder/hexo-generator-restful) is generate restful json data for Hexo plugins.

### Install

```bash
npm install hexo-generator-restful --save
```

### Config

???????????????????????????????????? `false` ??????????????????

```yml
restful:
  # site ?????????????????????????????????????????????
  # site: ['title', 'subtitle', 'description', 'author', 'since', email', 'favicon', 'avatar']
  site: true        # hexo.config mix theme.config
  posts_size: 10    # ?????????????????????0 ???????????????
  posts_props:      # ???????????????????????????????????????
    title: true
    slug: true
    date: true
    updated: true
    comments: true
    path: true
    excerpt: false
    cover: true      # ????????????????????????????????????
    content: false
    keywords: false
    categories: true
    tags: true
  categories: true         # ????????????
  use_category_slug: false # Use slug for filename of category data
  tags: true               # ????????????
  use_tag_slug: false      # Use slug for filename of tag data
  post: true               # ????????????
  pages: false             # ????????? Hexo ????????????, ??? About
```

### Get Hexo Config

???????????? Hexo ??????????????????????????????????????????

> Request

```
GET /api/site.json
```

> Response

[/api/site.json](https://samzong.me/api/site.json)

### Get Posts

???????????? `posts_size: 0` ???????????????????????????????????????????????????

> Request

```
GET /api/posts.json
```

> Response

????????????????????????????????????????????????????????? `total`???`pageSize`???`pageCount`??????????????????????????????????????????

[/api/posts.json](https://samzong.me/api/posts.json)