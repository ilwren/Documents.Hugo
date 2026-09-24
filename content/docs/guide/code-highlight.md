---
title: 代码高亮示例
weight: 1
prev: /docs/getting-started/
date: 2025-12-01
lastmod: 2026-02-20
tags: ["C#", "Avalonia", "示例"]
---

Hextra 内置基于 Chroma 的代码高亮,悬停代码块右上角还会出现"复制"按钮。

```csharp
public class MainViewModel : ViewModelBase
{
    private string _title = "Hello Avalonia";

    public string Title
    {
        get => _title;
        set => this.RaiseAndSetIfChanged(ref _title, value);
    }
}
```

```xml
<Window xmlns="https://github.com/avaloniaui"
        x:Class="MyApp.Views.MainWindow"
        Title="MyApp">
    <TextBlock Text="{Binding Title}" />
</Window>
```

## 提示框

```markdown
{{</* callout type="info" */>}}
这是一条提示信息。
{{</* /callout */>}}
```

{{< callout type="info" >}}
这是一条提示信息。
{{< /callout >}}
