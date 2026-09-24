---
title: 组件与语法示例
weight: 3
tags: ["组件", "Shortcode"]
---

汇总一些除 [Markdown 语法速查](../markdown-syntax) 之外,常用但容易漏掉的写法。

## Tab 页(Tabs)

用 `name` 给每个 `tab` 命名,**不要用**已废弃的 `items="A,B"` 写法。

````markdown
{{</* tabs */>}}
  {{</* tab name="C#" icon="code" */>}}
```csharp
Console.WriteLine("Hello, Avalonia!");
```
  {{</* /tab */>}}
  {{</* tab name="XAML" */>}}
```xml
<TextBlock Text="Hello" />
```
  {{</* /tab */>}}
{{</* /tabs */>}}
````

{{< tabs >}}
  {{< tab name="C#" icon="code" >}}
```csharp
Console.WriteLine("Hello, Avalonia!");
```
  {{< /tab >}}
  {{< tab name="XAML" >}}
```xml
<TextBlock Text="Hello" />
```
  {{< /tab >}}
{{< /tabs >}}

> 想让"同名"的 Tab 在全站范围内联动切换(比如所有页面的 "C#" Tab 一起切换),在 `hugo.yaml` 加:
> `params.page.tabs.sync: true`,或者单页 front matter 写 `tabs.sync: true`。

## 折叠内容(Details)

用的是百分号定界符&#123;&#123;% … %&#125;&#125;(内容会按 Markdown 渲染,而不是纯文本)。

```markdown
{{%/* details title="点击展开安装步骤" */%}}
1. 下载 Hugo extended
2. 运行 `hugo server -D`
{{%/* /details */%}}
```

{{% details title="点击展开安装步骤" %}}
1. 下载 Hugo extended
2. 运行 `hugo server -D`
{{% /details %}}

## 步骤条(Steps)

用普通的 Markdown 标题(`###`)作为每一步的标题,`steps` 会自动加编号和竖线。

```markdown
{{%/* steps */%}}

### 第一步:安装 Hugo

...

### 第二步:创建站点

...

{{%/* /steps */%}}
```

{{% steps %}}

### 第一步:安装 Hugo

下载 Hugo extended 二进制文件。

### 第二步:创建站点

```bash
hugo new site my-site --format=yaml
```

{{% /steps %}}

## 徽标(Badge)

```markdown
{{</* badge content="v0.12.3" color="blue" */>}}
{{</* badge "稳定版" */>}}
```

{{< badge content="v0.12.3" color="blue" >}} {{< badge "稳定版" >}}

## 文件树(Filetree)

```markdown
{{</* filetree/container */>}}
  {{</* filetree/folder name="content" */>}}
    {{</* filetree/folder name="docs" */>}}
      {{</* filetree/file name="_index.md" */>}}
    {{</* /filetree/folder */>}}
  {{</* /filetree/folder */>}}
{{</* /filetree/container */>}}
```

{{< filetree/container >}}
  {{< filetree/folder name="content" >}}
    {{< filetree/folder name="docs" >}}
      {{< filetree/file name="_index.md" >}}
    {{< /filetree/folder >}}
  {{< /filetree/folder >}}
{{< /filetree/container >}}

## 图标(Icon)

```markdown
{{</* icon "github" */>}}
```

{{< icon "github" >}} 这是一个行内图标,图标名要在 `themes/hextra/data/icons.yaml` 里能查到。

## 术语表(Term / 缩写高亮)

需要先在**站点自己的** `data/zh-cn/termbase.yaml` 里定义词条(主题本身不带任何词条,是空的),鼠标悬停在词条上会显示浏览器原生的 tooltip(`<abbr title="...">`)。

```yaml
# data/zh-cn/termbase.yaml
- abbr: WPF
  term: Windows Presentation Foundation
  definition: "微软基于 .NET 的桌面 UI 框架,使用 XAML 描述界面。"
```

```markdown
鼠标悬停在 {{</* term "WPF" */>}} 上可以看到全称与释义。
```

鼠标悬停在 {{< term "WPF" >}} 上可以看到全称与释义,{{< term "MVVM" >}} 也是同理。

## 原生 HTML

因为 `hugo.yaml` 里开了 `markup.goldmark.renderer.unsafe: true`,Markdown 正文里可以直接写原生 HTML,会原样输出:

```html
<div style="padding:12px;border-radius:8px;background:#eef2ff;">
  这是一段直接写在 Markdown 里的原生 HTML。
</div>
```

<div style="padding:12px;border-radius:8px;background:#eef2ff;">
  这是一段直接写在 Markdown 里的原生 HTML。
</div>

## 图片(带说明文字 + 点击放大预览)

标准 Markdown 图片语法直接支持三种来源:远程图片(`http` 开头,原样输出)、`static/` 目录下的静态文件(路径以 `/` 开头)、`assets/` 目录或页面同级目录下的资源(会走 Hugo 的图片处理管线)。

**基础写法:**

```markdown
![组件预览截图](/images/preview-demo.png)
```

![组件预览截图](/images/preview-demo.png)

**加说明文字(caption):** 在图片语法的第二个参数里加引号包住的标题,会自动包一层 `<figure>` + `<figcaption>`,不需要额外写 HTML:

```markdown
![组件预览截图](/images/preview-demo.png "图 1:代码高亮组件效果示意")
```

![组件预览截图](/images/preview-demo.png "图 1:代码高亮组件效果示意")

**点击放大预览:** 主题内置了基于 medium-zoom 的点击缩放功能,默认是关闭的(`site.Params.imageZoom.enable`),而且默认会去 CDN(`cdn.jsdelivr.net`)拉取脚本——离线部署同样要 vendor 到本地,做法和之前 FlexSearch 那次完全一样:

