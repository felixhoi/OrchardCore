# 创建模块化ASP.NET Core 应用程序

## 你将构建什么

您将构建一个由模块组成的应用程序。该模块将提供一个控制器和一个视图，而布局将由主应用程序项目提供。

## 你需要准备什么

- .NET Core SDK的当前版本。你可以从这里下载 [https://www.microsoft.com/net/download/core](https://www.microsoft.com/net/download/core).
- 一个文本编辑器和一个可以键入dotnet命令的终端。

## Creating an Orchard Core site and module

有不同的方法来创建网站和模块的Orchard Core。了解更多 [here](../../getting-started/templates/README.md).  
在本指南中，我们将使用我们的“代码生成模板”.

可以使用以下命令安装最新发布的模板：

```dotnet new -i OrchardCore.ProjectTemplates::1.0.0-*```

!!! 注意
    使用模板的开发版分支需要添加 `--nuget-source https://nuget.cloudsmith.io/orchardcore/preview/v3/index.json`

创建一个包含站点的空文件夹。打开终端，导航到该文件夹并运行以下命令：

```dotnet new ocmvc -n MySite```

这将创建一个新的ASP.NETMVC应用程序在一个名为 `MySite`.  
现在可以使用以下命令创建新模块：

```dotnet new ocmodulemvc -n MyModule```

该模块在“MyModule”文件夹中创建。
下一步是通过添加项目引用从应用程序引用模块：

```dotnet add MySite reference MyModule```

## 测试生成的应用程序

从包含两个项目的文件夹根目录中，运行以下命令：

`dotnet run --project .\MySite\MySite.csproj`

!!! 注意
    如果您使用的是模板的开发分支, 运行程序前，先执行：
    
     `dotnet restore .\MySite\MySite.csproj --source https://nuget.cloudsmith.io/orchardcore/preview/v3/index.json` 

您的应用程序现在应该运行在以下端口：

```
Now listening on: https://localhost:5001
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

打开浏览器 <https://localhost:5001/MyModule/Home/Index>  
它应该显示 __Hello from MyModule__

> 布局来自主应用程序项目，而控制器、操作和视图来自模块项目。

## 注册自定义路由

默认情况下，模块中的所有路由都为`{area}/{controller}/{action}`其中`{area}`是模块的名称。
我们将更改此模块中视图的路径以处理主页。

在 `Startup.cs` 文件 `MyModule` ，请将此代码添加到 `Configure()` 方法中。

```csharp
    routes.MapAreaControllerRoute(
        name: "Home",
        areaName: "MyModule",
        pattern: "",
        defaults: new { controller = "Home", action = "Index" }
    );
```

重新启动应用程序并打开主页，该主页应显示与之前的url相同的结果。

## 摘要

你刚刚创造了一个ASP.NET具有包含控制器和视图的模块的核心应用程序。

## 视频讲解

<https://www.youtube.com/watch?v=LoPlECp31Oo>
