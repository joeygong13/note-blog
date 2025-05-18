---
title: Hugo 初步使用
date: 2025-05-17T00:07:00
summary: 开始 hugo 之路
tags: ["Hugo"]
categories: ["Hugo"]
lastmod: 2025-05-17T04:50:53.348Z
---
## 开启一个新工程

```bash
# create a new hugo project
hugo new site blog
# 打开本地开发模式服务
hugo server -D
```

刚开始的项目启动时，是没有任何页面的，因为你没有任何模板来渲染 md 文档，我们需要引入主题。可以手动新建，也可以使用别人写好的主题。

```bash
# 手动新建
hugo new theme mytheme

# 或者引入别人的主题，使用 git submodule，或者直接下载，然后放到 themes 目录下
# 这里使用 git，并使用该主题的 0.3.0 版本
git submodule add -b v0.3.0 git@github.com:dillonzq/LoveIt.git themes/LoveIt
```

然后配置自己的 `hugo.toml` 文件，添加 theme 配置

```toml
...
theme = 'LoveIt'
...
```

## 开始写文档

```bash
hugo new posts/first-article.md
```

创建了第一篇文档

### 模板

Hugo 创建模板时，是可以使用模板的，模板位于 `archetypes` 文件夹下，当该文件夹下有多个模板文件时，会按顺序使用，如，使用以下命令创建：

```sh
hugo new content posts/my-first-post.md
```

则模板的查找顺序为

1. `archetypes/posts.md`
2. `archetypes/default.md`
3. `themes/mytheme/archetypes/posts.md`
4. `themes/mytheme/archetypes/default.md`

模板中可以使用变量

| Var  | Description                                                |
| ---- | ---------------------------------------------------------- |
| Date | string 类型，当前的日期                                            |
| File | hugolib.fileInfo 类型，当前创建的文件信息                              |
| Type | string 类型，继承至 section 目录，或者使用 `hugo new content --kind` 传递 |
| Site | page.site，当前网站的对象                                          |

默认的模板文件：

```toml
+++
date = '{{ .Date }}'
draft = true
title = '{{ replace .File.ContentBaseName `-` ` ` | title }}'
+++
```

## 发布

文档写好后，把 `drfat` front matter 改为 true。

{{< admonition info >}}

在 hugo 中，文档的属性，即开头使用两个 `---` 或者 `+++` 包围的键值对内容，其中 `---` 使用的是 yaml 格式，`+++` 使用的是 toml 格式。

{{< /admonition >}}

这里我们使用 github 发布到 Cloudflare Pages 上。通过 github 集成 Cloudflare Pages，每次 github 提交后会触发 Pages 的自动构建（构建在 cloudflare，不是 github）。

注意在构建中添加变量 `HUGO_VERSION` 为你自己本地的 hugo 版本。
