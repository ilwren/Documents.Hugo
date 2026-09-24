---
title: 首页
layout: hextra-home
type: docs
---

{{< hextra/hero-badge >}}
  <div class="hx:w-2 hx:h-2 hx:rounded-full hx:bg-primary-400"></div>
  <span>离线部署 · 开箱即用</span>
{{< /hextra/hero-badge >}}

<div class="hx:mt-6 hx:mb-6">
{{< hextra/hero-headline >}}
  项目文档站
{{< /hextra/hero-headline >}}
</div>

<div class="hx:mb-12">
{{< hextra/hero-subtitle >}}
  基于 Hextra 主题与 Hugo 构建的静态文档站点&nbsp;<br class="hx:sm:block hx:hidden" />无需数据库,无需服务端,一份 HTML 即可离线浏览与部署
{{< /hextra/hero-subtitle >}}
</div>

<div class="hx:mb-6">
{{< hextra/hero-button text="开始阅读文档" link="docs" >}}
</div>

<div class="hx:mt-6"></div>

{{< hextra/feature-grid >}}
  {{< hextra/feature-card
    title="纯静态,离线可用"
    subtitle="构建产物是纯 HTML/CSS/JS,不依赖任何在线 CDN 或后端服务,可在内网或本地直接打开。"
  >}}
  {{< hextra/feature-card
    title="Markdown 即文档"
    subtitle="用 Markdown 编写内容,支持代码高亮、目录、卡片等 Shortcode 组件。"
  >}}
  {{< hextra/feature-card
    title="内置全文搜索"
    subtitle="基于 FlexSearch 的全文检索,无需额外配置或第三方服务。"
  >}}
{{< /hextra/feature-grid >}}
