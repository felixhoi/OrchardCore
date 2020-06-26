# Orchard Core 

Orchard Core包含两个不同的项目:

- __Orchard Core Framework__: 一个用于在ASP.NET Core上构建模块化的多租户应用程序的应用程序框架。
- __Orchard Core CMS__: 在Orchard Core框架之上构建的Web内容管理系统（CMS）。

[![Join the chat at https://gitter.im/OrchardCMS/OrchardCore](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/OrchardCMS/OrchardCore?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![BSD-3-Clause License](https://img.shields.io/badge/license-BSD--3--Clause-blue.svg)](LICENSE.txt)
[![Documentation](https://readthedocs.org/projects/orchardcore/badge/)](https://docs.orchardcore.net/)
[![Crowdin](https://badges.crowdin.net/orchard-core/localized.svg)](https://crowdin.com/project/orchard-core)

## Build Status

稳定版 (master): 

[![Build Status](https://api.travis-ci.org/OrchardCMS/OrchardCore.svg?branch=master)](https://travis-ci.org/OrchardCMS/OrchardCore/branches)
[![Build status](https://img.shields.io/appveyor/ci/alexbocharov/orchardcore/master.svg?label=appveyor&style=flat-square)](https://ci.appveyor.com/project/alexbocharov/orchardcore/branch/master)
[![NuGet](https://img.shields.io/nuget/v/OrchardCore.Application.Cms.Targets.svg)](https://www.nuget.org/packages/OrchardCore.Application.Cms.Targets)

每日更新 (dev): 

[![Build Status](https://api.travis-ci.org/OrchardCMS/OrchardCore.svg?branch=dev)](https://travis-ci.org/OrchardCMS/OrchardCore/branches)
[![Build status](https://img.shields.io/appveyor/ci/alexbocharov/orchardcore/dev.svg?label=appveyor&style=flat-square)](https://ci.appveyor.com/project/alexbocharov/orchardcore/branch/dev)
[![Cloudsmith](https://api-prd.cloudsmith.io/badges/version/orchardcore/preview/nuget/OrchardCore.Application.Cms.Targets/latest/x/?render=true&badge_token=gAAAAABey9hKFD_C-ZIpLvayS3HDsIjIorQluDs53KjIdlxoDz6Ntt1TzvMNJp7a_UWvQbsfN5nS7_0IbxCyqHZsjhmZP6cBkKforo-NqwrH5-E6QCrJ3D8%3D)](https://cloudsmith.io/~orchardcore/repos/preview/packages/detail/nuget/OrchardCore.Application.Cms.Targets/latest/)

## 现状

### RC 2

该软件几乎已准备好最终发布。 不进行功能开发或软件增强； 在此阶段仅允许严格限定范围的错误修复，除非出现重大的错误。

这是一个更详细的 [路线图](https://github.com/OrchardCMS/OrchardCore/wiki/Roadmap).

## 开始

- 使用命令 `git clone https://github.com/OrchardCMS/OrchardCore.git` 克隆此仓库，并切换到 `dev` 分支.

### Command line

- 从这个页面安装最新版的 .NET Core SDK  <https://www.microsoft.com/net/download/core>
- 接下来,导航到 `D:\OrchardCore\src\OrchardCore.Cms.Web` 或你的文件夹，在管理员模式下命令行。.
- 执行 `dotnet run`.
- 然后在浏览器中打开 `http://localhost:5000` .

### Visual Studio

- 从 https://www.visualstudio.com/downloads/ 下载 Visual Studio 2019 (任何版本) 
- 打开解决方案： `OrchardCore.sln`，然后等待恢复所有包
- 确保启动项目为： `OrchardCore.Cms.Web` ，然后运行

### Docker

- 运行 `docker run --name orchardcms orchardproject/orchardcore-cms-linux:latest`

Docker 镜像和参数可以到这里查看 <https://hub.docker.com/u/orchardproject/>

### 文档

可以从这里访问文档: <https://docs.orchardcore.net/>

## 编码规范

看这里 [编码规范](./CODE-OF-CONDUCT.md)

## .NET Foundation

这个项目支持 [.NET Foundation](http://www.dotnetfoundation.org).