```yaml
# hugo.yaml
params:
  imageZoom:
    enable: true
    js: "js/vendor/medium-zoom.min.js"   # vendor 到本地,不走默认 CDN
```

开启之后,**上面这两张图直接点击就能放大**(不需要改 Markdown 写法,全站所有图片自动生效);如果只想单独给某一张图关闭/开启,在**页面** front matter 里写 `imageZoom: false`(或 `true`)覆盖全局设置。

> 图片路径的坑:`/images/xxx.png` 这种以 `/` 开头的写法,实际指向的是 `static/images/xxx.png`(经过实测确认,查阅的是主题自带的 `layouts/_markup/render-image.html` 渲染钩子源码,不是网上的资料)。如果图片放在 `assets/` 目录下,则是走图片处理管线(可以用 `card` shortcode 里 `image` 参数那种 `Resize`/`webp` 转码能力),两种目录的图片同样都用 `/xxx.png` 这种绝对路径引用,主题会自动判断优先去哪里找。

## 视频预览播放

**Hextra 主题同样没有内置视频组件**(查过全部源码,没有 `<video>` 相关模板),Markdown 语法本身也没有视频标签——所以这是本站自己加的一个 shortcode,用的是原生 HTML5 `<video>` 标签,本地视频文件直接播放,不需要联网、不需要任何播放器 SDK。

```markdown
{{</* video src="/videos/demo.mp4" poster="/images/preview-demo.png" caption="图 2:功能演示视频" */>}}
```

{{< video src="/videos/demo.mp4" poster="/images/preview-demo.png" caption="图 2:功能演示视频" >}}

路径规则跟图片完全一致:`/videos/demo.mp4` 对应的是 `static/videos/demo.mp4`。`poster` 是可选的封面图(没播放之前显示的画面),`caption` 是可选的说明文字。

实现文件:`layouts/_shortcodes/video.html`,样式在 `assets/css/custom.css` 里(让视频宽度自适应容器,不会撑破版面)。

> 如果是 YouTube / 哔哩哔哩这种平台上托管的视频,不用这个 shortcode,直接在 Markdown 里写平台给的 `<iframe>` 嵌入代码就行(因为开了 `unsafe: true`)。但这种方式要联网加载,跟"离线站点"的定位是冲突的,只建议内网能访问对应视频平台时使用。

## 代码块里跳转到指定行

给某一行代码加一个可以被链接跳转的"锚点",要在 fenced code block 的语言后面加属性:`{linenos=inline,anchorlinenos=true,lineanchors=某个前缀}`。**`lineanchors` 的前缀值在同一个页面里每个代码块必须不一样**,不然多个代码块的行号 id 会重复冲突,浏览器只会跳到第一个。

````markdown
点击跳转到 [第 3 行](#demo-3)。

```csharp {linenos=inline,anchorlinenos=true,lineanchors=demo}
public class Foo
{
    public int Bar;
    public void Baz() {}
}
```
````

点击跳转到 [第 3 行](#demo-3)。

```csharp {linenos=inline,anchorlinenos=true,lineanchors=demo}
public class Foo
{
    public int Bar;
    public void Baz() {}
}
```

效果上,`anchorlinenos=true` 会让 Hugo 把每一行的行号都渲染成 `id="demo-1"`、`id="demo-2"`……这样的锚点(同时行号本身也会变成可点击链接),所以你在页面任何地方用 `[文字](#demo-3)` 都能精确跳到第 3 行。

⚠️ 这里有两点是我实测才确认的,不是官方文档明确写出来的:
1. Hugo 曾经有一个 issue(2022 年,v0.92)说 `anchorlinenos`/`lineanchors` 这两个属性写在 fenced code block 里不生效——**这个 bug 目前用的 Hugo v0.151.0 已经修复**,我在这个项目里实测过是正常的。
2. `linenos=inline` 而不是 `linenos=table`:table 模式下行号和代码是两个独立的 `<table>`单元格,没法用纯 CSS 做到跳转后整行高亮;inline 模式下行号和代码在同一个 `<span>` 里,配合 `custom.css` 里 `.chroma .line:has(.ln:target)` 这条规则,跳转到的那一行会有黄色背景高亮(用了 `:has()` 选择器,是比较新的 CSS 特性,如果要兼容很老的浏览器可以去掉这条,保留另一条效果差一点的兜底规则)。

## 引用其他页面时的"悬浮预览"

**Hextra 主题本身没有内置这个功能**(查过主题全部源码,没有找到悬浮预览/tooltip 相关组件),下面是本站自己加的一个轻量扩展:纯 CSS 实现,鼠标悬停在链接上会弹出目标页面的标题和摘要,不需要点击。

实现文件:
- `layouts/_shortcodes/linkpreview.html` — 取目标页面的 `Title` 和 `Summary`
- `assets/css/custom.css` — 悬浮弹出的样式(覆盖主题空的 `custom.css`)

```markdown
之前提到的 {{</* linkpreview link="/docs/guide/code-highlight" */>}}代码高亮示例{{</* /linkpreview */>}},
鼠标悬停就能看到预览,不用点进去。
```

之前提到的 {{< linkpreview link="/docs/guide/code-highlight" >}}代码高亮示例{{< /linkpreview >}},鼠标悬停就能看到预览,不用点进去。

> 局限性:摘要取的是目标页面的 `.Summary`(默认是正文前 70 个词左右,也可以在正文里手动插入 Hugo 的摘要分隔符来指定摘要范围,具体写法见 Hugo 官方文档的 "Summaries" 一节),不支持图片预览,移动端没有 hover,长按也不会触发(移动端建议直接用普通链接或前面讲过的 `cards` 卡片导航)。
