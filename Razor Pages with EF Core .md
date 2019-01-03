
# **Razor Pages with EF Core - 1**

#### **本文内容** 

入门
添加模型
使用DB
更新页面
添加搜索
[添加新字段]()

[添加验证]()

**通过本教程，你将GET到以下技能:**

- 创建Razor页面Web应用
- 添加模型
- 使用数据库
- 添加搜索和验证

该示例展示了一个管理和显示电影标题项的应用。

#### **工具**

- 已安装“ASP.NET 和 Web 开发”工作负载的 Visual Studio 2017 版本 15.9 或更高版本
- .NET Core 2.2 SDK 或更高版本



### **第1步：创建Razor Web应用(Create a Razor web app)**



- 从 Visual Studio“文件”菜单中，选择“新建”>“项目”。
- 创建新的 ASP.NET Core Web 应用程序。 将该项目命名为 RazorPagesMovie。 务必将该项目命名为 ContosoUniversity，以便复制/粘贴代码时命名空间相匹配。 ![img](E:\GitHub\RazorPagesInNETCore\img\1NewWeb.PNG)
- 在下拉列表中选择“ASP.NET Core 2.2”，然后选择“Web 应用程序”。 ![img](E:\GitHub\RazorPagesInNETCore\img\1NewWeb2.PNG)

####  问题

1. VS自动添加了哪些文件夹



### **第2步：添加数据模型（add a data model)**



在此部分中，添加了用于管理数据库中的电影的类。 
可以结合 Entity Framework Core (EF Core) 来使用这些类处理数据库。EF Core 是一种对象关系映射 (ORM) 框架，可以简化数据访问代码。 
模型类称为 POCO 类（源自“简单传统 CLR 对象”），因为它们与 EF Core 没有任何依赖关系,只定义了存储在数据库中的数据的属性。



- 右键单击“RazorPagesMovie”项目 >“添加” > “新建文件夹”。 将文件夹命名为“Models”。
- 右键单击“Models”文件夹。 选择“添加” > “类”。 将类命名“Movie”。
- 给Movie类添加如下属性（可复制粘贴以下所有代码）。

```C#
using System;
using System.ComponentModel.DataAnnotations;

namespace RazorPagesMovie.Models
{
    public class Movie
    {
        public int ID { get; set; }
        public string Title { get; set; }

        [DataType(DataType.Date)]
        public DateTime ReleaseDate { get; set; }
        public string Genre { get; set; }
        public decimal Price { get; set; }
    }
}
                    
```

####  问题

1. 属性分别代表什么

2. `[DataType(DataType.Data)]`有什么用



### **第3步：为Movie模型添加基架（Scaffold the movie model)**



在此部分中，将为刚刚创建的数据模型Movie添加基架。基架工具将生成前端页面，用于对“电影”模型执行创建、读取、更新和删除 (CRUD) 操作。



- 右键单击 Pages 文件夹 >“Add” > “New Folder”。 将文件夹命名为“Movies”。

- 右键单击“Movies”文件夹。 选择“Add” > “New Scaffold Item”。

- 在“Add Scaffold”对话框中，选择“Razor Pages using Entity Framework(CRUD)” > “Add”。

- 完成“Razor Pages using Entity Framework(CRUD)”对话框：

  - 在“Model class”下拉列表中，选择“Movie (RazorPagesMovie.Models)。

  - 在“Data Context class”行中，选择 +（加号）并接受生成的名称“RazorPagesM5odels.RazorPagesMovieContext”。

  - 选择“Add”。


#### 问题

1. 搭建基架后创建和修改了什么
   - 创建了文件：*Pages/Movies/Create.cshtml、Edit.cshtml*、*Details.cshtml、Delete.cshtml、Edit.cshtml*； 
     *Data/RazorPagesMovieContext.cs*

   - 修改了文件：*startup.cs*

----
#### 让我们来研究一下基架到底生成了些什么代码

**Index**

先看一下Pages/Movies/Index.cshtml，代码如下：

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.RazorPages;
using Microsoft.EntityFrameworkCore;
using RazorPagesMovie.Models;

namespace RazorPagesMovie.Pages.Movies
{
    public class IndexModel : PageModel 
    {
        private readonly RazorPagesMovie.Models.RazorPagesMovieContext _context;

        public IndexModel(RazorPagesMovie.Models.RazorPagesMovieContext context)
        {
            _context = context;
        }

        public IList Movie { get;set; }

        public async Task OnGetAsync()
        {
            Movie = await _context.Movie.ToListAsync();
        }
    }
}
```

Razor页面派生自`PageModel`类。按照约定，`PageModel`派生类的名字为`<PageName>Model`。

```C#
        public IndexModel(RazorPagesMovie.Models.RazorPagesMovieContext context)
        {
            _context = context;
        }
```

此构造函数使用依赖注入（dependency injection）将数据上下文`RazorPagesMovieContext` 添加到页面中。

```C#
 public async Task OnGetAsync()
{
     Movie = await _context.Movie.ToListAsync();
     }
