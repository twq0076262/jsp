# JSP——环境配置

开发环境是你将开发 JSP 程序、测试程序并最终运行程序的地方。

本教程将指导你设置 JSP 开发环境，包括以下步骤：

## 设置 Java 开发工具包

这一步涉及到下载 Java 软件开发工具包(SDK)的实现并正确的设置 PATH 环境变量。

你可以从 Oracle 的 Java 站点下载 SDK：[**Java SE 下载**](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。

当你下载 Java 实现之后，按照给定的指示来安装和配置设置。最后设置路径和 JAVA_HOME 环境变量来引用目录，其中包含 java 和 javac，通常分别是 java_install_dir/bin 和 java_install_dir。

如果你运行的是 Windows，且 SDK 安装在 C:\ jdk1.5.0_20 中，将以下行添加到你的 C:\ autoexec.bat 文件中。

``` 
set PATH=C:\jdk1.5.0_20\bin;%PATH%
set JAVA_HOME=C:\jdk1.5.0_20
```

另外，在 Windows NT / 2000 / XP 系统中，你也可以右键单击我的电脑，选择属性，然后单击高级系统设置，选择环境变量。之后，你可以更新路径值，然后按下 OK 按钮。

在 Unix(Solaris ，Linux 等等)系统中，如果 SDK 安装在 /usr/local/jdk1.5.0_20 中，你使用 C shell，将以下行添加到你 .cshrc 文件中。

``` 
setenv PATH /usr/local/jdk1.5.0_20/bin:$PATH
setenv JAVA_HOME /usr/local/jdk1.5.0_20
```

另外，如果你使用一个集成开发环境(IDE)，如 Borland JBuilder、Eclipse、IntelliJ IDEA 或 Sun ONE Studio，就编译并运行一个简单的程序来确认 IDE 知道你在哪安装了 Java。

## 设置 Web 服务器：Tomcat

许多支持 JavaServer Pages 和 Servlets 开发的 Web 服务器都能在市场中找到。一些 web 服务器是免费下载的，Tomcat 就是其中之一。

Apache Tomcat 是 JSP 和 Servlet 技术的一个开源软件实现，可以作为一个独立的服务器测试 JSP 和 Servlet，并且可以与 Apache Web 服务器集成。下面是在计算机上安装 Tomcat 的步骤：

- 从 [http://tomcat.apache.org/](http://tomcat.apache.org/) 下载最新版本的 Tomcat。

- 下载安装后，解压二进制发行版到一个方便的位置。例如 windows 系统中的 C:\ apache-tomcat-5.5.29 位置，或在 Linux / Unix 系统中的 /usr/local/apache-tomcat-5.5.29 位置，然后创建 CATALINA_HOME 环境变量来指向这些位置。

在 windows 系统的计算机中，可以通过执行以下命令来启动 Tomcat：

``` 
%CATALINA_HOME%\bin\startup.bat 
```

或

``` 
C:\apache-tomcat-5.5.29\bin\startup.bat 
```

在 Unix(Solaris，Linux 等)系统的计算机中，可以通过以下命令来启动 Tomcat：

``` 
$CATALINA_HOME/bin/startup.sh 
```

或

```
/usr/local/apache-tomcat-5.5.29/bin/startup.sh 
```

启动成功后，通过访问 **http://localhost:8080 /**，包含 Tomcat 的默认的 web 应用程序将是可用的。如果一切进展顺利，那么应该显示如下结果： 

![environment1](../images/envirnoment1.jpg)

关于配置和运行 Tomcat 的更多信息可以在这里的文档中找到，也可以在 Tomcat 网站中找到：http://tomcat.apache.org

在 windows 系统的计算机中，可以通过执行以下命令来结束 Tomcat：

``` 
%CATALINA_HOME%\bin\shutdown
```

或

```
C:\apache-tomcat-5.5.29\bin\shutdown
```

在 Unix(Solaris，Linux 等)系统的计算机中，可以通过以下命令来结束 Tomcat：

``` 
$CATALINA_HOME/bin/shutdown.sh
```

或

```
/usr/local/apache-tomcat-5.5.29/bin/shutdown.sh
```

## 设置类路径 


由于 servlet 不是标准版 Java 平台的一部分，你必须为编译器识别 servlet 类。

如果你运行的是 Windows 系统，你需要把以下行添加到 C:\ autoexec.bat 文件中。

``` 
set CATALINA=C:\apache-tomcat-5.5.29
set CLASSPATH=%CATALINA%\common\lib\jsp-api.jar;%CLASSPATH%
```

另外，在 Windows NT / 2000 / XP 系统中，你也可以右键单击我的电脑，选择属性，然后单击高级系统设置，选择环境变量。之后，你可以更新路径值，然后按下 OK 按钮。

在 Unix(Solaris ，Linux 等等)系统中，如果你使用的是 C shell，可以将以下行添加到你 .cshrc 文件中。

``` 
setenv CATALINA=/usr/local/apache-tomcat-5.5.29
setenv CLASSPATH $CATALINA/common/lib/jsp-api.jar:$CLASSPATH
```

**注意：** 假设你的开发目录是 C:\ JSPDev(Windows 系统)或 /usr/JSPDev(Unix 系统)，那么你需要以上述类似的方式在类路径中添加这些目录。
