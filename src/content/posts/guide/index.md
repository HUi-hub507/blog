---
title: 写博客指南
published: 2024-04-01
description: "How to use this blog template."
image: "./cover.jpeg"
tags: ["指南", "Blogging"]
category: Guides
draft: false Source
---

> Cover image source: [Source](https://image.civitai.com/xG1nkqKTMzGDvpLrqFT7WA/208fc754-890d-4adb-9753-2c963332675d/width=2048/01651-1456859105-(colour_1.5),girl,_Blue,yellow,green,cyan,purple,red,pink,_best,8k,UHD,masterpiece,male%20focus,%201boy,gloves,%20ponytail,%20long%20hair,.jpeg)

This blog template is built with [Astro](https://astro.build/). For the things that are not mentioned in this guide, you may find the answers in the [Astro Docs](https://docs.astro.build/).

## 格式要求

```yaml
---
title: My First Blog Post
published: 2023-09-09
description: This is the first post of my new Astro blog.
image: ./cover.jpg
tags: [Foo, Bar]
category: Front-end
draft: false
---
```

| Attribute     | Description                                                                                                                                                                                                 |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `title`       | 标题                                                                                                                                                                                      |
| `published`   | 发布时间                                                                                                                                                                       |
| `description` | 简单描述                                                     |
| `image`       | The cover image path of the post.<br/>1. Start with `http://` or `https://`: Use web image<br/>2. Start with `/`: For image in `public` dir<br/>3. With none of the prefixes: Relative to the markdown file |
| `tags`        | 标签                                                                                                                                                                                       |
| `category`    | 分类                                                         |
| `draft`        | 是否为草稿，                                                                                                                                          |

## 文章放在哪里

你的文章应该放在 `src/content/posts/` 目录中. 你也可以创建子文件夹来放其他文件。

```
src/content/posts/
├── post-1.md
└── post-2/
    ├── cover.png
    └── index.md
```
