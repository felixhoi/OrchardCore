# 创建一个 Orchard Core CMS 网站

在本指南中，您将从项目模板将果园核心设置为内容管理系统。

## 您需要什么

- NET Core SDK 的最新版本。你可以从这里下载 [https://www.microsoft.com/net/download/core](https://www.microsoft.com/net/download/core).
- 一个文本编辑器和终端，您可以在其中键入 dotnet 命令。

## 创建项目

有不同的方式为果园核心创建网站和模块。你可以在这里了解更多 [here](../../getting-started/templates/README.md).  
在本指南中，我们将使用我们的"代码生成模板"。

您可以使用以下命令安装最新发布的模板：

```dotnet new -i OrchardCore.ProjectTemplates::1.0.0-*```

!!! 注意
    要使用开发分支请添加 `--nuget-source https://nuget.cloudsmith.io/orchardcore/preview/v3/index.json`

创建包含网站的空文件夹。打开终端，导航到该文件夹并运行此操作：

```dotnet new occms -n MySite```

这将在名为 的文件夹中创建一个新的 Orchard Core CMS 项目。 `MySite`.

## 设置网站

应用程序已由模板创建，但尚未设置。

通过执行此命令运行应用程序：

`dotnet run --project .\MySite\MySite.csproj`

!!! note
    如果使用模板的开发分支，请先执行 `dotnet restore .\MySite\MySite.csproj --source https://nuget.cloudsmith.io/orchardcore/preview/v3/index.json` before running the application

应用程序现在应该正在运行，并包含打开的端口：

```
Now listening on: https://localhost:5001
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

浏览器打开<https://localhost:5001>，它应该显示设置页面。 Open a browser on , it should display the setup screen.


为了建立一个网站与CMS的所有功能，将使用 _Blog_ 配方 。食谱包含配置果园核心网站的模块和步骤的列表。


填写表单并选择 __Blog__ 配方和 __SQLite__ 数据库.

![image](assets/setup-screen.jpg)

提交表单。几秒钟后，你应该看一个博客网站。

![image](assets/blog-home-page.jpg)

为了配置它并开始编写内容，您可以转到 <https://localhost:5001/admin>.

## 总结

您刚刚创建了一个Orchard Core CMS 驱动的博客引擎。
