# DAILY NOTES 

by Dadaxin

written in 16th to 20th in Jan.,2019




## 16th

今日内容：Bootstrap Table学习、

### Bootstrap Table

以下来自[官网](https://bootstrap-table.wenzhixin.net.cn/docs/getting-started/usage/)

#### 1.入门模板

要引入的文件：

- bootstrap-table.min.css
- bootstrap-table.min.js

```html
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/css/bootstrap.min.css" integrity="sha384-GJzZqFGwb1QTTN6wy59ffF1BuGJpLSa9DkKMp0DgiMDm4iYMj70gZWKYbI706tWS" crossorigin="anonymous">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.6.3/css/all.css" integrity="sha384-UHRtZLI+pbxtHCWp1t77Bi1L4ZtiqrqD80Kn4Z8NTSRyMA2Fd33n5dQ8lWUE00s/" crossorigin="anonymous">
    <link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/bootstrap-table/1.13.1/bootstrap-table.min.css">

    <title>Hello, Bootstrap Table!</title>
  </head>
  <body>
    <table data-toggle="table">
      <thead>
        <tr>
          <th>Item ID</th>
          <th>Item Name</th>
          <th>Item Price</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>1</td>
          <td>Item 1</td>
          <td>$1</td>
        </tr>
        <tr>
          <td>2</td>
          <td>Item 2</td>
          <td>$2</td>
        </tr>
      </tbody>
    </table>

    <!-- jQuery first, then Popper.js, then Bootstrap JS, and then Bootstrap Table JS -->
    <script src="https://code.jquery.com/jquery-3.3.1.min.js" integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8=" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.6/umd/popper.min.js" integrity="sha384-wHAiFfRlMFy6i5SRaxvfOCifBUQy1xHdJ/yoi7FRNXMRBu5WHdZYu1hA6ZOblgut" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/js/bootstrap.min.js" integrity="sha384-B0UglyR+jN6CkvvICOB2joaf5I4l3gm9GU6Hc1og6Ls7i6U/mkkaduKaBhlAXv9k" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/core-js/2.6.2/core.min.js"></script>
    <script src="//cdnjs.cloudflare.com/ajax/libs/bootstrap-table/1.13.1/bootstrap-table.min.js"></script>
  </body>
</html>
```



#### 2.基本用法

bootstrap Table插件可以通过数据属性或JS以表格格式显示数据。

- 通过数据属性：

```html
<table data-toggle="table" data-url="data1.json" data-pagination="true" data-search="true">
  <thead>
    <tr>
      <th data-sortable="true" data-field="id">Item ID</th>
      <th data-field="name">Item Name</th>
      <th data-field="price">Item Price</th>
    </tr>
  </thead>
</table>
```

其中，`data-url="data1.json"`使用远程URL数据。可以通过`pagination`、`search`和`sorting`来添加导航、搜索和分类。

- 通过JS：

```html
<table id="table"></table>
```

```javascript
$('#table').bootstrapTable({
  pagination: true,
  search: true,
  columns: [{
    field: 'id',
    title: 'Item ID'
  }, {
    field: 'name',
    title: 'Item Name'
  }, {
    field: 'price',
    title: 'Item Price'
  }],
  data: [{
    id: 1,
    name: 'Item 1',
    price: '$1'
  }, {
    id: 2,
    name: 'Item 2',
    price: '$2'
  }]
})
```

先写一个空表格，再用`bootstrapTable()`初始化。

#### 3.显示数据方式

Bootstrap-Table显示数据到表格的方式有两种，一种是**客户端（client）模式**，一种是**服务器（server）模式**。

客户端模式，指的是在服务器中把要显示到表格的数据一次性加载出来，然后转换成JSON格式传到要显示的界面中。

服务器模式，指的是根据设定的每页记录数和当前要显示的页码，发送数据到服务器进行查询，然后再显示到表格中。该方法可以根据用户的需要动态的加载数据，节省了服务器的资源，但是不能使用其自带的全数据搜索功能。因为你加载的数据只是一页的数据，所以全数据搜索的范围也只在一页之中。





## 17th,Jan.



### 前后端数据传参

在MVC之间进行数据传递的时候可以有三种方式，ViewData、ViewBag和ViewModel。此三种方式下，数据都是以Model类的对象的形式传递。

前后端传参的方式也可以是使用Json字符串，过程是数据库数据—>json字符串—>表格数据。此时的表格可以利用一些插件来完成，例如Bootstrap Table。



### MVC七天总结

#### 简单MVC数据传递

1. 创建Model类。

```c#
public class Employee
{
    public string FirstName{get;set;}
    ···
}
```
2. 在Controller的方法中获取创建Model类的对象，并为其赋值。

  创建ViewData，将对象传给ViewData，并返回View给浏览器。

```c#
Employee emp=new Employee();
emp.FirstName="Sukesh";
```
```c#
ViewData["Employee"]=emp;
return View("MyView");
```
4. 在View中，从ViewData获取数据并显示。
```html
@{
    Demo.Models.Employee employee=(Demo.Models.Employee)ViewData["Employee"]；
}
<td>@employee.FirstName</td>
```

**Controller是协调者的角色，接收浏览器的Request，执行操作，将Model的数据传给View，并将View传回浏览器。**



#### 当使用ViewModel时

与上述过程不同的是，在Controller中，直接**将ViewModel对象和View名称一起作为参数传给`View()**`。

```c#
return View("MyView",emp);//此emp是ViewModel对象
```

ViewModel是View的强类型，与Model没直接关系。



#### 当前端有表格时

可以将表格要呈现的数据用泛型类List<T>表示。
```C#
public class EmployeeListViewModel
{
  public List<EmployeeViewModel>Employees{get;set;}
  ···
}
```
```C#
public class EmployeeViewModel
{
  string EmployeeName{get;set;}
}
```
此时，我们可以看到有两个ViewModel。

其中，*EmployeeListViewModel*包含要呈现视图所需的所有数据。



**而*EmployeeViewModel*的属性就是每行的字段。一个*EmployeeViewModel*对象就对应表格的一行，也就对应*Employees*集合中的一个EmployeeViewModel类型的一个item。【理解List<T>的时候，可以把它装作一个数组。只是，数组的数据类型是int、float等，而泛型的数据类型是类。】**



呈现表格的代码：

```html
@model EmployeeListViewModel
···
<table>
  @foreach(EmployeeViewModel item in in Model.Employees)
  {
      <tr>
        <td>@item.EmployeeName</td>
      </tr>
  }
</table>
```



#### 该程序的结构理解

基于前面的典型MVVM（Model-VIew-ViewModel)结构，加上以下数据传递和处理部分。

- 在*Data Access Layer*中，新建一个类**SalesERPDAL**，该类继承自**DbContext**。
该类做了两件事：
  1. 生成数据表：在该类中重写了`OnModelCreating`方法，该方法利用已创建好的Model类生成数据表。备注：在此教程中，程序与数据库的连接通过配置文件中的`<connectionstring>`实现。
  2. 新建数据集存放数据：添加数据集属性。
```C#
protected override void OnModelCreating(DbModelBuilder modelBuilder)
{
    modelBuilder.Entity<Employee>().ToTable("TblEmployee");
    base.OnModelCreating(modelBuilder);
}
public DbSet<Employee> Employees{get;set;}
```
- 在类**EmployeeBusinessLayer**中，`GetEmployees()`将创建**SalesERPDAL**的对象，并将其返回为`List<Employee>`类型。
```C#
public List<employee> GetEmployees()
{
    SalesERPDAL salesDal = new SalesERPDAL();
    return salesDal.Employees.ToList();
}
```
本示例中，将数据库的数据放在了DataSet里面。



结构如下图：

![MVC结构](https://github.com/Dadaxin/Daily-Notes/tree/master/img/MVC7Days.png)

