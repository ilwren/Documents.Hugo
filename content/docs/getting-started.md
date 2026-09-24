---
title: 快速开始
weight: 1
next: /docs/guide/code-highlight/
---

## 安装

本站点使用 [Hugo](https://gohugo.io/)(extended 版本,>= 0.146.0)构建。

```bash
# 本地开发预览(带热重载)
hugo server -D

# 生产构建(生成 public/ 静态文件)
hugo --gc --minify
```

## 目录结构

```text
hugo-docs-site/
├── hugo.yaml           # 站点配置
├── content/            # Markdown 内容
│   ├── _index.md       # 首页
│   └── docs/           # 文档章节
├── themes/hextra/      # 主题(本地目录,离线可用)
└── public/             # 构建产物(部署这个目录即可)
```

## 新增一篇文档

在 `content/docs/` 下新建一个 `.md` 文件,填写 front matter 即可:

```markdown
---
title: 我的新页面
weight: 10
---

正文内容...
```