```

`OnGetAsync()`方法或`onGet()`方法是用来初始化Razor页面。当页面发出请求时，函数将返回一个电影列表。

 当 `OnGet `返回` void `或 `OnGetAsync` 返回`Task`时，不使用任何返回方法。 当返回类型是 `IActionResult `或 `Task`时，必须提供返回语句。 例如，Pages/Movies/Create.cshtml.cs `OnPostAsync `方法，返回类型是`IActionResult`，所以提供了返回语句

```C#
return RedirectToPage("./Index");
```

接下来，我们看一下Index的Razor页面  *Pages/Movies/Index.cshtml*。

```html
@page
@model RazorPagesMovie.Pages.Movies.IndexModel

@{
    ViewData["Title"] = "Index";
}

<h1>Index</h1>

<p>
    <a asp-page="Create">Create New</a>
</p>
<table class="table">
    <thead>
        <tr>
            <th>
                @Html.DisplayNameFor(model => model.Movie[0].Title)
            </th>
            <th>
                @Html.DisplayNameFor(model => model.Movie[0].ReleaseDate)
            </th>
            <th>
                @Html.DisplayNameFor(model => model.Movie[0].Genre)
            </th>
            <th>
                @Html.DisplayNameFor(model => model.Movie[0].Price)
            </th>
            <th></th>
        </tr>
    </thead>
    <tbody>
@foreach (var item in Model.Movie) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Title)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.ReleaseDate)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Genre)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Price)
            </td>
            <td>
                <a asp-page="./Edit" asp-route-id="@item.ID">Edit</a> 
                <a asp-page="./Details" asp-route-id="@item.ID">Details</a> 
                <a asp-page="./Delete" asp-route-id="@item.ID">Delete</a>
            </td>
        </tr>
}
    </tbody>
</table>
```

`@`符号可以将Html语言转换成Razor语言。单个语句使用时，直接在前面加`@`，语句块时，使用`@`包裹起来`@{}`。

```
@page
```

`@page`指令是每个页面必须的，将此文件转换成一个可以处理请求的MVC操作。

```html
@model RazorPagesMovie.Pages.Movies.IndexModel
```

`@model`指令传递给Razor页面的模型。

```html
@{
    ViewData["Title"]="Index";
}
```

将"Title"属性添加到`Viewdata`中，随后“Title”属性会被用于 *Pages/Shared/_layout.cshtml*中:

```html
<title>@ViewData["Title"]-RazorPagesMovie</title>
```

`ViewDataPage` 是`PageModel`的一个字典属性，通过键/值模式存储对象，可用于添加要传递到某个视图的数据。

```html
@Html.DisplayNameFor(model => model.Movie[0].Title))
```

`model=>model.Movie[0].Title`这种表达式叫lambda表达式。`DisplayNameFor`通过查看lambda表达式中的`model.movie[0].Title`来显示名称。



**Data文件夹**

Data文件夹下的 *RazorPagesMovieContext*类是基架自动创建的。

```C#
using Microsoft.EntityFrameworkCore;

namespace RazorPagesMovie.Models
{
    public class RazorPagesMovieContext : DbContext
    {
        public RazorPagesMovieContext (DbContextOptions<RazorPagesMovieContext> options)
            : base(options)
        {
        }   //构造函数

        public DbSet<RazorPagesMovie.Models.Movie> Movie { get; set; }   //为实体集创建一个DbSet/<Movie>属性
    }
}
```



**startup.cs**

在Stratup.ConfigureServices中添加了下面代码：

```
services.AddDbContext<RazorPagesMovieContext>(options =>
      options.UseSqlServer(
           Configuration.GetConnectionString("RazorPagesMovieContext")));
```

`AddDbContext`函数利用依赖注入（dependency injecton)将数据上下文添加到服务里。

 数据上下文指定数据模型中包含哪些实体。`RazorPagesMovieContext` 为 `Movie` 模型协调 EF Core 功能（创建、读取、更新、删除等）。



----




### **第四步：初始迁移**



在此部分中，我们将用程序包管理器控制台（PMC）来添加初始迁移，并使用初始迁移来更新数据库。

- “工具” > "NuGet包管理器" > “包管理器控制台”。在控制台输入以下命令。

  ```
  Add-Migration Initial
  Update-Database
  ```

  `Add-Migration` 命令生成用于创建初始数据库架构的代码。 此架构的依据是 `RazorPagesMovieContext` 中指定的模型。 `Initial` 参数用于为迁移命名。 可以使用任何名称，但是按照惯例，会使用可说明迁移的名称。 

  `Update-Database` 命令在用于创建数据库的 *Migrations/{time-stamp}_InitialCreate.cs* 文件中运行 `Up` 方法。



### **第四步：更改布局**



- 更改 Pages/Shared/_Layout.cshtml 文件中的 `<title>` 元素以显示 Movie 而不是 RazorPagesMovie。

  ```html
  <!DOCTYPE html>
  <html>
  <head>
      <meta charset="utf-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>@ViewData["Title"] - Movie</title>
  ```

- 将下面中的"RazorPagesMovie"改成"RPMovie"。

  ```html
  <a class="navbar-brand" asp-area="" asp-page="/Index">RazorPagesMovie</a>
  ```



