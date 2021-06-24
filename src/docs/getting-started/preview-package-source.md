# Add preview package source

在本文中，我们将添加一个指向预览包的新包源。   
每次在 dev 分支上提交一些代码时都会构建预览包，和从master分支构建的Nuget包相比，
它们是最新版本，但不是最稳定的，并且可能包含重大更改。 

!!! warning
    我们不建议您在生产中使用 dev 包。

## Adding Orchard Core preview Feed to Visual Studio

In order to be able to use the __preview__ feed from Visual Studio, open the Tools menu under NuGet Package Manager --> Package Manager Settings.
The feed url is <https://nuget.cloudsmith.io/orchardcore/preview/v3/index.json>

![image](assets/add-preview-package-source.png)


## Adding Orchard Core preview Feed with NuGet.config

You can also add the package source by using a NuGet.config file:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <clear />
    <add key="NuGet" value="https://api.nuget.org/v3/index.json" />
    <add key="OrchardCorePreview" value="https://nuget.cloudsmith.io/orchardcore/preview/v3/index.json" />
  </packageSources>
  <disabledPackageSources />
</configuration>
```
