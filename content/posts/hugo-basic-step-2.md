+++
date = '2025-05-18T10:50:35+08:00'
title = 'Hugo 的页面'
tags = ['hugo']
categories = ['hugo']
summary = 'Hugo 中的页面有多种类型，如文档 Page, 章 Section，如果想自己修改些页面样式的话，需要了解 Hugo 的渲染模板机制。'
+++

```text
layouts/
├── _default/
│   ├── _markup/
│   │   ├── render-image.html   <-- render hook
│   │   └── render-link.html    <-- render hook
│   ├── baseof.html
│   ├── home.html
│   ├── section.html
│   ├── single.html
│   ├── taxonomy.html
│   └── term.html
├── articles/
│   └── card.html               <-- content view
├── partials/
│   ├── footer.html
│   └── header.html
└── shortcodes/
    ├── audio.html
    └── video.html
```

## 页面类型

[Template Config](https://gohugo.io/templates/types/)

### 1. 首页 Home

使用模板 `layouts/_default/index.html` 渲染

### 2. 章节页 Section

在 Hugo 中，content 文件夹下的每个子目录是一个 section，或者包含 `_index.md` 的目录为 section。

section 页的作用为展示该文件夹下的所有文章。使用 `layouts/_default/section.html` 渲染。

### 3. 文档页 Single

渲染文档，默认使用 `layouts/_default/single.html`，但当 layouts 有 `<section>/single.html` 时，则优先使用该模板。

### 4. 分类页 Term

hugo 默认启用 tags, category 分类，其中 tags 就叫做一个 term。在文档中使用 tags、categories 等 front matter 进行配置即可。

使用 `layouts/_default/term.html` 进行渲染。

### 5. list

通用列表页，在渲染列表时，如每个章节 section，或者某个 tag 下需要展示关联的所有文章，默认使用 `layouts/_default/list.html`。但该页优先级是最低的，是一个回退模板。优先使用上面的 `term` 或者 `section` 自带的模板
