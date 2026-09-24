---
title: Markdown 语法速查
weight: 2
date: 2026-01-10
lastmod: 2026-03-02
tags: ["Markdown", "语法"]
---

本站基于 Goldmark 渲染引擎(已在 `hugo.yaml` 中开启 `extras` 扩展),下面是常用语法。

## 高亮 / 删除线 / 上下标 / 插入

需要在 `hugo.yaml` 的 `markup.goldmark.extensions.extras` 中开启(本站已开启),并且**关闭内置 `strikethrough`**,否则 `~下标~` 会被内置的删除线扩展抢先解析。

```markdown
==高亮文字==
~~删除线~~
++插入文字++
上标: X^2^
下标: H~2~O
```

==高亮文字==
~~删除线~~
++插入文字++
上标: X^2^
下标: H~2~O

## 链接

```markdown
行内链接: [Hugo 官网](https://gohugo.io/)

引用式链接: [参考文档][ref]

[ref]: https://gohugo.io/ "鼠标悬停时的提示文字"

站内页面互链(推荐,自动处理路径且构建时校验): [快速开始]({{</* relref "getting-started" */>}})
```

## 表格

```markdown
| 特性 | 是否需要额外配置 |
| --- | --- |
| 表格 | 否,默认支持 |
| 任务列表 | 否,默认支持 |
```

| 特性 | 是否需要额外配置 |
| --- | --- |
| 表格 | 否,默认支持 |
| 任务列表 | 否,默认支持 |

## 任务列表

```markdown
- [x] 已完成
- [ ] 未完成
```

- [x] 已完成
- [ ] 未完成

## 脚注

```markdown
这是一段正文[^1]。

[^1]: 这里是脚注的具体说明。
```

## 提示框 / 卡片等 Hextra 组件(Shortcode)

除了标准 Markdown,Hextra 还提供了一些 Shortcode 组件,常用的有:

```markdown
{{</* callout type="warning" */>}}
这是一条警告提示。
{{</* /callout */>}}

{{</* cards */>}}
  {{</* card link="../getting-started" title="快速开始" icon="lightning-bolt" */>}}
{{</* /cards */>}}

{{</* tabs items="C#,XAML" */>}}
  {{</* tab */>}}C# 代码...{{</* /tab */>}}
  {{</* tab */>}}XAML 代码...{{</* /tab */>}}
{{</* /tabs */>}}
```

更完整的组件列表可查看主题目录 `themes/hextra/layouts/_shortcodes/`。
