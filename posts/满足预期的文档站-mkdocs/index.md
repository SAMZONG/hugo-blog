# 满足预期的文档站 Mkdocs




## 组合三件套

- Mkdocs	# 热门的静态博客框架
- Mkdocs-material	# Mkdocs 颜值担当的主题
- MkDocs Awesome Pages Plugin   # Mkdocs 动态的 Navgation 插件



### 依赖的插件

```sh
pip install mkdocs 
pip install mkdocs-material 
pip install mkdocs-git-revision-date-plugin 
pip install mkdocs-mermaid2-plugin 
pip install mkdocs-rss-plugin 
pip install mkdocs-minify-plugin 
pip install mkdocs-macros-plugin 
pip install mkdocs-git-revision-date-localized-plugin 
pip install mkdocs-awesome-pages-plugin 
```



### Github repo

Private Teamplate https://github.com/SAMZONG/mkdocs-template



### Awesome Plugin 常用参数

> 在文档内的路径展示

~~~sh
```sh
docs
├── .pages.yaml     # 站点顶部导航配置文件，控制顺序和名称，一般不增加
├── README.md       # 默认情况下 目录下 README.md 作为 default 页面
├── SUMMARY.md
├── dce5.0          # 子文件夹，支持多级目录，自动检测配置
│   ├── .pages.yaml
│   ├── 01kpanda.md # 子文件自动检测，可以通过文件名前缀数字控制排序
│   ├── 02ghippo.md
│   ├── 03clusterpedia.md
│   ├── ...
├── design
│   ├── .pages.yaml # 每个目录下都有一个 `.pages.yaml` 用来进行目录的配置
│   ├── README.md
│   ├── ...
~~~



通过对每个文件下的特定处理，默认情况下 `.pages.yaml` 为空即可，如需要特殊处理，可以在文档添加下方参数:

```yaml
title: Products     # 文件夹展示的标题
order: 1            # 文件夹的顺序，数字越小越靠前
hide: false         # 是否隐藏，默认不隐藏
nav:                # 采用自定义导航
    - filename.md
    - filename2.md
    - ...
```

> `nav` 的配置方式，还有更多高级用法，可以参考插件做的的 Github 介绍 [传送门](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin#customize-navigation)



## mkdocs.yaml 的配置变更

1. 不要设定 `nav` OR `page`
2. 在 `plugin` 增加下方配置

```yaml
plugins:
  - awesome-pages:
       filename: .pages.yaml
       collapse_single_pages: true
       strict: false
```


