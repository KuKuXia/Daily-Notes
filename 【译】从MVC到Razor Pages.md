## ![img](https://www.codeproject.com/KB/aspnet/1208668/MVCFolders.png)

## 概念整合

！[img](https://github.com/Dadaxin/Daily-Notes/blob/master/ConceptInFromMVCToRazorPages.PNG)

## 介绍

使用ASP.NET Core 2，Microsoft为我们提供了创建Web应用程序的MVC（Model-View-Controller）方法的全新替代方案。微软将其命名为“Razor Pages”，尽管采用不同的方法，但在某些方面仍然很熟悉。

本文将展示一个场景，其中Razor Pages用于生产一个小型电子商务网站，并在Facebook的React / ReactJS.NET帮助下，为其提供基于JavaScript代码的视图呈现/绑定引擎。


> 引用：
>
> **免责声明：本文主要关注Razor页面，并补充了我几个月前发布的以前的  React Shop - 微型电子商务文章。如果您想了解有关在ASP.NET应用程序中使用React和React JS.NET的更多信息，请参阅其他文章。**

## 安装

为了在附带的源代码中运行应用程序，请安装以下内容：

- [.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core)或更高版本。
- [Visual Studio 2017版本15.3](https://www.visualstudio.com/downloads/)或更高版本与ASP.NET和Web开发工作负载。
- [Microsoft®SQLServer®2014 Express](https://www.microsoft.com/en-US/download/details.aspx?id=42299)或更高版本。
- 下载本文顶部的项目源代码。

## 背景

如果您从过去十年开始关注ASP.NET开发，您可能已经注意到，Microsoft曾经和微软一起提出了一种新的开发工具或框架的创新 - 甚至是新的设计模式。其中一些已被证明是非常强大可靠的，如ASP.NET MVC和Razor视图引擎，而其他还没有通过时间的考验，被放弃，如AJAX Control Toolkit。

![img](https://www.codeproject.com/KB/aspnet/1208668/Timeline.png)

但是，自从2016年发布ASP.NET Core 1.0以来，很多事情都发生了变化。微软重新编写了ASP.NET作为一个开放源代码的GitHub托管项目，并首次向其Web开发框架介绍了多平台。

自从第一个版本开始，ASP.NET Core为ASP.NET 3.0提供了标准的Web开发框架，这个ASP.NET MVC是基于Model-View-Controller设计模式的。
MVC设计模式是1979年在神话中的Xerox Palo Alto研究中心（XPARC）开发的，但是在几个Web框架开始采用之后才开始出现：2002年的Spring为Java，2005年为Django和Ruby on Rails以及ASP。 NET在2009年。

而ASP.NET MVC是我们社区的一大热门。在此之前，我们必须处理从ASP.NET Web窗体中出现的问题，例如更新面板，增加ViewState，Postbacks以及相当复杂的页面事件管理。使用ASP.NET MVC，我们被教导在开发我们的Web应用程序时说出分离问题的语言：数据属于模型，表示逻辑仅适用于视图，每个请求必须由Controller操作处理，而这些操作又决定哪个视图将与其适当的模型一起呈现。没有更多的需要从程序员隐藏网络的无国籍性质。  

但ASP.NET MVC虽然给我们带来了很多好处，但有时仍然遇到了一些批评。虽然用户 - 当然是Web开发人员 - 将Web应用程序基本看作一组“网页”，ASP.NET MVC没有一个清晰的Web页面概念。相反，在ASP.NET MVC项目中，每个组件通常都有自己的文件，并且属于不同的文件夹，具体取决于它在MVC框架内的作用。

现在，暂停一会，想像你如何组织你的电脑文件夹。想象一下，您有不同的工作要做，涉及不同的文件，而且您的计算机文件夹不是按主题或工作或主题组织，而是由文件类型组织。并且想像您正在执行多个不同的作业，而不是分配每个作业的文件，您将每个作业的文件分散在不同的文件夹中，如下所示： 

![img](https://www.codeproject.com/KB/aspnet/1208668/ManyFolders.png)

这会是个好主意吗？

类似地，我们可以从下面的图像中看出，典型的MVC项目如何将一个文件中的单个页面的组件分散在许多文件和文件夹中：

![img](https://www.codeproject.com/KB/aspnet/1208668/MVCFolders2.png)

所以在MVC中没有一个“网页”文件。向技术新手的人解释一下有点尴尬。

那么微软有人认为同样的事情可以用不同的方式完成。


## 介绍Razor页面

如果您使用MVC应用程序，然后将您的View称为页面（例如，在  Index.cshtml文件中），并且您不仅集中了模型数据，还集中了与该页面相关的服务器端代码（以前驻留在你的控制器）里面一个专门的页面（在一个Index.cshtml.cs文件里面  ） - 你现在称之为页面模型？

如果您已经在本地移动应用程序中工作，那么在[Model-View-ViewModel（MVVM）模式中](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93viewmodel)可能已经看到类似的内容。

![img](https://www.codeproject.com/KB/aspnet/1208668/PagePageModel.png)

*Razor页面中的页面和页面模型*

这就是剃刀页出生！ASP.NET Core 2.0 - 更准确地说，Visual Studio 2017 - 使用Razor页面作为默认内容引入了一个新的Web应用程序模板。

![img](https://www.codeproject.com/KB/aspnet/1208668/AddNewProject.png)

那么你可能会认为“但等一下......这看起来有点太熟悉了”。因为现在你有一个页面，一个执行服务器端功能的类。页面模型不是与文件中的旧代码相同吗？Web窗体不是一遍又一遍吗？

不，让我解释一下为什么Razor Pages不是网络形式的复兴。首先，我们必须意识到，一个Razor页面与MVC设计模式并没有很大的不同。过去，通过Web窗体，您通常会将业务规则，用户界面和数据层混合在一起。在ASP.NET Web窗体中，您已经拥有了以简单，性能和带宽为代价的事件处理的人造管道，另一方面，所有MVC组件在Razor Pages中都可以看到。它们只是位于不同的类/文件/文件夹中，以方便开发页面。

有些人对于Razor页面的另一个误解是关于它主要是初级开发人员或较不复杂的应用程序。尽管新手开发人员可以轻松了解Razor Pages而不是MVC网络应用程序，但仍然可以构建复杂的应用程序，我们将在本文附带的源代码中看到。

创建新的Razor Pages网页应用程式后，您也可能会以某种方式“丢失”使用MVC项目的能力。但幸运的是，这不是真的。记住，这两个模板（MVC和Razor Pages）都依赖于相同的ASP.NET Core MVC框架。所以，例如，您可以创建一个新的Razor页面项目，然后创建MVC文件夹（控制器，视图等）和所需的文件，以便在同一个项目中使用MVC控制器和视图以及Razor页面！

在Razor Pages项目中，在项目根目录下创建一个新的**Controllers**文件夹，然后创建一个`TestController`类。现在我们实现了`Index`返回纯文本的操作：

 

隐藏   复制代码

```
public class TestController : Controller
{
    public IActionResult Index()
    {
        //Accessible through /Test
        return Content("You can work with MVC Controllers and Views " +
            "alongside Razor Pages in the same project!");
    }
}
```

 

运行应用程序并在浏览器的地址栏中输入**http：// localhost：XXXXX / test**，我们得到：

![img](https://www.codeproject.com/KB/aspnet/1208668/TestIndexView.png)

不是很棒吗

## 配置（Configuration）

当您创建一个新的ASP.NET Core Razor Pages Web App时，这是您在**Program.cs**文件中获得的：

```
public class Program
{
    public static void Main(string[] args)
    {
        BuildWebHost(args).Run();
    }

    public static IWebHost BuildWebHost(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .UseStartup<Startup>()
            .Build();
}
```

*Program.cs文件* 

现在，注意  `.UseStartup<Startup>()` 这行，它让ASP.NET Core指定Web主机使用的启动类。

**启动类** 会在选择Razor页面模板时自动创建。它配有为Web应用程序添加服务的**ConfigureServices**方法，以及配置HTTP请求管道的**Configure**方法。

```C#
public class Startup
{
public Startup(IConfiguration configuration)
{
	Configuration = configuration;
}

public IConfiguration Configuration { get; }

// This method gets called by the runtime. Use this method to add services to the container.
public void ConfigureServices(IServiceCollection services)
{
	services.AddMvc();
}

// This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
	if (env.IsDevelopment())
	{
		app.UseDeveloperExceptionPage();
		app.UseBrowserLink();
	}
	else
	{
		app.UseExceptionHandler("/Error");
	}

	app.UseStaticFiles();

	app.UseMvc(routes =>
	{
		routes.MapRoute(
			name: "default",
			template: "{controller}/{action=Index}/{id?}");
	});
}
}
```

*Startup.cs*文件

上面的代码显示了调用**MVC**服务**services.AddMvc**的**ConfigureServices**方法; （**Razor Pages**就是通过这种方式依赖于MVC框架）。此外，在运行时，**Configure**方法会被调用来设置*请求管道（request pipeline）*。 从上面的代码，我们看到**Congigure**方法：

- 指定错误页面配置
- 启用当前请求路径的静态文件服务
- 将MVC添加到Microsoft.AspNetCore.Builder.IApplicationBuilder请求执行管道

所以你有了它，就可以像ASP.NET Core MVC应用程序一样，在Razor Pages Web应用程序中也使用  Startup  类来配置有关Web应用程序的所有内容。

## 新的Razor Pages Web应用程序

记得我们说过Razor Pages就像ASP.NET Core MVC，但是又有所不同么？尽管与MVC不同，Razor Pages仍然依赖于ASP.NET Core MVC Framework。使用Razor Pages模板创建新项目后，Visual Studio将通过`Startup.cs`文件配置应用程序以启用ASP.NET Core MVC框架，正如我们刚刚看到的那样。

该模板不仅可以配置新的Web应用程序以供MVC使用，还可以为示例应用程序创建**Page**文件夹和一组Razor页面和页面模型：

![img](https://www.codeproject.com/KB/aspnet/1208668/PagesFolder.png)

对于**Razor页面 Shop**网络应用程序，我需要3个不同的视图（页面）：

- **产品目录**： 用户将从目录中选择放入购物车的产品
- **购物车**：  为采购订单选择的产品
- **订单详细信息：**运送数据，客户信息和刚刚放入的订单的产品列表

![img](https://www.codeproject.com/KB/aspnet/1208668/flow.png)

所以我保持**Index.cshtml**作为产品目录页面，并包含另外2个Razor页面页面：  **Cart.cshtml**和**CheckoutSuccess.cshtml**，用于购物车和订单明细，因此：

![img](https://www.codeproject.com/KB/aspnet/1208668/RazorPagePages.png)

*2个新的Razor页面*：*Cart.cshtml*和*CheckoutSuccess.cshtml*。

## 页面文件夹

前面的图像显示了每个视图（ahem，Razor页面）如何包含在**Pages**文件夹中。新的Pages文件夹和传统的MVC Web应用程序“Views”文件夹之间的区别超出了文件夹名称。事实上，由于我们在Razor页面 web应用程序中没有控制器（Controller）和操作(action)的概念，所以在页面文件夹内的**cshtml**文件的位置  定义了应该访问哪个url路由。例如：

- /Pages/Index.cshtml - >**“/”或“/ Index”**
- /Pages/Cart.cshtml - > **“/ Cart”**
- /Pages/CheckoutSuccess.cshtml - > **“/ CheckoutSuccess”  **

同样，您也可以在Pages文件夹中创建子文件夹，以创建更复杂的URL路由方案：

- /Pages/Products/WhatsNew.cshtml - > **“/ Products / WhatsNew ”**
- /Pages/Categories/Listing.cshtml - >**“/ Categories / Listing ”**
- /Pages/Admin/Dashboard.cshtml - >**“/ Admin / Dashboard ” ** 

## 一个Razor页面的解析

第一眼，Razor页面看起来就像一个普通的ASP.NET MVC View文件。但Razor页面需要一个新的指令。每个Razor页面都必须以这个开头`@page directive`，它告诉ASP.NET Core将其视为Razor页面。下面的图片显示了一些关于典型Razor页面的更多细节。  

![img](https://www.codeproject.com/KB/aspnet/1208668/RazorPage.png)

**@page** - 将文件标识为Razor页面。没有它，该页面根本无法由ASP.NET Core访问。
**@model** - 就像在MVC应用程序中一样，定义了发起绑定数据的类，以及页面请求的Get / Post方法。
**@using** - 定义命名空间的常规指令。
**@inject **- 配置哪些接口实例应该注入到页面模型类中。
**@ {}** - Razor括号中的一段C＃代码，在这种情况下用于定义页面标题。
**<div ...>** - 与启用Razor的C＃代码一起提供的常规HTML代码。

## Razor Pages使Web开发简单

那如果要在Razor页面应用程序中创建静态页面怎么样呢？假设您必须创建一个**Terms Of Use**页面。

在Razor Pages之前，使用常规的MVC Web应用程序，您必须遵循一些步骤才能在Web应用程序中创建一个简单的静态页面：

 

- 添加控制器（Controllers / TermsOfUseController.cs）
- 添加一个Action方法（Index（））
- 添加查看文件夹（/ Views / TermsOfUse）
- 添加视图（/Views/TermsOfUse/Index.cshtml）

 

现在，使用Razor页面，您的工作变得更加简单：

- 添加页面（Pages / TermsOfUse.cshtml）

现在你可能会想，该页面使用的页面模型（Page Model）呢。由于页面只是静态页面，因此不需要任何页面模型，这是MVC Web应用程序的另一个优点。

## 页面模型类（The Page Model Class）

MVC视图通常是被绑定到自定义`Model`或`ViewModel`，与此不同，一个典型的Razor页面将指定其`Model`作为一个继承自`PageModel`的类。看看下面的`IndexModel`课程：


```C#
public class IndexModel : PageModel
{
public IList<ProductDTO> Products { get; set; }
readonly ICheckoutManager _checkoutManager;

public IndexModel(ICheckoutManager checkoutManager)
{
    this._checkoutManager = checkoutManager;
}

public void OnGet()
{
    Products = this._checkoutManager.GetProducts();
}

public async Task<IActionResult> OnPostAddAsync(string SKU)
{
    this._checkoutManager.SaveCart(new CartItemDTO
    {
        SKU = SKU,
        Quantity = 1
    });

    return RedirectToPage("Cart");
}
}
```

*Index.cshtml.cs文件*

上述页面模型通常放在**.cshtml.cs**文件中，有时被称为“a code behind”文件。但是，请不要将此文件和过去Web Forms的臭名昭著的“code behind”文件混为一谈。他们几乎没有共同点。

现在看看`IndexPageModel`构造函数：


```
readonly ICheckoutManager _checkoutManager;

public IndexModel(ICheckoutManager checkoutManager)
{
this._checkoutManager = checkoutManager;
}
```

你可能想知道谁使用`ICheckoutManager checkoutManager`参数调用这个构造函数。幸运的是，从ASP.NET Core 1开始，该框架具有内置的**依赖注入（dependency injection**服务。



:yellow_heart: **依赖注入**的概念是某些类实例必须由框架自动创建，但是这样的类有一个构造函数，该构造函数**依赖**于另一个接口的实例。所以，在第一个类（在这个例子中是`IndexModel`）实例化之前，框架应该先创建一个依赖关系（在这个例子中下是`ICheckoutManager`接口），然后将它们传递给构造函数。

但是为了从接口创建实例，应该为框架提供哪些类可以实现这种接口的信息。您应该在**Startup.cs**文件中配置此依赖注入信息，更准确地说在`ConfigureServices`方法中：

```
public IServiceProvider ConfigureServices(IServiceCollection services)
{
services.AddMvc();
services.AddScoped<ICheckoutManager, CheckoutManager>();
.
.
.
```

*在Startup.cs文件中配置依赖注入。*

请注意，`services.AddScoped<ICheckoutManager, CheckoutManager>();`代码如何将`CheckoutManager`类定义为在`ICheckoutManager`需要新实例时应该创建的类型。这是通过该`services.AddScoped`方法完成的。



说到配置，请注意我们使用的`AddScoped`方法。ASP.NET Core为我们提供了一些这些实例应该多久创建一次的选项，以及它们应该用于依赖注入的次数。这被称为**服务生命周期(Service lifetime)**，并且这些生命周期可以配置如下：

**Transient：**每次请求时创建一个新的实例。

**Scoped：**每个请求创建一个新的实例。

**Singleton：**在第一次请求时创建一个新的实例，并且在每个后续请求中使用相同的实例。

除了`Startup.cs`配置之外，您还应该`@injection`在页面文件中包含一个指令，指示依赖注入服务应根据请求生成哪些接口：


```
@inject ICheckoutManager ICheckoutManager;
```

*配置@inject指令*

## 介绍页面处理程序（Page Handlers)

如果您习惯使用MVC模式，您可能会想知道如何使用Razor Pages替换**MVC Action Methods**。在MVC Web应用程序中，**控制器r**是您应用程序中每个请求的入口点。在**MVC模式中**，控制器是可以响应应用程序中不同视图的许多操作的集合，它们可以方便地分组在一起，以共享过滤器(filters)和路由模板(route templates)等资源。

Razor Pages现在具有**页面处理程序**，它是MVC控制器操作的替代。这些处理程序响应特定的HTTP动词，例如GET和POST。处理程序存在于Razor Pages中，名称约定为**“on {HTTP Verb}”**。

这意味着，针对Razor页面的每个HTTP Get请求都位于“code behind”文件里的`OnGet`上。例如，在`Index`Razor页面中，我们有一个`OnGet`处理程序方法，用于实例化Bootstrap产品转盘中显示的产品列表：


```C#
public void OnGet()
{
Products = this._checkoutManager.GetProducts();
}
```

但是如果页面模型没有这样的**OnGet**方法，或者页面模型甚至不存在，该怎么办？幸运的是，在这种情况下，Razor页面无论如何也是无误的。这是一个方便的解决方案，避免了简单Razor页面的样式和模板。

现在，如果要处理HTTP Post请求，例如由HTML `<form>`元素提交的那些请求，例如：


```html
<form method="post">
.
.
.
<button type="submit" class="btn btn-link" name="SKU" value="@product.SKU">
<i class="fa fa-shopping-cart" aria-hidden="false"></i>
Add to Cart
</button>
.
.
.
</form>
```

那么你应该遵循**“on {HTTP Verb}”**的名称约定，并创建一个新的Razor页面处理程序（方法）`OnPostAsync`：



```C#
public async Task<IActionResult> OnPostAsync(string SKU)
{
this._checkoutManager.SaveCart(new CartItemDTO
{
    SKU = SKU,
    Quantity = 1
});

return RedirectToPage("Cart");
}
```

 

还有一种情况，您可能希望在Razor页面中为不同目的提交不同的HTTP POST请求。例如，您可能有3个按钮：一个用于**添加**，另一个用于**更新**，另一个用于**删除**操作。您应该如何在单个`OnPostAsync`处理程序中容纳不同的POST请求？

幸运的是，在这种情况下，Razor Pages提供了一个方便的替代方法，使用**标签助手（Tag Helpers）**。标签助手，如ASP.NET Core 1.0中首次看到的，使服务器端代码能够在Razor文件中创建和呈现HTML元素。使用标签助手，您可以指定要在同一页面中使用的多个POST处理程序方法。例如，假设您要将方法名称更改`OnPostAsync`为`OnPostAddAsync`：



```C#
public async Task<IActionResult> OnPostAddAsync(string SKU)
{
this._checkoutManager.SaveCart(new CartItemDTO
{
    SKU = SKU,
    Quantity = 1
});

return RedirectToPage("Cart");
}
```

 

显然，以前的`<form>`HTML将无法向新重命名的处理程序方法提交请求。但是，您可以将`<form>`HTML元素更改为**Tag Helper，**并使用**asp-page-handler**来为POST请求指定新的处理程序变体：



```html
<form asp-page-handler="Add"

.

.

.

<button type="submit" class="btn btn-link" name="SKU" value="@product.SKU">
<i class="fa fa-shopping-cart" aria-hidden="false"></i>
Add to Cart
</button>
.
.
.
</form>
```

## 将ReactJS.NET集成到ASP.NET Core 2.0中

最后一次使用**React**和ASP.NET 4.x时，我按照[React的“服务器端渲染”指南](https://reactjs.net/guides/server-side-rendering.html)，使用包含每个视图内容的**.jsx**文件配置静态类`ReactConfig`：


```C#
public static class ReactConfig
{
    public static void Configure()
    {
        ReactSiteConfiguration.Configuration
            .AddScript("~/Scripts/showdown.js")
            .AddScript("~/Scripts/react-bootstrap.js")
            .AddScript("~/Scripts/Components.jsx")
            .AddScript("~/Scripts/Cart.jsx")
            .AddScript("~/Scripts/CheckoutSuccess.jsx");
    }
}
```

*老版本的ReactConfig.cs配置文件*

但是该教程是针对ASP.NET 4.x而进行的，并且在ASP.NET Core Web应用程序中不起作用。所以我不得不遵循新的[React教程](https://reactjs.net/getting-started/tutorial.html)，将服务器端渲染部分移植到ASP.NET Core **Startup.cs**文件中。于是，我必须包含进那些`Configure`（Startup类中）中的脚本，以便**ReactJS.NET**可以从**.jsx**文件中呈现服务器端的HTML内容。


```
app.UseReact(config =>
{
    config
        .AddScript("~/lib/react-bootstrap/react-bootstrap.min.js")
        .AddScript("~/js/Components.jsx")
        .AddScript("~/js/Cart.jsx")
        .AddScript("~/js/CheckoutSuccess.jsx")
        .SetUseDebugReact(true);
});
```

*启动配置文件中的新配置方法*

但是**React.AspNet**扩展还需要调用`services.AddReact();`方法来注册ReactJS.NET所需的所有服务：

```
public IServiceProvider ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    services.AddScoped<ICheckoutManager, CheckoutManager>();
    services.AddReact();
    .
    .
    .
}
```

## 应用页面

由于这个网络应用程序的页面是从另一个MVC应用程序的视图移植到这个Razor Pages Web应用程序，并且在我的其他文章“ **React Shop - A Tiny e-Commerce”中**已经讨论过了，而且由于它们几乎保持不变，我就不再解释一切。如果您想了解有关**React-Bootstrap**组件，**React JS**视图和**.jsx**文件以及ASP.NET应用程序的详细信息，请访问我的其他文章。

这里仅仅是对应用页面的简单概述。

#### 产品目录

![img](https://www.codeproject.com/KB/aspnet/1208668/Index.png)

*产品目录页。*

产品目录页面显示了一个简单的产品轮播（Carousel）控制。此Bootstrap控件对于显示无限动画非常有用，并且可以只使用一小部分页面空间来显示许多产品。

产品转盘通过**Razor**视图引擎在服务器端呈现。轮播界面一次显示四个产品，因此**Index.cshtml**视图中的代码定义了一个`foreach`循环，每个循环遍历4个产品的“页面”。

#### 购物车

![img](https://www.codeproject.com/KB/aspnet/1208668/Cart.png)

*购物车页面。*

与“产品目录”相比，“购物车”页以非常不同的方式呈现。首先，Razor引擎不用于直接渲染视图。相反，Razor调用了**React.Web.Mvc.HtmlHelperExtensions**类的`React`方法，并将模型传递给它。该**Razor**反过来致使已被宣布为一个**阵营**的组成部分。`CartView`

#### 结帐细节

![img](https://www.codeproject.com/KB/aspnet/1208668/Success.png)

*结帐成功页面。*
