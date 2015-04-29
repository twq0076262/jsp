# JSP——生命周期

理解 JSP 的低级功能的关键是理解它们遵循的简单的生命周期。

JSP 生命周期可以被定义为从创建到销毁的整个过程，这类似于一个 servlet 的生命周期与一个额外的步骤，该步骤将一个 JSP 编译成 servlet。

以下是 JSP 带着的步骤

- 编译

- 初始化

- 执行

- 清理

JSP 生命周期的四个主要阶段非常类似于 Servlet 生命周期，它们如下所示：

![lifecyle1](../images/life_cycle1.jpg)

## JSP 编译：

当浏览器请求一个 JSP，JSP 引擎首先检查是否需要编译页面。如果页面从未被编译，或者 JSP 自上次编译后被修改了，那么 JSP 引擎就会编译页面。

编译过程包括三个步骤：

- 解析 JSP。

- 将 JSP 转换为 servlet。

- 编译 servlet。

## JSP 初始化：

当容器加载 JSP时，在响应任何请求之前它会调用 jspInit()方法。如果你需要执行 JSP-specific 初始化，那么就覆盖 jspInit()方法：

``` 
public void jspInit(){
  // Initialization code...
}
```

通常初始化只执行一次，servlet init 方法也是只执行一次。一般初始化数据库连接，打开文件，并在 jsplnit 方法中创建查找表。

## JSP 执行：

JSP 生命周期的这个阶段代表所有的交互请求，直到 JSP 被摧毁。

当浏览器请求一个 JSP 页面时并且该页面被加载并初始化，JSP 引擎就会在 JSP 中调用**_jspService()** 方法。 

_jspService() 方法接受一个 **HttpServletRequest** 和一个 **HttpServletResponse** 作为其参数，如下所示：

``` 
void _jspService(HttpServletRequest request, 
                 HttpServletResponse response)
{
   // Service handling code...
}
```

每次请求时 JSP 的 _jspService()方法都会被调用，且该方法负责生成请求的响应，并且该方法还负责生成所有七个 HTTP 方法的反应，即 GET、POST、DELETE 等。

## JSP 清理：

JSP 生命周期的破坏阶段代表 JSP 从容器中删除。

**jspDestroy()**方法是 JSP 的相当于 servlet 的销毁方法。当你需要执行任何清理时，覆盖 jspDestroy，比如释放数据库链接或关闭打开的文件。

jspDestroy()方法具有以下形式：

``` 
public void jspDestroy()
{
   // Your cleanup code goes here.
}
```


