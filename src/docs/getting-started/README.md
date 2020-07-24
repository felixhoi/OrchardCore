# Orchard Core的NuGet包使用 入门篇

在这篇文章中，我们将看到使用Orchard Core的NuGet包创建一个CMS网站应用有多简单。
 
Chris Payne撰写的原文链接如下：
<http://ideliverable.com/blog/getting-started-with-orchard-core-as-a-nuget-package>

## 创建一个Orchard Core CMS网站应用

使用Visual Studio，创建一个名为Cms.Web空的.NET Core网站应用。在配置新项目界面，不要勾选`将解决方案和项目放在同一目录中`选项，因为稍后创建模块和主题时，你可能希望它们在解决方案的同级目录中。

!!! 备注
    如果你想使用“预发行”包，[在“程序包源”中配置OrchardCore预览地址](preview-package-source.md)

    为项目添加包引用,在项目里的 `依赖项` 上右击然后选择 `管理NuGet程序包` , 勾选 `包括发行版` (如果需要的话) 。 如果你配置了上面的预览地址，点击右上角的 `程序包源` 并选择刚才配置的预览地址。在 `浏览` 选项卡中，搜索 `OrchardCore.Application.Cms.Targets` ，然后选中并 `安装` 这个包。

打开 `Startup.cs` 并修改 `ConfigureServices` 方法，添加以下代码：

```csharp
services.AddOrchardCms();
```

在 `Configure` 方法中, 选中以下代码:

```csharp
app.UseEndpoints(endpoints =>
{
    endpoints.MapGet("/", async context =>
    {
        await context.Response.WriteAsync("Hello World!");
    });
});
```

然后使用以下代码替换:

```csharp
app.UseOrchardCore();
```

## 编译生成应用

运行项目 (Ctrl+F5)。浏览器显示了 安装界面。

在安装界面输入需要的信息：

- 站点名字。 比如： `Orchard Core`.
- 配方。 比如： `Agency`.
- 默认时区。 比如： `(+01:00) Europe/Paris`.
- 数据库类型。 比如： `SqLite`.
- 超级用户名。 比如： `admin`.
- 超级用户的电子邮箱。 比如： `foo@bar.com`
- 超级用户的密码以及确认密码。

提交表单，你的网站在几秒后将会生成。

然后，你就可以使用 `/admin` 地址访问管理界面了。开始享受成果吧。
