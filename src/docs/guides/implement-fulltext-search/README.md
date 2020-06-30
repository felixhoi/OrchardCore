# 如何实现网站全文检索

Orchard Core提供了一个Lucene模块/功能，允许在您的网站上进行全文搜索。
大多数时候，当你运行一个博客或一个简单的代理网站时，你需要在你的页面内容中进行搜索。
在Orchard Core中，可以通过使用Liquid在内容类型配置中配置要索引的文本/数据。

在进一步讨论之前，我想指定 `TheBlogTheme` 包含一个配方，它将在不需要任何必要知识的情况下为您默认配置所有这些。
让我们一步一步地为您提供这些信息。

## 第一步：在Orchard Core启用Lucene功能。
![Features configuration](images/1.jpg)

正如你在这里看到的，我们有3个不同的Lucene 功能 在Orchard Core。
您需要启用“Lucene”功能才能创建Lucene索引。

## 第二步：创建Lucene索引

![Indices list](images/2.jpg)

点击“添加索引”按钮。

![Create index form](images/3.jpg)

让我们在这里暂停一下，看看在Lucene索引上有哪些选项。

*Index Name*将是用于标识索引的名称。它将在“/App_Data/Sites/{YourTenantName}/Lucene/{IndexName}”中创建一个同名文件夹，其中包含Lucene在索引时创建的所有文件。

第二个选项是用于该索引的*Analyzer Name*。这里的分析器对于高级用户来说是一个更复杂的特性。
它允许您在索引文本时微调文本的词干。例如，当您搜索“Car”时，您可能希望在人们键入小写的“Car”时也有结果。
在这种情况下，分析仪可以用一个小写过滤器编程，它将索引所有小写文本。
更多详情请参考分析仪Lucene.NET网站文档。默认情况下，Orchard Core中的*Analyzer Name*只有*standardanalyzer*可用，
它针对“英语”文化字符进行了优化。Orchard Core使分析器具有可扩展性，因此您可以使用Lucene.NET或者通过实现你自己的。参见：

https://github.com/apache/lucenenet/tree/master/src/Lucene.Net.Analysis.Common/Analysis

例如，您可以使用Startup.cs来自定义模块中的文件：

```C#
using Microsoft.Extensions.DependencyInjection;
using OrchardCore.Lucene.Model;
using OrchardCore.Lucene.Services;
using OrchardCore.Modules;

namespace OrchardCore.Lucene.FrenchAnalyzer
{
    [Feature("OrchardCore.Lucene.FrenchAnalyzer")]
    public class Startup : StartupBase
    {
        public override void ConfigureServices(IServiceCollection services)
        {
            services.Configure<LuceneOptions>(o =>
                o.Analyzers.Add(new LuceneAnalyzer("frenchanalyzer",
                    new MyAnalyzers.FrenchAnalyzer(LuceneSettings.DefaultVersion))));
        }
    }
}
```


第三个选项是文化。默认情况下，将选择“任意区域性”。在这里，可以选择定义这个索引是应该只索引特定区域性的内容项还是其中任何一个。

*contenttypes*：您可以选择希望看到这个索引解析的任何内容类型。

*索引最新版本*：此选项将允许您仅索引已发布的项目或还索引草稿，如果您希望在自定义前端仪表板中甚至在管理后端自定义模块中搜索内容项，这可能非常有用。默认情况下，如果不选中此选项，它将只索引已发布的内容项。

## 第三步：配置搜索设置

![Search settings](images/4.jpg)

通过之前启用的Lucene模块，我们还添加了一个新的路由映射到“/search”，这需要一些设置才能正常工作。创建新的Lucene索引后要做的第一件事是在Orchard Core中配置搜索设置。在这里，我们可以定义网站上的“/search”页面应该使用哪个索引，也可以定义这个搜索页面应该使用哪些索引字段。默认情况下，我们通常使用`Content.ContentItem.FullText`. 我稍后解释原因。

## 第四步：设置索引权限

![Anonymous user role settings](images/5.jpg)

默认情况下，每个索引都是受权限保护的，因此如果不设置哪些索引应该是公共的，就没有人可以查询它们。
要使“搜索”Lucene索引可用于您网站上的*匿名*用户，您将需要去编辑此用户角色并向其添加权限。每个索引都会在这里列出`OrchardCore.Lucene Feature`section。

## 第六步：测试搜索页面

![Search page](images/6.jpg)

在这个例子中，我使用blogtheme配方自动配置所有东西。所以上面的截图是这个主题的搜索页面结果的一个例子。

## 第七步：微调全文搜索

![Content type indexing settings](images/7.jpg)

Here we can see the Blog Post content type definition. We have now a section for every content type to define which part of this content item should be indexed as part of the `FullText`. 
By default content items will index the "display text" and "body part" but we also added an option for you to customize the values that you would like to index as part of this `FullText` 
index field. By clicking on the "Use custom full-text" we allow you to set any Liquid script to do so. So as the example states you could add `{{ Model.Content.BlogPost.Subtitle.Text }}` if you would like to also find this content item by it's *Subtitle* field. For the remaining, we let you imagine what you could possibly do with this Liquid field : index identifiers, fixed text or numeric values and else!
这里我们可以看到Blog Post内容类型的定义。现在每个内容类型都有一个部分，用于定义此内容项的哪个部分应作为`FullText` 的一部分进行索引。
默认情况下，内容项将索引“Display text”和“body part”，但我们还为您添加了一个选项，用于自定义要作为`FullText` 索引字段一部分索引的值。
通过单击“使用自定义全文”，我们允许您设置任何Liquid脚本。因此，正如示例所述，
您可以添加`{{ Model.Content.BlogPost.Subtitle.Text }}`如果您还想通过它的*Subtitle*字段找到这个内容项。对于剩下的部分，我们让您想象一下您可以用这个Liquid字段做些什么：索引标识符、固定文本或数值等等！

## 可选：搜索模板自定义

此外，您还可以通过重写以下内容，根据主题中的特定需要自定义这些模板：

`/Views/Shared/Search.liquid or .cshtml` (常规布局)  
`/Views/SearchForm.liquid or .cshtml` (表单布局)  
`/Views/SearchResults.liquid or .cshtml` (结果布局)   

例如，这里的一个想法可以是通过将 “Summary” 更改为“SearchSummary”并创建相应的形状模板，来定制搜索结果模板以满足您的需要。

SearchResults.liquid : 
```html
{% if Model.ContentItems != null and Model.ContentItems.size > 0 %}
    <ul class="list-group">
        {% for item in Model.ContentItems %}
            <li class="list-group-item">
                {{ item | shape_build_display: "SearchSummary" | shape_render }}
            </li>
        {% endfor %}
    </ul>
{% elsif Model.Terms != null %}
    <p class="alert alert-warning">{{"There are no such results." | t }}</p>
{% endif %}
```
