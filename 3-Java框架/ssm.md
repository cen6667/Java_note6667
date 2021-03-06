# web基础

## 基本概念

### 前言

web开发：

	- web 网页的意思

 - 静态web
   - html， css，
      - 提供给所有人看的数据始终不会发生变化
 - 动态web
   - 提供给所有人看的数据，会发生变化，每个人在不同的时间不同的地点看到的信息各不相同
      - 淘宝，几乎所有的网站都是
        - 技术栈  servlet/jsp  asp  php

在java中，动态web资源开发的技术统称为javaweb；

### web应用程序

web应用程序：可以提供浏览器访问的程序

​	a.html  b.html 多个web资源被整合起来就可以对外提供web服务

​	一个web应用由多个部分组成(静态web,动态web)

	-	html css js
	-	jsp servlet
	-	java程序
	-	jar包
	-	配置文件(Properties)

web应用程序编写完毕后，若想提供给外界访问，需要一个服务器来统一管理；

### 静态web

- *.htm *.html 这些都是网页文件的后缀，如果服务器上一直存在这些东西，我们就可以直接进行读取
- 静态web存在的缺点
  - web页面无法动态更新，所有用户看到的都是同一个页面
    - 轮播图，点击特效，伪动态
    - javascript[实际开发，他用的最多]
    - vbscript
  - 它无法和数据库交互(数据无法持久化，用户无法交互)

### 动态web

页面会动态展示: web的页面展示的效果因人而异

![image-20201121184950790](img/image-20201121184950790.png)

缺点：

 - 加入服务器的动态web资源出现了错误，我们需要重新编写我们的后台程序，重新进行发布；
   - 停机维护

优点：

	- web页面可以动态更新，所有用户看到的都可以定制化
	- 可以和数据库进行交互，数据可以持久化(可以和数据库进行访问)



新手村:--->魔鬼训练(分析原理，看源码)--->pk场





## web服务器

### web的一些开发技术

ASP:  微软的，早些年非常流行，在HTML中嵌入了VB的脚本，ASP+COM，在ASP开发中，基本一个页面都有几千行的业务代码，页面及其混乱，维护成本特别高！ 主要使用C#语言

jsp/servlet:

- sun公司主推的B/S架构(浏览器和服务器)，C/S架构(客户端和服务器)
- 主要的实现语言是基于JAVA语言(所有的大公司或一些开源的组件，都是用JAVA写)
- 可以承载高并发，高可用，高性能
- 语法结构像asp，加强市场的强度; ASP-->JSP



PHP  

- Php开发速度很快，功能很强大，跨平台，代码很简单(70% wordpress);
- 无法承载大访问量情况, 有一些局限性!

### web服务器

服务器是一种被动的操作，用来处理用户的一些请求和给用户一些响应信息。

Tomcat

百度一下tomcat的资料

IIS : 微软的公司，主要跑一些ASP的程序，Windows自带的



## Tomcat

### Tomcat安装

![image-20201121194019952](img/image-20201121194019952.png)

tomcat官网：https://tomcat.apache.org/



### Tomcat启动和配置

文件夹作用和信息

![image-20201121193937523](img/image-20201121193937523.png)





**启动.关闭 Tomcat**

启动 startup.bat

关闭 shutdown.bat

访问http://localhost:8080

可能遇到的问题：

​	1、java环境变量么有配置，tomcat会闪退，需要配置java_home,java_path

​	2、闪退问题

​	3、 乱码问题

### Tomcat配置

![image-20201121200020206](img/image-20201121200020206.png)

**可以配置启动的端口号 port**

    <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />

tomcat 默认端口号 8080

mysql默认端口号3306

HTTPS 默认端口 443

HTTP 默认端口 80

**可以配置启动的appBase:webapps，可以配置启动的Host主机名称:localhost** 

```xml
  <Host name="localhost"  appBase="webapps"
        unpackWARs="true" autoDeploy="true">
        
   <Host name="www.qinjiang.com"  appBase="webapps"
        unpackWARs="true" autoDeploy="true">       
        
```

高难度面试题：

请你谈谈网站是如何进行访问的! 百度作业! DNS解析流程

用户----> 本机浏览器----------------用户发起请求--------------------------->查询本机etc/hosts



本机浏览器----------------3.用户发起请求------------------------------------->LocalDNSServer

-

LocalDNSServer-----------4.请根域名发起解析请求----------------------------->Root DNS Server

LocalDNSServer<----------5.返回gTLD域名解析服务器地址---------------------Root DNS Server



LocalDNSServer-----------6.向gTLD域名解析服务器发起解析请求--------------->gTLD Server

LocalDNSServer<-----------7.返回NameServer的服务器地址--------------------gTLD Server



LocalDNSServer-----------8.查询请求的域名对应的IP地址----------------------->Name Server

LocalDNSServer<-----------9.返回域名对应的IP地址------------------------------Name Serverr



LocalDNSServer-----------10.返回域名对应的IP地址----------------------------->本机浏览器





### 配置tomcat环境变量(可选项)

```properties
##先配置环境变量
CATALINA_BASE =F:\Environment\apache-tomcat-9.0.38
CATALINA_HOME = F:\Environment\apache-tomcat-9.0.38

## 配置path
%CATALINA_HOME%\lib
%CATALINA_HOME%\bin
```



### 发布一个web网站

不会就先模仿

 - step1 将自己写的网站，放到服务器tomcat中指定的web应用的文件夹(webapps)下，就可以出来了；

 - step2 网站应该有的结构如下图

   ```java
   --webapps : Tomcat服务器的web目录
   	---Root
   	---kuangstudy:网站的目录名
   		- WEB-INF		放网站的程序
           	--class  java程序
           	--lib     web应用锁依赖的jar包
   			--web.xml  网站的配置文件
   		- index.html 默认的首页
   		- static
   			-css
   				-style.css
   			- js
   			- img
   		- .....
   ```

   

## HTTP

### 两个时代

- http1.0
  - http1.0  客户端可以与服务器连接后，只能获得一个web资源，断开连接
- http2.0
  - http2.0  客户端可以与服务器连接后，只能获得一个web资源，断开连接



### http请求(Request)

[http协议讲解](https://blog.csdn.net/sinat_41620463/article/details/81019962)

http协议有个request，分为request 和response 
从浏览器向服务器发起请求一般用resquest，从服务器返回一般是response
每个resquest和response 都由三部分组成，分别为 Line、header 、body
line 在request 中可能是 get: ![img](file:///C:\Users\admin\AppData\Roaming\Tencent\QQTempSys\[5UQ[BL(6~BS2JV6W}N6[%S.png)http://www.baidu.com http 1.1
    在response中可生是 status:200 ok
header： 即可由服务器设置，告诉浏览器按照什么约束执行
             也可由服务器设置，告诉服务器提供什么约束格式返回



客户端--发起请求---服务器

```
General 请求体:
Request URL  请求地址 https://www.baidu.com
Request Method get/post方法
Status Code ：200 ok  状态码 200
Remote（远程） Address 14.215.177.59:443
```

```java
Request headers 请求头:
Accept:text/html
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Cache-Control: max-age=0
Connection: keep-alive
```

1、请求体	

	- 请求行中的请求方式，get  

 - 请求方式 get,post,head,delete,put,tract......(restful)
   - get 请求能够携带的参数比较少，大小有限制，会在浏览器的url地址栏显示出数据内从，不安全，但是高效
   - post 请求能够携带的参数比较多，大小无限制，不会在浏览器的url地址栏显示出数据内容，安全，但不是高效

2、请求头

```
Accept  浏览器端可以接受的媒体类型
Accept-Encoding	浏览器申明自己接收的编码方法，通常指定压缩方法，是否支持压缩，支持什么压缩方法,支持哪种编码方式 gbk, utf-8 gb2312 iso8859-1
Accept-Language	浏览器申明自己接收的语言,告诉浏览器，他的语言环境
Cache-control	这个是非常重要的规则。 这个用来指定Response-Request遵循的缓存机制 Cache-Control:no-cache  所有内容都不会被缓存 缓存控制
connection	Connection: keep-alive   当一个网页打开完成后，客户端和服务器之间用于传输HTTP数据的TCP连接不会关闭，如果客户端再次访问这个服务器上的网页，会继续使用这一条已经建立的连接,
告诉浏览器，请求完成是断开还是保持连接
HOST  发送请求时，该报头域是必需的）主机
```

### http响应（Response）

```
响应头：
Cache-Control: private 	//缓存控制
Connection: keep-alive   //连接 保持连接
Content-Encoding: gzip		// 编码
Content-Type: text/html;charset=utf-8  //类型
Date: Sun, 22 Nov 2020 03:24:17 GMT
Expires: Sun, 22 Nov 2020 03:24:17 GMT
Server: BWS/1.1
Set-Cookie: BDSVRTM=313; path=/   
Set-Cookie: BD_HOME=1; path=/
Set-Cookie: H_PS_PSSID=32818_1436_33102_33119_33061_31254_33098_33100_32962_26350; path=/; domain=.baidu.com
Strict-Transport-Security: max-age=172800
Traceid: 1606015457060115431411151445472357802237
Transfer-Encoding: chunked
X-Ua-Compatible: IE=Edge,chrome=1
```



2、响应体，和消息一样

```
Accept  告诉浏览器，服务器锁支持的数据类型
Accept-Encoding	支持哪种编码方式 gbk, utf-8 gb2312 iso8859-1
Accept-Language	告诉浏览器，他的语言环境
Cache-control	缓存控制
connection	告诉浏览器，请求完成是断开还是保持连接
HOST  主机
Refresh  告诉客户端，多久刷新一次
Location  让网页重新定位:
```



### 响应状态码(重点)

200 请求响应成功

404 找不到资源

​	4XX 资源不存在

3** 请求重定向

	- 重定向 你重新定位到我给你的新位置去；

5xx  服务器代码错误  500 502网关错误





## Maven

我为什么要学习这个技术？

​	在javaweb开发中，需要导入大量的jar包，我们手动导入，很繁琐，如何让一个东西自动帮我们导入和配置这个jar包，由此Maven诞生了，Maven是一个工具，帮助我们来管理jar包，是一个项目架构管理工具! 我们用他就是方便我们导入jar包!

​	Maven核心思想：约定大于配置!

	-	有约束，不要去违反
	-	Manven会规定好你改如何去编写我们的Java代码，必须要按照这个规范去走!

安装Maven: 官网地址：https://maven.apache.org/index.html

![image-20201122120620436](img/image-20201122120620436.png)

Maven对应的目录解释:



小狂神友情建议，下载后所有的文件放到一个文件夹下面管理

### 5.1 配置Maven环境变量

step1. 进入我们的系统环境变量中，配置如下的配置：

M2_HOME   **F:\Environment\apache-maven-3.6.3\bin**

MAVEN_HOME  **F:\Environment\apache-maven-3.6.3**

![image-20201122121306352](img/image-20201122121306352.png)

step2 .进入系统的path，配置MAVEN_HOME

​	%MAVEN_HOME%\bin

![image-20201122121429863](img/image-20201122121429863.png)

经过上述步骤，就配置成功了,可以在命令行执行 mvn -version进行测试

![image-20201122121751759](img/image-20201122121751759.png)

注意：配置M2_HOME的原因是因为后续学习spring_boot， spring等框架都需要用到这个目录

### 5.2 配置阿里云镜像

镜像 mirrors 加速下载作用

添加步骤：

​	1、 进入自己的maven安装目录，找到F:\Environment\apache-maven-3.6.3\conf文件夹，

​	2、打开 settings.xml 并在文件的  <mirrors></mirrors>中间添加如下配置

```xml
  <mirrors>
     <!-- 阿里云仓库 -->
    <mirror>
        <id>nexus-aliyun</id>
        <mirrorOf>*,!jeecg,!jeecg-snapshots</mirrorOf>
        <name>Nexus aliyun</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public</url>
    </mirror>
  </mirrors>
```

### 5.3 配置本地仓库

本地仓库 远程仓库

建立一个本地仓库，存储网络下载下来的jar包 

操作步骤：

1、 进入自己的maven安装目录，找到F:\Environment\apache-maven-3.6.3\conf文件夹，

​	2、打开 settings.xml 并在文件的   <localRepository></localRepository>中间添加如下配置

```xml
  <!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  <localRepository>F:\Environment\apache-maven-3.6.3\maven-repo</localRepository>
  -->
  <localRepository>F:\Environment\apache-maven-3.6.3\maven-repo</localRepository>
```



### 5.4 在IDEA中使用MAVEN

step1 启动IDEA，创建一个Maven项目

![image-20201122125403471](img/image-20201122125403471.png)

step2点击Next, 配置项目的信息

![image-20201122125651754](img/image-20201122125651754.png)

​		上述填写 

​			- groupid: top.aigoo

​			- Artifactid: javaweb-01-maven

​			- name: javaweb-01-maven

step3 点击Next，配置maven的本地地址;

![image-20201122130348157](img/image-20201122130348157.png)

至此就创建成功，进入IDEA等待项目初始化完毕

![image-20201122130919974](img/image-20201122130919974.png)

Step4. IDEA中的MAVEN设置;

​	注意事项:创建完项目，需要进入到Setting里面看一眼Maven配置，确认是否是本地的配置。进入方式是 File--->settings--->Build Execution Deployment-->build tools--->Maven

![image-20201122131540259](img/image-20201122131540259.png)



Step5. 到这里，maven在idea中的配置和使用就OK了



### 5.5 创建一个普通的Maven项目

我们可以通过创建一个meven，但是不选择模板的方式创建一个干净的Maven项目

![image-20201122134806617](img/image-20201122134806617.png)



所以，使用模板创建的项目需要补充java 和resources文件夹，如下图

![image-20201122140114318](img/image-20201122140114318.png)



### 5.6 在IDEA中配置TOMCAT

Step1 先点击Add Configuration

![image-20201122140611198](img/image-20201122140611198.png)

Step2 。选择Tomcat Server

![image-20201122140652058](img/image-20201122140652058.png)

Step3 .填写对应的tomcat配置信息

![image-20201122141423459](img/image-20201122141423459.png)

Step4.新建一个tomcat artifacts

![image-20201122141809214](img/image-20201122141809214.png)

解决警告的问题，为什么会有这个问题：我们访问一个网站，需要指定一个文件夹的名字，而且必须要配置一个artifacts

Step 5.关于虚拟路径的设置

![image-20201122142255188](img/image-20201122142255188.png)



### 5.7 pom文件

pom.xml是maven的核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--Maven的版本和头文件-->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
<!--  这里是我们刚才配置的GAV-->
  <groupId>top.aigoo</groupId>
  <artifactId>javaweb-01-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
<!--  package：项目的打包方式
    jar:java应用
     war javaweb应用-->
  <packaging>war</packaging>

  <name>javaweb-01-maven Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>
  <!--配置-->
  <properties>
    <!--项目的默认构建编码-->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--编码的版本-->
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>
  </properties>
  <!--项目依赖-->
  <dependencies>
    <!--具体依赖的jar包的配置文件-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
    </dependency>

  </dependencies>
<!--项目构建用的东西-->
  <build>
    <finalName>javaweb-01-maven</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>
```

**maven 由于他的约定大于配置，我们之后可能会遇到我们写的配置文件，无法被导出或者生效的问题，而我们解决方案：**

```xml
<!--在build中配置resources,来防止我们资源导出失败的问题-->
   <build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
    </build>
```

### 5.8 解决遇到的问题

1、Maven3.6.2 版本问题，所有依赖无法导入

2、Tomcat闪退

3、IDEA中每次都需要重复配置Maven

4、Maven项目中Tomcat无法配置

5、maven默认web项目中web.xml的版本问题，替换为tomcat中ROOT下xml一样的文件

```xml
<?xml version="1.0" encoding="UTF-8"?>

<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">

  
</web-app>
```

7、Maven仓库的使用

直接百度Maven Responsity  https://mvnrepository.com/



### 5.9 编写自己第一个HttpServlet

step1.首先，我们创建一个Maven项目，如上述步骤，并在src/main/java下新建一个包 top.aigoo，在这个包里面建立一个HelloServlet的java文件

![image-20201122165118470](img/image-20201122165118470.png)

学习小技巧:

 - 如何快速知道去写一个servlet程序

   在tomcat的examples，有很多的例子，我们可以启动tomcat，然后访问examples里面的文件，然后找到自己需要的例子就可以

 - 如何去快速把项目的依赖包加载到Maven中

   可以在项目中，引入包的文件，点下 ctrl+enter ，选择Add to Maven，这样可以在本地的Maven库进行查找

- 如何快速定位HttpServlet所来自的包?

  首先，我们看tomcat可以启动这个例子，所以这个jar包在tomcat中肯定有，我们可以去tomcat/lib目录找一些相似的，进入里面可以发现有个名字叫做servlet-api.jar

  然后，我们可以去maven仓库，搜索httpservlet，但是没有搜索到，然后尝试搜索servlet-api，我们能够找到很多个servlet-api，这个时候参照tomcat里面例子代码，可以知道是来自于javax.servlet.XXX，所以我们选择一个类似的

  我们找到这个包，把dependce加入到自己项目的pom.xml中，并刷新；

  在这个过程中，我们还发现加了这个包并未正常运行，所以我们可以选择ctrl+enter 然后直接add

Step2. 编写我们的servlet文件

```java
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

public class HelloServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html");
        response.setCharacterEncoding("utf-8");
        PrintWriter out = response.getWriter();
        out.println("<html>");
        out.println("<head>");
        out.println("<title>大家是个好学生!</title>");
        out.println("</head>");
        out.println("<body>");
        out.println("<h1>大家是个好学生!</h1>");
        out.println("</body>");
        out.println("</html>");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}
```

step3. 编辑我们的web.xml，这个是项目的主要文件，我们需要进去配置我们的路由

```xml
<?xml version="1.0" encoding="UTF-8"?>

<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">
        <!--首先我们需要配置servlet，name可以随便写，class需要和自己的servlet对应-->
        <servlet>
            <servlet-name>helloServlet</servlet-name>
            <servlet-class>top.aigoo.HelloServlet</servlet-class>
        </servlet>
        <!--还需要配置servlet和自己路由的配对， 这个意思从浏览器http://localhost:8080/kuang/kuang2 就可以访问，-->
        <servlet-mapping>
            <servlet-name>helloServlet</servlet-name>
            <url-pattern>/kuang2</url-pattern>
        </servlet-mapping>
</web-app>

```



备注：

```
<!--首先我们需要配置servlet，name可以随便写，class需要和自己的servlet对应-->
 <!--还需要配置servlet和自己路由的配对， 这个意思从浏览器http://localhost:8080/kuang/kuang2 就可以访问，其中/Kuang/ 是在tomcat里面配置的Deployment里面的Application context，-->
```

![image-20201122170221397](img/image-20201122170221397.png)

### 5.10 关于父子项目遇到的一些坑

- 问题1、 安装了父子项目后，子项目无法继承父项目的依赖，同时子pom.xml变为灰色

  解决办法：进入settings-->Maven, 找到ignoredFiles, 将父pom.xml前面的√取消掉

- 问题2.生成子项目时候，刚开始的parent属性被自动刷掉了

  解决办法：待生成项目时候，拷贝下来，等子pom稳定后，在覆盖回去，或者直接手打 

  ```
    <parent>
      <artifactId>javaweb-02-servlet</artifactId>
      <groupId>top.aigoo</groupId>
      <version>1.0-SNAPSHOT</version>
    </parent>
  ```

- 问题3 删掉子项目，重新建立Module,在输入项目名，groupid和artifactid显示红色

  因为有缓存，关闭项目，重新打开就可以了

- 问题4. 在子项目的target---[WEB-INF]里面没有lib目录

  通过上述问题，勾选掉父pom.xml文件，然后这个问题得到了解决了!



## servlet

### 6.1 servlet简介

Sun公司开发动态web的一门技术

Sun在这些API中提供一个接口叫做Servlet，如果你想开发一个动态web的程序，只需要完成两个小步骤

	- 编写一个类，实现servlet的接口
	- 把开发好的servlet类，部署到web服务器中

我们会把实现了servlet接口的java程序叫做Servlet

### 6.2 helloservlet

Servlet接口在Sun公司有一两个默认的实现类，HttpServlet，GenericServlet



**step1. 构建一个普通的maven项目，删掉里面的src目录，以后我们的学习就在里面建立module**

项目名称：javaweb-03-servlet

**step2. 关于maven父子工程的简介**

	- 在父项目中会多一个modules

```xml
    <modules>
        <module>servlet-01</module>
    </modules>
```



	- 在子项目会多一个parent（在idea 202.1版本没有自动生成这个目录，但是删掉groupid就可以正常用了）

```xml
  <parent>
    <artifactId>javaweb-02-servlet</artifactId>
    <groupId>top.aigoo</groupId>
    <version>1.0-SNAPSHOT</version>
  </parent>
```

父项目中的java,子项目可以直接使用

> son extends father

注意，如果是子类的项目，那么在pom.xml里面，就可以不要存在<groupId>top.aigoo</groupId> 属性，不然子项目会找不到父项目的jar包



**step3. Maven的环境优化**

	1. 将web.xml的配置更新为最新的版本，我们可以到tomcat/webapps/ROOT里面找到对应的配置

```xml
<?xml version="1.0" encoding="UTF-8"?>

<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">
    
</web-app>
```

2. 添加java和resources文件夹

![image-20201122192133551](img/image-20201122192133551.png)



3. 将maven的结构搭建完整



step4. 编写一个Servlet程序

	- 编写一个普通类
	- 实现Servlet接口,这里直接继承HttpServlet，Servlet的继承关系如下图

 ![image-20201122193141687](img/image-20201122193141687.png)



```java
package top.aigoo.servlet;


import javax.servlet.ServletException;
import javax.servlet.ServletInputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletInputStream inputStream = req.getInputStream();
        System.out.println("doGet()");
        PrintWriter writer = resp.getWriter();
        writer.println("Hello World ,Servlet");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



step5 编写servlet的映射

编写完成后，我们需要进入到web.xml里面，去编写servlet映射

```xml
<!--注册servlet-->
<servlet>
    <servlet-name>hello</servlet-name>
    <servlet-class>top.aigoo.servlet.HelloServlet</servlet-class>
</servlet>
<!--servlet的请求路径-->
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

step6 配置tomcat



![image-20201122194748111](img/image-20201122194748111.png)

step7 启动项目

### 6.3 Servlet原理

Servlet是由web服务器调用，web服务器在收到浏览器请求之后，会：

![image-20201122215837769](img/image-20201122215837769.png)





### 6.4 Mapping问题

1、1个Servlet可以指定一个映射路径

```xml
    <!--servlet的请求路径-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello1</url-pattern>
    </servlet-mapping>
```



2、1个Servlet可以指定多个映射路径

```xml
    <!--servlet的请求路径-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello1</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello2</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello3</url-pattern>
    </servlet-mapping>
```



3、1个Servlet可以指定通用的映射路径

```xml
    <!--servlet的请求路径-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello/*</url-pattern>
    </servlet-mapping>
```

如果用/* 那就是默认请求路径，包括Index.html都会转移到这个请求地址



4、可以指定一些后缀实现请求映射

```xml
    <!--servlet的请求路径-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>*.hello</url-pattern>
    </servlet-mapping>
```

注意，*前面不能加项目的映射路径   /hello/\*.hello和     /\*.qinjiang 这个就会报错

6、优先级问题

指定了固有的mapping映射路径，优先级最高，如果找不到就会走默认的处理路径

```xml
<url-pattern>/hello</url-pattern>   //访问http://localhost:8080/s1/hello  会走这个
<url-pattern>/*</url-pattern>     
```

常用的一些方式：自定义404



解决Tomcat 在IDEA里面显示乱码的问题

- 1.Tomcat 容器下Conf文件夹logging.properties

```properties
如果是GBK改为UTF-8

java.util.logging.ConsoleHandler.encoding = UTF-8

```

- 2. 如果是IDEA2019.3以后版本，在工具栏help -》 Edit Custom VM Options，加上

> -Dfile.encoding=UTF-8

- 3、在tomcat启动参数中，加入参数

> -Dfile.encoding=UTF-8

- 在IDEA-setting-editr-fileEncodings，里面所有都改为utf-8  如下图

![image-20201123132711460](img/image-20201123132711460.png)

### 6.5 ServletContext 应用

 getServletContext（）

web容器在启动的时候，他会为每个web程序都创建一个ServletContext对象，他代表当前的web应用

- **案例1.共享数据 ，在一个servlet放置的数据，可以通过ServletContext被另一个servlet获取**

```java
//1. HelloServlet  ServletContext里面写入数据
public class HelloServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Hello");
        //this.getInitParameter()   //初始化参数
        //this.getServletContext()  上下文
        //this.getServletConfig()  //servlet配置
        ServletContext servletContext = this.getServletContext(); //获取当前Servlet的上下文对象
        String userName ="秦僵"; //定义一个准备写入到ServletContext中的变量
        servletContext.setAttribute("userName", userName); //添加到ServletContext

        resp.setContentType("text/html");  
        resp.setCharacterEncoding("utf-8");
        resp.getWriter().println("刚才已经向ServletContext里面写入了一个userName:秦僵");
    }
}

//2. GetCharServlet  从ServletContext里面读数据

public class GetCharServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext servletContext = this.getServletContext();
        String userName = (String)servletContext.getAttribute("userName");

        resp.setContentType("text/html");
        resp.setCharacterEncoding("utf-8");
        resp.getWriter().println("姓名:"+userName);
    }
}

//3. 对应的xml文件

    <!--注册servlet-->
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>top.aigoo.servlet.HelloServlet</servlet-class>
    </servlet>

    <servlet>
        <servlet-name>getc</servlet-name>
        <servlet-class>top.aigoo.servlet.GetCharServlet</servlet-class>
    </servlet>

    <!--映射servlet-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>getc</servlet-name>
        <url-pattern>/getc</url-pattern>
    </servlet-mapping>
```

- **案例2 获取初始化参数，主要使用使用ServletContext的getInitParameter()**

```java
> 在项目servlet-02/web.xml配置初始化参数
<web-app>
    .....
    <!--配置servlet初始化参数-->
    <context-param>
        <param-name>jdbcDriver</param-name>
        <param-value>com.mysql.jdbcDriver</param-value>
    </context-param>
    <context-param>
        <param-name>url</param-name>
        <param-value>jdbc:mysql://localhost:3306/mysql</param-value>
	</context-param>
    <context-param>
        <param-name>user</param-name>
        <param-value>root</param-value>
    </context-param>
    <context-param>
        <param-name>passpord</param-name>
        <param-value>123456</param-value>
    </context-param>
    .....
</web-app>   
>>>>编写Servlet,使用ServletContext的getInitParameter()可以读取到web.xml文件的配置
 /*学习使用ServletContext获取初始化参数*/
public class ServletDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String url = this.getServletContext().getInitParameter("url");
        String jdbcDriver = this.getServletContext().getInitParameter("jdbcDriver");
        String user = this.getServletContext().getInitParameter("user");
        String passpord = this.getServletContext().getInitParameter("passpord");
        
        resp.getWriter().println("getInitParameter:jdbcDriver-->"+jdbcDriver);
        resp.getWriter().println("getInitParameter:url-->"+url);
        resp.getWriter().println("getInitParameter:user-->"+user);
        resp.getWriter().println("getInitParameter:passpord-->"+passpord);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}   


```

- **案例3 请求转发，主要使用使用ServletContext的getRequestDispatcher()**

```java
>> 实现ServletDemo3，使用getRequestDispatcher()请求转发
    public class ServletDemo3 extends HttpServlet {
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("ServletDeme03执行!");
        ServletContext servletContext = this.getServletContext();
        RequestDispatcher requestDispatcher = servletContext.getRequestDispatcher("/sd2");
        requestDispatcher.forward(req,resp);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

>> 配置web.xml
    <servlet>
        <servlet-name>sd2</servlet-name>
        <servlet-class>top.aigoo.servlet.ServletDemo2</servlet-class>
    </servlet>

    <servlet>
        <servlet-name>sd3</servlet-name>
        <servlet-class>top.aigoo.servlet.ServletDemo3</servlet-class>
    </servlet>
            
     <servlet-mapping>
        <servlet-name>sd2</servlet-name>
        <url-pattern>/sd2</url-pattern>
    </servlet-mapping>

    <servlet-mapping>
        <servlet-name>sd3</servlet-name>
        <url-pattern>/sd3</url-pattern>
    </servlet-mapping>          
```

注意，请求转发和重定向是不同的

请求转发是在服务器进行处理，直接转发到另一个请求，在前台看到的url不变，

重定向，是返回新的url给浏览器，浏览器再次去请求新的url地址



- **案例4 读取资源文件，项目大量用到Properties**

properties

	-	在java路径下新建properties
	-	在resources目录下新建properties

发现:都被大宝到了同一个路径下:classes,我们俗称这个路径为类路径

思路：需要一个文件流!

**做这题时候碰到一个坑： 因为之前在系统的环境变量没有配置tomcat，然后再这儿使用maven遇到问题，maven可以将resources里面资源打包到war包，但是用tomcat启动生成的war包，就没有resources资源，只有 src/main/java下的资源**

解决办法： 设置系统的环境变量

CATALINA_BASE  =F:\Environment\apache-tomcat-9.0.38

CATALINA_HOME = F:\Environment\apache-tomcat-9.0.38

PATH添加

%CATALINA_HOME%\lib

%CATALINA_HOME%\bin



注意： 

第一: 我们的db.properties需要放到resources，因为我们执行编译后，maven会把这个文件直接放入到类路径下 /WEB-INF/classes下面；

第二：我们如果把db.properties里面，如果没有在子项目servlet-02的web.xml里面放入build参数，会导致无法将文件构建到项目中

```xml
    <build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
    </build>
```

```properties
jdbcDriver=com.mysql.jdbcDriver
url=jdbc:mysql://localhost:3306/mysql
user=root
passpord=123456
```

```java
public class ServletDemo4 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext servletContext = this.getServletContext();
        InputStream resourceAsStream = servletContext.getResourceAsStream("/WEB-INF/classes/db.properties");
        Properties prop = new Properties();
        prop.load(resourceAsStream);

        resp.getWriter().println("jdbcDriver---->"+prop.getProperty("jdbcDriver"));
        resp.getWriter().println("url---->"+prop.getProperty("url"));
        resp.getWriter().println("user---->"+prop.getProperty("user"));
        resp.getWriter().println("passpord---->"+prop.getProperty("passpord"));

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

### 6.6 HttpServletRequest

#### 1.什么是HttpServletRequest

HttpServletRequest代表客户端的请求，用户通过HTTP协议访问服务器时候，HTTP请求中的所有信息会被封装到HttpServletRequest,通过HttpServletRequest的方法，获得客户端的所有信息。



#### 2、获取前端参数并请求转发

```java
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Arrays;
import java.util.Set;

public class RequestDemoServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("我进来这个方法了!");
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");

        String username = req.getParameter("username");
        String password = req.getParameter("password");
        String[] checkboxes = req.getParameterValues("hobbys");

        System.out.println("=====================");
        System.out.println("username:"+username);
        System.out.println("password:"+password);
        System.out.println("checkboxes"+Arrays.toString(checkboxes));
        System.out.println("=====================");

        System.out.println(req.getContextPath());
        Set<String> realPath = this.getServletContext().getResourcePaths("/");
        for(String s: realPath){
            System.out.println("---:"+s);
        }
        System.out.println("realPath"+realPath);
        //通过请求转发
        //这了的/代表的是当前web的应用
        req.getRequestDispatcher("/success.jsp").forward(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



### 6.7 HttpServletResponse响应

web服务器接收到客户端的http请求，会针对这个请求分别创建一个代表请求的HttpServletRequest对象和一个代表响应的HttpServletResponse对象；我们只需要

	- 如果要获取客户端请求过来的参数， 找HttpServletRequest
	- 如果要给客户端响应一些信息，找HttpServletResponse

#### 1 .对HttpServletResponse的方法

第1类、负责向浏览器发送数据的方法

```java
ServletOutputStream getOutputStream() throws IOException  //写其他字符
PrintWriter getWriter() throws IOException  //写中文
```

第2类、负责向浏览器发送一些响应头的方法

```java
void setCharacterEncoding(String charset)
void setContentLength(int len)
void setContentLengthLong(long len)
void setContentType(String type)
void setBufferSize(int size)
void setHeader(String name, String value)
void setIntHeader(String name, int value)
void setStatus(int sc)
void setStatus(int sc, String sm)
void setDateHeader(String name, long date)
```

> 3. 常见应用

1、向浏览器输出消息getOutputStream()  getWriter()，前面一直在讲

#### 2、下载文件应用，一般步骤如下

	- 1.要获取下载文件的路径
	- 2.下载的文件名是什么
	- 3.设置想办法让浏览器能够下载我们需要的东西
	- 4.获取下载文件的输入流
	- 5.创建缓冲区
	- 6.获取OutPutStream对象
	- 7.将FileOutputStream流写入到buffer缓冲区
	- 8.使用OutputStream将缓冲区中的数据输出到客户端

```java
public class FileServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 1.要获取下载文件的路径
        String realPath = this.getServletContext().getRealPath("/WEB-INF/classes/1.png");
        Set<String> resourcePaths = this.getServletContext().getResourcePaths("/WEB-INF/classes/");
        Iterator<String> iterator = resourcePaths.iterator();
        while (iterator.hasNext()){
            String str = iterator.next();
            System.out.println("getResourcePaths(\"/WEB-INF/classes/\""+str);

        }
        System.out.println("下载的文件路径-->" + realPath);

        // 2.下载的文件名是什么
        String fileName = realPath.substring(realPath.lastIndexOf("\\") + 1);
        // 3.设置想办法让浏览器能够下载我们需要的东西
        resp.setHeader("Content-Disposition", "attachment;filename=" + URLEncoder.encode(fileName,"utf-8"));
        // 4.获取下载文件的输入流
        FileInputStream in = new FileInputStream(realPath);

        // 5.创建缓冲区
        int len = 0;
        byte[] buffer = new byte[1024];

        // 6.获取OutPutStream对象
        ServletOutputStream outputStream = resp.getOutputStream();
        // 7.将FileOutputStream流写入到buffer缓冲区,使用OutputStream将缓冲区中的数据输出到客户端
        while ((len = in.read(buffer)) > 0) {
            outputStream.write(buffer, 0, len);
        }

        // 8.关闭操作
        in.close();
        outputStream.close();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
```

> 几个知识点：
>
> ​	1、通过 this.getServletContext().getResourcePaths("/WEB-INF/classes/")，能够把classes下面的文件路径都给获取到
>
> ​	2、获取路径下的文件名可以使用	realPath.substring(realPath.lastIndexOf("\\") + 1);
>
> ​	3、实现下载需要在服务器设置响应头信息  resp.setHeader("Content-Disposition", "attachment;filename=" + URLEncoder.encode(fileName,"utf-8"));
>
> ​	URLEncoder.encode(fileName,"utf-8")); 这个的作用是保证中文的名字也可以支持处理
>
> ​	4、从文件读取文件并发送出去的方式
>
> ​	先读文件流
>
> ​	FileInputStream in = new FileInputStream(realPath);
>
> ​	建立缓冲区
>
> ​	int len =0
>
> ​	byte [] byte =new byte[1024];
>
> ​	建立输出流
>
> ​	ServletOutputStream st = resp.getOutputStream() 
>
> ​	开始输出
>
> ​	while((len=in.read(byte)>0){
>
> ​			st.write(byte,0,len);
>
> ​		}
>
> ​	最后关闭流
>
> ​	st.close()
>
> ​	in.close()

#### 3、通过HttpServletResponse实现验证功能

验证码怎么来的

```java
public class ImageCodeServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setHeader("refresh", "3");//设置浏览器3秒刷新一次
        //在内存中得到图片,
        BufferedImage image = new BufferedImage(100, 50, BufferedImage.TYPE_INT_RGB); //获得画板

        Graphics2D g = (Graphics2D) image.getGraphics(); //获得画板的笔
        //把图片的背景色画成白色
        g.setColor(Color.white);
        g.fillRect(-20, 0, 100, 20);
        //给图片协商数据
        g.setColor(Color.red);
        g.setFont(new Font(null, Font.BOLD, 20));
        g.drawString(makeNum(), 0, 20);
        //设置浏览器支持图片无缓存
        resp.setContentType("image/jpeg");
        //网站存在缓存，不让浏览器缓存
        resp.setDateHeader("expires", -1);
        resp.setHeader("Cache-Control", "no-cache");
        resp.setHeader("pragma", "no-cache");

        //发送图片给浏览器
        boolean send = ImageIO.write(image, "jpg", resp.getOutputStream());
        if (send)
            System.out.println("发送成功了!");

    }
	//生成7位数字
    private String makeNum() {
        Random random = new Random();
        String num = random.nextInt(999999) + "";
        StringBuffer sb = new StringBuffer();
        for (int i = 0; i < 7 - num.length(); i++) {
            sb.append("0");
        }
        num = sb.toString() + num;
        return num;
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```





#### 4、实现重定向



![image-20201124131114748](img/image-20201124131114748.png)



```java
public class RequestTest extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("进入这个请求了!");
        //处理请求
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        System.out.println("username:"+username+"   password:"+password);
        //重定向的时候一定要注意，路径问题，否则就会404
        resp.sendRedirect("/s/success.jsp");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```

```jsp
<html>
    <body>
        <%--这里提交的路径需要寻找到项目的路径，项目的路径怎么找，用${}--%>
        <%--${pageContext.request.contextPath}  这个代表当前的项目地址--%>
        <form action="${pageContext.request.contextPath}/login" method="get">
            用户名:<input type="text" name="username"><br>
            密码:<input type="password" name="password"><br>
            <input type="submit">
        </form>
	</body>
</html>

```





重定向和转发的区别：面试题

相同点

​	-页面都可以实现跳转

不同点

	- 请求转发的时候。url不会产生转发
	- 重定向时候，url地址栏会发生变化

#### 5.[获取资源路径](https://www.cnblogs.com/ncy1/articles/8811238.html)

```
1、xxx.class.getClassLoader().getResource(“”).getPath(); 
获取src资源文件编译后的路径（即classes路径） 


2、xxx.class.getClassLoader().getResource(“文件”).getPath(); 
获取classes路径下“文件”的路径 


3、xxx.class.getResource(“”).getPath()； 
缺少类加载器，获取xxx类经编译后的xxx.class路径 


4、this.getClass().getClassLoader().getResource(“”).getPath()； 
以上三种方法的另外一种写法 


5、request().getSession().getServletContext().getRealPath(“”)； 
获取web项目的路径 
```

![image-20201223221014038](img/image-20201223221014038.png)

#### 6 web读取路径的问题

项目结构

![image-20201223224624625](img/image-20201223224624625.png)



```java
public class FileServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("=======================");

        String path0 = this.getClass().getClassLoader().getResource("").getPath();
        String path01 = this.getClass().getClassLoader().getResource("1.png").getPath(); //Null
        String path011 = this.getClass().getClassLoader().getResource("/1.png").getPath(); //Null
        //String path0111 = this.getClass().getClassLoader().getResource("/WEB-INF/classes/11.png").getPath(); //Null

        String path2 = this.getClass().getResource("").getPath();
        String path21 = this.getClass().getResource("/1.png").getPath();

        //其实通过ServletContext().getRealPath来拼接路径只是绝对硬盘路径的升级版
        String path3 = this.getServletContext().getRealPath("");
        String path4 = this.getServletContext().getRealPath("resources/r1.png");


        System.out.println("获取src资源文件编译后的路径（即classes路径） "+path0);
        System.out.println("path01="+path01);
        System.out.println("path011="+path011);
        //System.out.println("path0111="+path0111);
        System.out.println("缺少类加载器，获取xxx类经编译后的xxx.class路径 "+path2);
        System.out.println("path21 "+path21);
        System.out.println("获取web项目的路径  "+path3);
        System.out.println("获取1.png的路径 "+path4);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

=======================
获取src资源文件编译后的路径（即classes路径） /F:/Environment/apache-tomcat-9.0.38/webapps/s/WEB-INF/classes/
path01=/F:/Environment/apache-tomcat-9.0.38/webapps/s/WEB-INF/classes/1.png
path011=/F:/Environment/apache-tomcat-9.0.38/webapps/s/WEB-INF/classes/1.png
缺少类加载器，获取xxx类经编译后的xxx.class路径 /F:/Environment/apache-tomcat-9.0.38/webapps/s/WEB-INF/classes/com/kuang/servlet/
path21 /F:/Environment/apache-tomcat-9.0.38/webapps/s/WEB-INF/classes/1.png
获取web项目的路径  F:\Environment\apache-tomcat-9.0.38\webapps\s\
获取1.png的路径 F:\Environment\apache-tomcat-9.0.38\webapps\s\resoutces\r1.png
```

### 总结

#### helloServlet流程

1. 将web.xml的配置更新为最新的版本，我们可以到tomcat/webapps/ROOT里面找到对应的配置
2. 添加java和resources文件夹
3. 将maven的结构搭建完整
4. 编写一个Servlet程序
5. **编写servlet的映射Mapping**（重要）
6. 配置tomcat
7. 启动项目



不需要前端，这个只是测试resp输出



#### Requset & Response

```java
//继承HttpServlet，重写方法doGet和doPost等
public class HelloServlet extends HttpServlet

//获得输入流
ServletInputStream inputStream = req.getInputStream();
//获取数据
String username = req.getParameter("username");

//获得输出流
PrintWriter writer = resp.getWriter();
writer.print(100);
```



```java
ServletOutputStream getOutputStream() throws IOException  //写其他字符
PrintWriter getWriter() throws IOException  //写中文
```



Servlet使用resp.getWriter()来给前端传数据。

https://blog.csdn.net/qq_37745470/article/details/99598276

```java
PrintWriter pw = resp.getWriter();
pw.print(100);
pw.flush();
pw.close();
```

PrintWriter 是有两个方法对页面进行传值的,首先说一下两个方法的区别：

+ write()紧支持输出字符类型，字符，字符数组字符串等
+ print()可以使各种类型，包括object，通过默认编码格式转换成bytes字节形式，这些字节都是通过write（int c）方法让然后被输出 print可以写入对象，write不可以。



PrintWriter对象的flush()和close()方法说明：

flush()将缓冲区的数据强制输出，用于清空缓冲区，若直接调用close()方法，则可能会丢失缓冲区的数据。所以通俗来讲它起到的是刷新的作用。

close()用于关闭数据流



#### ServletContext 应用（重点）

+ set写数据

```java
ServletContext servletContext = this.getServletContext(); //获取当前Servlet的上下文对象
String userName ="秦僵"; //定义一个准备写入到ServletContext中的变量
servletContext.setAttribute("userName", userName); //添加到ServletContext
```

+ get读数据

```java
ServletContext servletContext = this.getServletContext();
String userName = (String)servletContext.getAttribute("userName");
```

+ 获取初始化参数getInitParameter

```java
String url = this.getServletContext().getInitParameter("url");
String jdbcDriver = this.getServletContext().getInitParameter("jdbcDriver");
String user = this.getServletContext().getInitParameter("user");
String passpord = this.getServletContext().getInitParameter("passpord");
```

+ 请求转发getRequestDispatcher

```java
ServletContext servletContext = this.getServletContext();
RequestDispatcher requestDispatcher = servletContext.getRequestDispatcher("/sd2");
requestDispatcher.forward(req,resp);
```

注意，请求转发和重定向是不同的

请求转发是在服务器进行处理，直接转发到另一个请求，在前台看到的url不变，

重定向，是返回新的url给浏览器，浏览器再次去请求新的url地址



+ 读取资源文件   项目大量用到Properties文件

```java
ServletContext servletContext = this.getServletContext();
InputStream resourceAsStream = servletContext.getResourceAsStream("/WEB-INF/classes/db.properties");
Properties prop = new Properties();
prop.load(resourceAsStream);
```



#### HttpServletRequest 请求转发

```java
//通过请求转发
//这了的/代表的是当前web的应用
req.getRequestDispatcher("/success.jsp").forward(req,resp);
```



#### HttpServletResponse 重定向

```java
/重定向的时候一定要注意，路径问题，否则就会404
        resp.sendRedirect("/s/success.jsp");
```





#### 下载文件流程

- 1.要获取下载文件的路径
- 2.下载的文件名是什么
- 3.设置想办法让浏览器能够下载我们需要的东西
- 4.获取下载文件的输入流
- 5.创建缓冲区
- 6.获取OutPutStream对象
- 7.将FileOutputStream流写入到buffer缓冲区
- 8.使用OutputStream将缓冲区中的数据输出到客户端

```java
// 1.要获取下载文件的路径
String realPath = this.getServletContext().getRealPath("/WEB-INF/classes/1.png");
Set<String> resourcePaths = this.getServletContext().getResourcePaths("/WEB-INF/classes/");
Iterator<String> iterator = resourcePaths.iterator();
while (iterator.hasNext()){
    String str = iterator.next();
    System.out.println("getResourcePaths(\"/WEB-INF/classes/\""+str);

}
System.out.println("下载的文件路径-->" + realPath);

// 2.下载的文件名是什么
String fileName = realPath.substring(realPath.lastIndexOf("\\") + 1);
// 3.设置想办法让浏览器能够下载我们需要的东西
resp.setHeader("Content-Disposition", "attachment;filename=" + URLEncoder.encode(fileName,"utf-8"));
// 4.获取下载文件的输入流
FileInputStream in = new FileInputStream(realPath);

// 5.创建缓冲区
int len = 0;
byte[] buffer = new byte[1024];

// 6.获取OutPutStream对象
ServletOutputStream outputStream = resp.getOutputStream();
// 7.将FileOutputStream流写入到buffer缓冲区,使用OutputStream将缓冲区中的数据输出到客户端
while ((len = in.read(buffer)) > 0) {
    outputStream.write(buffer, 0, len);
}

// 8.关闭操作
in.close();
outputStream.close();
```



### ——servlet底部——



## Session & Cookie

### 7.1 什么是session和cookie

回话：用户打开一个浏览器，然后点击了很多超链接，访问了多个web资源，关闭浏览器，这个过程就叫做一个绘画

有状态回话：

你能怎么证明你是西开的学生？

1、发票	西开

西开给你发票，

2、学校登记	西开标记你来过来



一个网站如何证明你来过？

客户端		服务端

​	1、服务器给客户端一个信件，客户端下载访问服务端带上信件就可以了； cookie

​	2、服务器登记你来过了，下次你来得时候我来匹配你（核对你的票） session

### 7.2 保存会话的两种技术

cookie

​	- 客户端技术，通过响应和请求

session

	- 服务器技术，利用这个技术，可以保存用户的会话信息？我们可以吧信息或者数据保存在session

常见的用力：  网站登录后，你下次就不用继续登录了



### 7.3 示例代码

```java
/*服务器，告诉你，你来得时间，把这个时间封装成为一个信件，你下次带来，我就知道你来了*/
public class CookieDemo01Servlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决中文的乱码问题
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html;charset=utf-8"); //不加这个，在浏览器访问时候会显示为乱码

        PrintWriter out = resp.getWriter();
        //
        Cookie[] cookies = req.getCookies();
        if (cookies!=null){
            //如果存在怎么办？我们取出来数据
            out.write("你上一次访问的时间是：");
            for (int i = 0; i < cookies.length; i++) {
                Cookie cookie = cookies[i];
                if (cookie.getName().equals("lastLoginTime")){
                    //获取cookie的值
                    String value = cookie.getValue(); //拿出来的是字符串，要转换成长整型才能变成时间
                    System.out.println(value);
                    long lastLoginTime = Long.parseLong(value); //使用Long包装类转换成长整型
                    Date date = new Date(lastLoginTime); //使用Date转化为时间 变为date对象
                    out.write(date.toLocaleString());
                }
            }
        }else {
            out.write("你是第一次访问!");
        }

        //服务器给客户端响应一个cookie
        Cookie cookie = new Cookie("lastLoginTime", System.currentTimeMillis()+"");
        cookie.setMaxAge(24*60*60);
        resp.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

1、从请求中获取cookie信息

2、服务器响应诶客户端cookie

```java
Cookie[] cookies = req.getCookies();  //获取cookie
cookie.getName()  //获取cookie中的key
cookie.getValue()  //获取cookie中的value
Cookie cookie = new Cookie("lastLoginTime", System.currentTimeMillis()+""); //新建一个cookie
cookie.setMaxAge(24*60*60); //设置cookie的有效期
resp.addCookie(cookie);  //响应给客户端添加一个cookie
```



一个网站cookie是否存在上限!聊聊细节问题

- 一个cookie只能保存一个信息
- 一个web站点可以给浏览器发送多个，最多存20个
- cookie大小限制为4kb
- 300个cookie浏览器上线

删除cookie

- 不设置有效期，关闭浏览器，自动失效，设置有效期为0，就可以实现这个目标

```java
/*通过另一个请求删除掉cookie*/
public class CookieDemo02Servlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //创建一个cookie，名字必须和要删除的cookie一样
        Cookie cookie = new Cookie("lastLoginTime", System.currentTimeMillis()+"");
        //将cookie有效期设置为0，立马过期
        cookie.setMaxAge(0);
        resp.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

案例：遇到中文乱码问题如何解决

>```
>URLDecoder.decode(cookie.getValue(),"utf-8") 解码
>```
>
>```
>URLEncoder.encode("秦僵","utf-8")  编码
>```

```java
/*服务器，告诉你，你来得时间，把这个时间封装成为一个信件，你下次带来，我就知道你来了*/
public class CookieDemo03Servlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决中文的乱码问题
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html;charset=utf-8"); //不加这个，在浏览器访问时候会显示为乱码

        PrintWriter out = resp.getWriter();
        //
        Cookie[] cookies = req.getCookies();
        if (cookies!=null){
            //如果存在怎么办？我们取出来数据
            out.write("你上一次访问的时间是：");
            for (int i = 0; i < cookies.length; i++) {
                Cookie cookie = cookies[i];
                if (cookie.getName().equals("name")){
                    //获取cookie的值  ,因为读取是乱码，所以先进行解码
                    String value = URLDecoder.decode(cookie.getValue(),"utf-8"); //拿出来的是字符串，要转换成长整型才能变成时间
                    System.out.println(value);
                    out.write(value);
                }
            }
        }else {
            out.write("你是第一次访问!");
        }

        //服务器给客户端响应一个cookie
        Cookie cookie = new Cookie("name", URLEncoder.encode("秦僵","utf-8"));
        cookie.setMaxAge(24*60*60);
        resp.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

### 7.4 session(重点)

什么是session

	- 服务器会给没一个用户（浏览器）创建一个Session对象
	- 一个Session独占一个浏览器，只要浏览器没有关闭，这个Session就存在
	- 用户登录之后，整个网站都可以访问他-->保存购物车的信息

![image-20201125123038714](img/image-20201125123038714.png)

HttpSession的相关重点方法

![image-20201125115044125](img/image-20201125115044125.png)

Session和cookie的区别：

	- cookie是把用户数据写给用户的浏览器，浏览器保存(可以保存多个)
	- session是把用户的数据写到用户独占的session中，在服务器端保存(保存重要的信息，减少服务器资源浪费)；
	- session对象由服务器创建，

session使用场景：

​	保存用户的登录信息，只要用户不关闭浏览器，信息都存在

​	购物车信息也可以保存在session

​	经常在整个项目中被使用的数据，我们将它保存在Session中

使用session的示例代码：

```java
public class SessionDemoServlet1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html; charset=utf-8");
        //得到session
        HttpSession session = req.getSession();
        //给Session中存东西
        session.setAttribute("name", new Person("秦僵",18));
        //获取session的id
        String sessionId = session.getId();
        //判断是否是新创建的Session
        if (session.isNew()) {
            resp.getWriter().write("Session创建成功了! Session的ID：" + sessionId);
        } else {
            resp.getWriter().write("Session 已经在服务器中存在了!sessionId: " + sessionId);
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

```java
public class SessionDemoServlet2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html; charset=utf-8");
        //得到session
        HttpSession session = req.getSession();
        //给Session中存东西
        Person person = (Person)session.getAttribute("name");
        //获取session的id
        String sessionId = session.getId();
        //判断是否是新创建的Session
        if (session.isNew()) {
            resp.getWriter().write("Session创建成功了! Session的ID：" + sessionId+"\n");
        } else {
            resp.getWriter().write("Session 已经在服务器中存在了!sessionId: " + sessionId);
            resp.getWriter().write("session.getAttribute(\"name\"):"+person.toString());
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

```java
public class SessionDemoServlet3 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html; charset=utf-8");
        //得到session
        HttpSession session = req.getSession();
        //移除name这个属性
        session.removeAttribute("name");
        //手动注销session，一旦注销sessionid就么有了，浏览器再访问就是生成新的sessionid
        session.invalidate();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



会话自动过期，Web.xml配置

```xml
<!--    设置Session默认失效时间-->
    <session-config>
        <!--15分钟后，session自动失效，以分钟为单位  24*60=1440=一天-->
        <session-timeout>15</session-timeout>
    </session-config>
```



## jsp

### 8.1 什么是JSP

java server pages  JAVA服务器端页面，也和servlet一样，用来实现动态web站点的

最大的特点

	- 写jsp就像在写Html
	- html只给用户提供静态的数据，jsp页面中可以嵌入java代码，为用户提供动态数据；

### 8.2 jsp原理

思路:kankan JSP到底如何执行的？

- 代码层面没有任何问题

- 服务器内部工作

  - tomcat中有一个work目录

  - 我们用IDEA中使用TOMCAT会在IDEA的TOMCAT中生成一个work目录，发现页面装备成了JAVA程序

  - ![image-20201125124204236](img/image-20201125124204236.png)

    ​	![image-20201125124305277](img/image-20201125124305277.png)

- 浏览器向服务器发送请求，不管访问什么资源，其实都是在访问Servlet

- JSP最终也会转译成一个JAVA类，从源码上，她也是继承HttpServlet，也就是一个Servlet

在JSP的生成java文件C:\Users\admin\AppData\Local\JetBrains\IntelliJIdea2020.2\tomcat\Unnamed_javaweb-01-maven\work\Catalina\localhost\kuang\org\apache\jsp\index_jsp.java中，可以看到下面三个方法

```java
//初始化  
public void _jspInit() {
  }
//销毁
  public void _jspDestroy() {
  }
//jspService
  public void _jspService(final javax.servlet.http.HttpServletRequest request, final javax.servlet.http.HttpServletResponse response)
      throws java.io.IOException, javax.servlet.ServletException {
```

1、判断请求

```java
    if (!javax.servlet.DispatcherType.ERROR.equals(request.getDispatcherType())) {
      final java.lang.String _jspx_method = request.getMethod();
      if ("OPTIONS".equals(_jspx_method)) {
        response.setHeader("Allow","GET, HEAD, POST, OPTIONS");
        return;
      }
      if (!"GET".equals(_jspx_method) && !"POST".equals(_jspx_method) && !"HEAD".equals(_jspx_method)) {
        response.setHeader("Allow","GET, HEAD, POST, OPTIONS");
        response.sendError(HttpServletResponse.SC_METHOD_NOT_ALLOWED, "JSP 只允许 GET、POST 或 HEAD。Jasper 还允许 OPTIONS");
        return;
      }
    }
```

2\定义内置的对象

```java
    final javax.servlet.jsp.PageContext pageContext; //页面上下文
    javax.servlet.http.HttpSession session = null;  //session
    final javax.servlet.ServletContext application;  //ServletContext 改名为applicationContext
    final javax.servlet.ServletConfig config; //ServletConfig 改为了config
    javax.servlet.jsp.JspWriter out = null;   //out的输出对象
    final java.lang.Object page = this;		//page代表了当前页
    javax.servlet.jsp.JspWriter _jspx_out = null; 
    javax.servlet.jsp.PageContext _jspx_page_context = null;
final javax.servlet.http.HttpServletRequest request, // 请求
final javax.servlet.http.HttpServletResponse response  //响应
```

3、输出页面之前，增加代码进行页面处理

```java
      response.setContentType("text/html");  //设置响应的页面类型为text/html
      pageContext = _jspxFactory.getPageContext(this, request, response,null, true, 8192, true);
      _jspx_page_context = pageContext; 
      application = pageContext.getServletContext();
      config = pageContext.getServletConfig();
      session = pageContext.getSession();
      out = pageContext.getOut();
      _jspx_out = out;

      out.write("<html>\n");
      out.write("<body>\n");
      out.write("<h2>Hello World!</h2>\n");
      out.write("</body>\n");
      out.write("</html>\n");
```

以上的这些对象，我们可以在jsp页面中直接使用!

在JSP中，可以直接使用 < % 编写java代码%>

![image-20201125131539624](img/image-20201125131539624.png)



在JSP页面中，只要是JAVA代码就会原封不动的输出出来

如果是HTML代码，就会被转换为：



> out.write("<html>\r\n");

这样的格式输出到前端!



### 8.3 jsp基础语法

任何语言都有自己的语法,JAVA中有，JSP作为JAVA技术的一种应用，也有自己扩充的语法

我们创建一个普通的MAVEN项目，通过支持WEB，修改为WEB项目的过程

step1.在IDEA中，选择NewProject,不用勾选模板创建，

step2.待Maven项目加载完成后，光标定位到项目，右键选择[Add Framework Support] ，添加架构支持，选择WEB，即可!



接下来的语法学习，先搭建项目依赖，依赖包配置

```xml
pom.xml
    <dependencies>
        <!--        Servlet依赖-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
        </dependency>
        <!--        JSP依赖-->
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>javax.servlet.jsp-api</artifactId>
            <version>2.3.3</version>
        </dependency>
        <!-- JSTL表达式依赖 -->
        <dependency>
            <groupId>javax.servlet.jsp.jstl</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
        <!-- Standard标签库依赖 -->
        <dependency>
            <groupId>taglibs</groupId>
            <artifactId>standard</artifactId>
            <version>1.1.2</version>
        </dependency>

    </dependencies>
```

**1.JSP表达式**

表达式：<%= new java.util.Date() %> 用来将程序的输出，输出到客户端



**2.JSP脚本片段**

表达式:

<% 

​	int sum=0;

​	for(int i=1;i<100;i++){

​		sum+=i;	

}

​	out.println("<h1>Sum="+sum+>"</h1>");

%>

**3.脚本片段再实现**

```jsp
<%--jsp脚本片段--%>
<%
    int sum = 0;
    for (int i = 0; i < 100; i++) {
        sum += i;
    }
    out.print("<h1>Sum=" + sum + "</h1>");
%>
<h1>下面输出日期</h1>

<%=new java.util.Date()%>

<h1>下面还可以把java脚本片段进行分离</h1>
<%
    for (int i = 0; i < 5; i++) {
%>
<h1>Hello World!<%= i%>
</h1>
<%}%>
```

对应jsp生成的servlet

```java
      out.write("\n");
      out.write("\n");
      out.write("<html>\n");
      out.write("<head>\n");
      out.write("    <title>$Title$</title>\n");
      out.write("</head>\n");
      out.write("<body>\n");
      out.write('\n');

    int sum = 0;
    for (int i = 0; i < 100; i++) {
        sum += i;
    }
    out.print("<h1>Sum=" + sum + "</h1>");

      out.write("\n");
      out.write("<h1>下面输出日期</h1>\n");
      out.print(new java.util.Date());
      out.write("\n");
      out.write("<h1>下面还可以把java脚本片段进行分离</h1>\n");

    for (int i = 0; i < 5; i++) {

      out.write("\n");
      out.write("  <h1>Hello World!");
      out.print( i);
      out.write("</h1>\n");
}
      out.write("\n");
      out.write("</body>\n");
      out.write("</html>\n");
    }
```

4.JSP声明<%! %>

```java
<%!
  static {
    System.out.println("Loading servlet!");
  }
  static int globalVar =0;

  public void kuang(){
    System.out.println("进入了方法kuang()狂神秦僵!");
  }
%>
```

编译后生成的jsp.java

![image-20201126095029604](img/image-20201126095029604.png)



JSP声明 <%!%>： 会被编译到jsp生成的java类的类中

jsp脚本片段<%%>和jsp表达式<%=%>， 会被编译生成到jsp的 _jspService()中

上述的写法，使用起来不方便，所以衍生出来使用EL表达式 比如  <%=%> 用el表达式就是 ${}

```jsp
<%%>
<%=%>
<%! %>
<%--注释--%>
```

jsp的注释，不会在客户端显示，html就会

### 8.4 jsp指令

1、@page  errorPage="error/500.jsp"	这个设置500页面

2、@page import java.util.* 这个在当前页面引用库

关于设置错误页面的两种方法：

​	准备，在web目录下创建error文件夹，放入404.jsp和500.jsp， 在web目录下，创建img目录

​	方法1： 在相关页面使用 @page  errorPage="error/500.jsp"这样出现500的错误就会进入到error/500.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@page errorPage="error/500.jsp" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%
    int i = 1 / 0;
%>
</body>
</html>
```



​	方法2:  在web.xml配置

```
<error-page>
    <error-code>404</error-code>
    <location>/error/404.jsp</location>
</error-page>
<error-page>
    <error-code>500</error-code>
    <location>/error/500.jsp</location>
</error-page>
```

```
<@page encoding="utf-8">
<@include file=""> 包含，一般网站头尾都一样，作为共用的，可以直接提取公共页面，其他页面include

<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%@include file="common/header.jsp" %>
<h1>网页</h1>
<%@include file="common/footer.jsp" %>
<%--    jsp标签--%>
<jsp:include page="common/header.jsp"/>
<h1>网页</h1>
<jsp:include page="common/footer.jsp"/>
</body>
</html>
```

两种区别

![image-20201126113140834](img/image-20201126113140834.png)

方法1，可以直接写写代码，写对象会有错误，方法2 ，不能重复定义变量

### 8.5 9大内置对象

```java
    final javax.servlet.jsp.PageContext pageContext; //页面上下文
    javax.servlet.http.HttpSession session = null;  //session
    final javax.servlet.ServletContext application;  //ServletContext 改名为applicationContext
    final javax.servlet.ServletConfig config; //ServletConfig 改为了config
    javax.servlet.jsp.JspWriter out = null;   //out的输出对象
    final java.lang.Object page = this;		//page代表了当前页
    javax.servlet.jsp.JspWriter _jspx_out = null; 
    javax.servlet.jsp.PageContext _jspx_page_context = null;
final javax.servlet.http.HttpServletRequest request, // 请求
final javax.servlet.http.HttpServletResponse response  //响应
```



- PageContext (PageContext) 存东西
- Request  存东西
- Response
- Session  这个存东西
- Application(ServletContext)  存储东西
- config(ServletConfig) 
- out
- page
- exception

不同对象存储东西，作用域的不同

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%--内置对象--%>
<%
    pageContext.setAttribute("name1", "秦僵1号"); //保存的数据只在一个页面中有效
    request.setAttribute("name2", "秦僵2号"); //保存的数据只在一次请求中有效，请求转发会携带这个数据
    session.setAttribute("name3", "秦僵3号"); //保存在一次会话中有效，从打开浏览器，到关闭浏览器
    //统计在线人数
    application.setAttribute("name4", "秦僵4号"); //凌驾所有数据之上，保存的数据，在服务器存续期间都会有效，从打开服务器到关闭服务器
%>
<%--脚本片段的代码，会被原封不动的生成到到jsp.java中
要求：脚本片段的代码，必须保证java语法的正确性--%>
<%--<%--%>
<%--//通过pageContext取出我们保存的值--%>
<%--    Object name1 = pageContext.getAttribute("name1");--%>
<%--    Object name2 = request.getAttribute("name2");--%>
<%--%>--%>
<%
    //通过pageContext寻找的方法
    //从底层到高层(作用域)
    String name1 = (String)pageContext.findAttribute("name1");
    String name2 = (String)pageContext.findAttribute("name2");
    String name3 = (String)pageContext.findAttribute("name3");
    String name4 = (String)pageContext.findAttribute("name4");
    String name5 = (String)pageContext.findAttribute("name5");
%>
<%--使用EL表达式输出${} 等价于<%=%>--%>
    <h1>取出的值为:</h1>
    <h3>${name1}</h3>
    <h3>${name2}</h3>
    <h3>${name3}</h3>
    <h3>${name4}</h3>
    <h3>${name5}</h3>
</body>
</html>
```



```
    public void setAttribute(String name, Object attribute, int scope) {
        switch(scope) {
        case 1:
            this.mPage.put(name, attribute);
            break;
        case 2:
            this.mRequest.put(name, attribute);
            break;
        case 3:
            this.mSession.put(name, attribute);
            break;
        case 4:
            this.mApp.put(name, attribute);
            break;
        default:
            throw new IllegalArgumentException("Bad scope " + scope);
        }

    }
    
    public abstract class PageContext extends JspContext {
    public static final int PAGE_SCOPE = 1;
    public static final int REQUEST_SCOPE = 2;
    public static final int SESSION_SCOPE = 3;
    public static final int APPLICATION_SCOPE = 4;
```

request:客户端向服务器发送其你去，产生的数据，用户看完就没用了，比如新闻；

session:客户端向服务器发送请求，产生的数据，用户用完了一会还会用，比如购物车

application：客户端向服务器发送请求，产生的数据，一个用户用完了，其他用户还可能使用比如聊天数据

### 8.6 JSP标签、JSTL标签、EL表达式

EL（Expression Language）表达式：${}

	- 获取数据
	- 执行运算
	- 获取web开发的常用对象
	- 调用java方法

JSP标签

```
<%--http://localhost:8080/jsptag.jsp?name=kuangshen&age=12--%>
<jsp:forward page="jsptag2.jsp">
    <jsp:param name="name" value="kuangshen "></jsp:param>
    <jsp:param name="age" value="12"></jsp:param>
</jsp:forward>
    
    <body>
    名字:<%= request.getParameter("name")%>
    年龄:<%= request.getParameter("age")%>
    </body>   
```

JSTL标签



JSTL标签库的使用就是为了弥补HTML标签的不足，它自定义许多标签，可以供我们使用，标签的功能和JAVA代码一样

**核心标签(掌握)**

> 要导入  <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>



示例代码1： c:if 

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>coreif</title>
</head>
<body>
<h4>测试</h4>
<form action="coreif.jsp" method="get">
    <%--El表达式，获取表单数据，使用${param.参数名}--%>
    <input type="text" name="username" value="${param.username}">
    <input type="submit">
</form>
<%--判断如果用户提交用户名是管理员，则登录成功--%>
<c:if test="${param.username.equals('admin')}" var="isAdmin">
    <c:out value="${param.username}"/>
</c:if>


<c:out value="${isAdmin}"/>
</body>
</html>
```

示例代码2： c:choose 

```jsp
<head>
    <title>c:choose标签实例</title>
</head>
<body>
<%--在pageContent里面设置一个salary=4000--%>
<c:set var="salary" scope="page" value="${2000*2}"/>
<p>你的工资是:<c:out value="${salary}" /></p>

<c:choose>
    <c:when test="${salary <= 0}">
        太惨了!
    </c:when>
    <c:when test="${salary >= 1000}">
        不错的薪水,还能生活!
    </c:when>
    <c:otherwise>
        什么都没有!
    </c:otherwise>
</c:choose>
</body>
</html>
```



示例代码3： c:forEach

```jsp
<%@ page import="java.util.ArrayList" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>coreforeach实例代码</title>
</head>
<body>
    <%
        ArrayList<String> people = new ArrayList<String>();
        people.add(0,"张三");
        people.add(1,"李四");
        people.add(2,"王五");
        people.add(3,"赵六");
        people.add(4,"钱七");
        request.setAttribute("list",people);
    %>
<%--
var 每次遍历的变量
items 要遍历的数组
begin 开始位置
end 结束的位置
step 步进 默认为1
--%>
<c:forEach var="people" items="${list}" begin="" end="" step="">
    <c:out value="${people}"/><br>
</c:forEach>
</body>
</html>
```





**格式化标签**

**SQL标签**

**XML标签**

### 8.7 JAVA BEEN

实体类

JAVA BEAN 与特定的写法

	- 必须有一个无参构造
	- 属性必须私有化
	- 必须有对应的get/set方法

一般用来和数据库的字段做映射ORM

ORM 对象关系映射

	- 数据库一张表对应java一个类
	- 表里面的字段-对应类的一个属性
	- 表里面的行记录，对应一个类的一个对象；

People表

| id   | name      | age  | address |
| ---- | --------- | ---- | ------- |
| 1    | 秦僵1号   | 3    | 西按    |
| 2    | 秦僵2号18 | 3    | 西安    |
| 3    | 秦僵3号   | 100  | 西安    |

```
class People{
	private int id;
	private String name;
	private int age;
	private String address;
}

class A{
	new People(1,"秦僵1号",3，"西安");
}
```

```xml
<body>
<jsp:useBean id="people" class="top.aigoo.pojo.People" scope="page"/>
<%--设置属性值--%>
<jsp:setProperty name="people" property="id" value="1"/>
<jsp:setProperty name="people" property="name" value="王丽"/>
<jsp:setProperty name="people" property="age" value="25"/>
<jsp:setProperty name="people" property="address" value="北京市顺义区高丽营镇金马工业区18号"/>

<%--得到属性值并显示出来--%>
主键id:<jsp:getProperty name="people" property="id"/><br>
姓名:<jsp:getProperty name="people" property="name"/><br>
年龄:<jsp:getProperty name="people" property="age"/><br>
地址:<jsp:getProperty name="people" property="address"/><br>


</body>
```



com.kuang.pojo

- 过滤器
- 监听器  GUI
- 文件上传
- 邮件发送
- JDBC复习:如何使用JDBC，JDBC CRUD JDBC事务

### 8.8.三层架构 MVC

什么是MVC  Model View Controller  模型视图控制器

Servlet和jsp都可以写java代码，为了易于维护和使用，servlet专注于处理请求，以及控制视图跳转，jsp专注于显示数据

用户直接访问控制层，控制层就可以直接操作数据库：

>servlet--curd--数据库
>
>弊端：程序十分臃肿，不利于维护，servlet的代码中，处理请求，响应，视图跳转，处理JDBC，处理业务代码，处理逻辑代码
>
>架构：没有什么是加一层解决不了的!
>
>程序员调用!
>
>|
>
>JDBC
>
>|
>
>Mysql oralcle sqlserver.......
>
>2 三层架构![image-20201127223837589](img/image-20201127223837589.png)

Model:

​	-业务处理  业务逻辑Service

	- 数据持久层CRUD DAO

View

	- 展示数据

- 提供链接发起Servlet请求(a,form,.img.....)

Controller(servlet)

	- 接收用户请求(req 请求参数session信息....)
	- 交给业务层处理对应的代码
	- 控制视图的跳转

> 登录--->接收用户的登录请求---->处理用户的请求(获取用户的登录的参数 username password)---->交给业务层处理登录业务(判断用户名密码是否正确)--->Dao层查询数据库用户名密码是否正确--->数据库



## Filter

Filter：过滤器，用来过滤网站的数据；

![image-20201127232944733](img/image-20201127232944733.png)

	- 处理中文乱码
	- 登录、验证



Filter开发步骤

	-	导入包，导入包不要错

> ```
> <artifactId>javax.servlet-api</artifactId>
> <artifactId>javax.servlet.jsp-api</artifactId>
> <artifactId>jstl</artifactId>
> <artifactId>standard</artifactId>
> <artifactId>mysql-connector-java</artifactId>
> ```

	-	开发Filter,编写过滤器

```java
public class JavaFilterDemo1 implements Filter {
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("JavaFilterDemo1 初始化.....");
    }

    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        request.setCharacterEncoding("utf-8");
        response.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");
        System.out.println("+++++++++++过滤器执行前+++++++++++");
        chain.doFilter(request,response);
        System.out.println("<--------过滤器执行后---------->");
    }

    public void destroy() {
        System.out.println("JavaFilterDemo1 销毁.....");
    }
}
```



- 配置过滤器

```xml
    <filter>
        <filter-name>JavaFilterDemo1</filter-name>
        <filter-class>top.aigoo.filter.JavaFilterDemo1</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>JavaFilterDemo1</filter-name>
        <url-pattern>/servlet/*</url-pattern>
    </filter-mapping>
### 上述式子代表所有/servlet/后面的相关页面都会被过滤器捕获到
```



1、过滤中的所有代码，在过滤特定请求的时候都会执行

2、必须要让过滤器继续通行，chain.doFilter(request, response) //过滤器放行



## JDBC复习

Java连接数据库 

需要的jar包

- java.sql
- javax.sql
- mysql-conneter-java....连接驱动(必须要导入)

事务：

```java
开启事务  connection.setAutoCommit(false)

事务提交  commit()

事务回滚  rollback()

关闭事务
```

Junit单元测试

依赖：

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.11</version>
</dependency>
```



简单实用

@Test注解只有在方法上面有效，只有加了这个注解的方法，就可以直接运行!

```java
public class TestInsertDemo3 {
    @Test
    public void testDe() {
        System.out.println("demo");
    }
}
```

示例代码

```java
public class TestInsertDemo3 {
    @Test
    public void test() {
        //1.配置信息
        String url = "jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=UTF-8&useSSL=false";
        String username = "root";
        String password = "123456";
        Connection conn =null;

        try {
            //1.加载驱动
            Class.forName("com.mysql.jdbc.Driver");
            //2.连接数据库，代表数据库
            conn = DriverManager.getConnection(url, username, password);
            String sql = "update account set money=money-100 where name='A'";
            conn.prepareStatement(sql).executeUpdate();
            //3.通知数据库开启事务，false 开启
            conn.setAutoCommit(false);
            //制造错误
            int i = 1/0;
            String sql2 = "update account set money=money+100 where name='B'";
            conn.prepareStatement(sql2).executeUpdate();

            conn.commit();//以上两条SQL都执行成功了，就执行事务!
            System.out.println("插入成功");
        } catch (Exception e) {
            try {
                conn.rollback();//执行失败，事务回滚
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
            e.printStackTrace();
        }finally {
            try {
                conn.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }

    }
}

```









# mybatis

## 简介

### 1.1  什么是Mybatis

​	MyBatis 是一款优秀的持久层框架，它支持自定义 SQL、存储过程以及高级映射。MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。

- MyBatis 是一款优秀的**持久层框架**
- 它支持定制化 SQL、存储过程以及高级映射。
- **MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集**。
- MyBatis 可以使用简单的 XML 或注解来配置和映射原生类型、接口和 Java 的 POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。
- MyBatis 本是[apache](https://baike.baidu.com/item/apache/6265)的一个开源项目[iBatis](https://baike.baidu.com/item/iBatis), 2010年这个项目由apache software foundation 迁移到了google code，并且改名为MyBatis 。
- 2013年11月迁移到Github。  



### 1.2 如何获得mybatis

​	@ github   https://github.com/mybatis/mybatis-3

​	@ 中文文档地址  https://mybatis.org/mybatis-3/zh/index.html

​	@ maven  https://mvnrepository.com/artifact/org.mybatis/mybatis/3.5.2

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.2</version>
</dependency>

```



### 1.3 持久层

**数据持久化**

- 持久化就是将程序的数据在持久状态和瞬时状态转化的过程
- 内存：**断电即失**
- 数据库(Jdbc)、io文件持久化。
- 生活：冷藏、 罐头能够将食品持久化。

**为什么需要需要持久化？**

- 有一些对象，不能让他丢掉。
- 内存太贵了



Dao层，Service层，Controller层….

- 完成持久化工作的代码块
- 层界限十分明显。



### 1.4 为什么需要MyBatis

- 帮助程序猿将数据存入到数据库中。
- 方便
- 传统的JDBC代码太复杂了。简化。框架。自动化。
- 不用Mybatis也可以。更容易上手。 **技术没有高低之分**
- 优点：
  - 简单易学
  - 灵活
  - sql和代码的分离，提高了可维护性。
  - 提供映射标签，支持对象与数据库的orm字段关系映射
  - 提供对象关系映射标签，支持对象关系组建维护
  - 提供xml标签，支持编写动态sql。



## 第一个mybatis程序

思路：搭建环境-->导入mybatis--->编写代码-->测试

第一步，写一个工具类 SqlSessionFactoryBuilder ()----SqlSessionFactory----SqlSession  （引申出需要去配置一个mybatis-config.xml）

> 每个基于 MyBatis 的应用都是以一个 **SqlSessionFactory** 的实例为核心的。**SqlSessionFactory** 的实例可以通过 **SqlSessionFactoryBuilder** 获得。而 **SqlSessionFactoryBuilder** 则可以从 XML 配置文件或一个预先配置的 Configuration 实例来构建出 SqlSessionFactory 实例。

### 2.1 搭建环境

step 1 搭建数据库, 相应的环境脚本

step 2 新建 一个项目，普通maven项目

step 3. 创建一个普通的项目



step 1 搭建数据库, 相应的环境脚本

```sql
create database `mybatis`;
use `mybatis`

create table `user`(
	`id` int(20) not null,
	`name` VARCHAR(30) default null,
	`pwd` varchar(30) default null,
	primary key(`id`)
)ENGINE=INNODB default charset=utf8;

insert into `user`(`id`,`name`,`pwd`) 
VALUES(1,'狂神','123456'),
(2,'张三','123456'),
(3,'李四','123456'),
(4,'王五','123456')
```



step 2 新建 一个项目，普通maven项目

​	1、新建一个maven普通项目

​	2、删除src，变更项目为一个<!--父工程-->

​	3、导入对应的依赖 

```xml
<!--导入依赖-->
    <dependencies>
        <!--mysql驱动-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.20</version>
        </dependency>
        <!--mybatis-->
        <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.2</version>
        </dependency>
        <!--junit-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
    </dependencies>
```



​	step 3. 创建一个普通的项目

​		接下来就是使用了





### 2.2 编写mybatis的核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--configuration核心配置文件-->
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>  <!--事务管理-->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/> <!--驱动-->
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=utf-8"/><!--连接-->
                <property name="username" value="root"/><!--用户名-->
                <property name="password" value="123456"/><!--密码-->
            </dataSource>
        </environment>

    </environments>
    <mappers>
        <mapper resource="org/mybatis/example/BlogMapper.xml"/>
    </mappers>
</configuration>
```



工厂模式，建造模式



### 2.3 编写读取配置文件的工具类

```java
//工具类  sqlSessionFactory
public class MyBatisUtils {
    private  static  SqlSessionFactory sqlSessionFactory ;

    static {
        try {
            //使用mybatis第一步： 获取sqlSessionFactory对象
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }

    }

    //既然有了 SqlSessionFactory，顾名思义，我们可以从中获得 SqlSession 的实例。SqlSession 提供了在数据库执行 SQL 命令所
    // 需的所有方法。你可以通过 SqlSession 实例来直接执行已映射的 SQL 语句

    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
        //sqlSession 和 之前的prepareStatement一样
    }

}

```

### 2.4 编写业务代码

	- 实体类

```java
public class User implements Serializable {
    private int id;
    private String name;
    private String pwd;

    public User() {
    }

    public User(int id, String name, String pwd) {
        this.id = id;
        this.name = name;
        this.pwd = pwd;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPwd() {
        return pwd;
    }

    public void setPwd(String pwd) {
        this.pwd = pwd;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", pwd='" + pwd + '\'' +
                '}';
    }
}
```



	- Dao接口操作

```java
public interface UserDao {
    //获取用户列表
    List<User> getUserList();
}
```



	- 接口实现类

接口实现类由原来的UserDaoImpl转换为一个Mapper配置文件  resultType就要用完全路径

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace==绑定一个对应的Dao/Mapper接口-->
<mapper namespace="com.kuang.dao.UserDao">
    <!--select 查询语句 id对应Dao/Mapper里面的方法名字-->
    <select id="getUserList" resultType="com.kuang.pojo.User">
        select * from mybatis.user
    </select>
</mapper>
```

### 2.5 测试(Junit)

```xml
<mappers>
        <mapper resource="com/kuang/dao/UserMapper.xml"/>
</mappers>
```



注意点1 :ause: org.apache.ibatis.builder.BuilderException: Error parsing SQL Mapper Configuration. Cause: java.io.IOException: Could not find resource org/mybatis/example/BlogMapper.xml

注意点2. 在 mybatis-config.xml里面，mapper注册是用/ ,不是用.

```xml
    <!--每一个Mapper.xml都需要在mybatis核心配置文件注册-->
    <mappers>
        <!--<mapper resource="org/mybatis/example/UserMapper.xml"/>-->
        <mapper resource="com/kuang/dao/UserMapper.xml"/>
    </mappers>
```

注意点3.配置错了localhost，导致产生数据库连接错误

```
### Cause: com.mysql.jdbc.exceptions.jdbc4.CommunicationsException: Communications link failure

```

注意点4. 没有注册mapper会报错

> org.apache.ibatis.binding.BingingException:Type interface com.kuang.dao.UserDao is not known to the MapperRegistry.
>
> MapperRegistry是什么？
>
> 没一个Mapper.xml都需要在Mybatis核心配置文件中注册!

测试代码

```java
public class UserDaoTest {
    @Test
    public void test() {
        //使用工具类,获取sqlSession对象
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        try {
            //方式一(推荐)执行sql
            UserDao userDao = sqlSession.getMapper(UserDao.class);
            List<User> userList = userDao.getUserList();
            //方式二
            List<User> objects = sqlSession.selectList("com.kuang.dao.UserDao.getUserList");

            for (User user : userList) {
                System.out.println("User:" + user.getName());
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //关闭sqlSession
            sqlSession.close();
        }
    }
}
```

可能会遇到的问题：

1、配置文件没有注册

2、绑定接口错误

3、方法名不对

4、返回类型不对

5、Maven导出资源问题

6、Error:java: 不再支持源选项 5。请使用 6 或更高版本。

解决方法：在pom.xml加上jdk配置

  ```java
<properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.encoding>UTF-8</maven.compiler.encoding>
        <java.version>11</java.version>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
</properties>
  ```



## CRUD操作的MyBatis实现

### 1、namespace

 	namespace中的包名要和Dao/Mapper 接口中的包名完全一致! 全限定类名

### **2、select 选择、查询语句**

里面的属性有如下字段

	- id 就是对应的namespace中的方法名，
	- resultType sql语句执行的返回值类型 
	- parameterType 参数的类型，传递的参数类型

Step1 编写接口

```java
    //获取全部用户列表
    List<User> getUserList();
    //根据id查询用户
    User getUserById(int id);
```



Step2 编写对应的mapper中的sql语句

```xml
<!--namespace==绑定一个对应的Dao/Mapper接口-->
<mapper namespace="com.kuang.dao.UserDao">
    <!--select 查询语句 id对应Dao/Mapper里面的方法名字-->
    <select id="getUserList" resultType="com.kuang.pojo.User">
        select * from mybatis.user;
    </select>
    <!--根据id查找指定的一个用户-->
    <select id="getUserById" parameterType="int" resultType="com.kuang.pojo.User">
        select * from mybatis.user where id = #{id};
    </select>
</mapper>
```



Step3 测试

```java
    @Test
    public void test() {
        //使用工具类,获取sqlSession对象
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        try {
            //方式一(推荐)执行sql
            /**
             * 1、一开始mybatis框架会解析映射配置文件UserMapper.xml文件，会将insert等sql标签封装为一个个的MappedStatement对象，
             * 再以全限定类名+方法名作为key，MappedStatement对象为value封装到MappedStatements这一个map集合中。
             * 2、当你调用getMapper方法时，mybatis会为Userdao使用动态代理创建一个代理对象，只有传入Userdao.class，框架才知道对哪一个
             * 接口创建代理对象，并且UserDao.class也包含了此接口的全限定类名，也就是能够作为key查询到MappedStatements集合中的value值
             * ，也就是对应的MappedStatement对象
             */
            UserDao userDao = sqlSession.getMapper(UserDao.class);
            List<User> userList = userDao.getUserList();
            //方式二
            List<User> objects = sqlSession.selectList("com.kuang.dao.UserDao.getUserList");

            for (User user : userList) {
                System.out.println("User:" + user.getName());
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //关闭sqlSession
            sqlSession.close();
        }
    }

    @Test
    public void getUserById() {
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        UserDao mapper = sqlSession.getMapper(UserDao.class);
        User userById = mapper.getUserById(1);
        System.out.println("userById:" + userById);
        sqlSession.close();
    }
```



### **3、insert**

Step1 编写接口

```java
    //insert一个用户
    int addUser(User user);
```



Step2 编写对应的mapper中的sql语句

```xml
    <!--添加一个用户，对象中的属性，可以直接取出来但是要和User属性一一对应否则拿不到-->
    <insert id="addUser" parameterType="com.kuang.pojo.User">
        insert into mybatis.user (id,name,pwd) values (#{id},#{name},#{pwd});
    </insert>
```



Step3 测试

```java
    //增删改需要提交事务
    @Test
    public void addUser() {
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        UserDao mapper = sqlSession.getMapper(UserDao.class);
        User user6 = new User(6, "钱六", "123456");
        int i = mapper.addUser(user6);
        if (i>0){
            System.out.println("添加成功");
        }
        //提交事务,必须提交事务，不然数据库没有
        //sqlSession.commit();
        System.out.println(mapper.getUserById(5));
        sqlSession.close();
    }
```



### **4、update**

Step1 编写接口

```java
    //update修改一个用户
    int updateUser(User user);
```



Step2 编写对应的mapper中的sql语句

```xml
    <!--修改，对象中的属性，可以直接取出来,但是要和User属性一一对应否则拿不到-->
    <update id="updateUser" parameterType="com.kuang.pojo.User">
        update mybatis.user set name =#{name},pwd=#{pwd}  where id=#{id};
    </update>
```



Step3 测试

```java
    @Test
    public void updateUser(){
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        UserDao mapper = sqlSession.getMapper(UserDao.class);
        int 呵呵 = mapper.updateUser(new User(4, "呵呵", "123123"));
        //一定要提交事务，不然没变更
        sqlSession.commit();
        if (呵呵>0){
            System.out.println("修改成功");
        }
        sqlSession.close();
    }
```



### **5、delete**

Step1 编写接口

```
    //删除一个用户
    int deleteUser(int id);
```



Step2 编写对应的mapper中的sql语句

```xml
    <!--删除，对象中的属性，可以直接取出来,但是要和User属性一一对应否则拿不到-->
    <delete id="deleteUser" parameterType="int">
        delete from mybatis.user where id=#{id};
    </delete>
```



Step3 测试

```java
    @Test
    public void deleteUser(){
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        UserDao mapper = sqlSession.getMapper(UserDao.class);
        int 呵呵 = mapper.deleteUser(4);
        //一定要提交事务，不然没变更
        sqlSession.commit();
        if (呵呵>0){
            System.out.println("删除成功");
        }
        sqlSession.close();
    }
```







注意点&分析错误

增删改查需要提交事务!

标签不要配置错误

resource绑定mapper，需要使用路径，而不是.访问符

数据库连接，需要标记正确

**程序读错误日志，要从后往前读，这样比较容易排查错误**

### 6. 万能的mapper

假设我们的实体类或者数据库中字段或者参数过多，我们应当考虑使用Map！,这样我们就可以有如下两个好处

1、不用User的字段和select  sql字段一一对应，map传递参数，直接在sql中取出key即可

2、我们可以传递任意多个参数，而不用每次都必须传递一个User

实现方式

step1. 编写UserDao对应接口

```java
//insert一个用户
int addUser(User user);
//使用神奇的Map传递参数
int addUser2(Map<String,Object> map);

int addUser3(@Param("username")String username,@Param("passwordNew")String passwordNew)
//注意： 这里我们定义的是一个Map对象
```

step2.编写UserDaoMapper.xml, 在这里我们传递的parameterType是写的小写map

```xml
<!--添加一个用户，对象中的属性，可以直接取出来但是要和User属性一一对应否则拿不到-->
<insert id="addUser" parameterType="com.kuang.pojo.User">
    insert into mybatis.user (id,name,pwd) values (#{id},#{name},#{pwd});
</insert>
<!--对象中的属性，可以直接取出来,可以用map的key传递参数，可以随意进行定义命名，不需要一一对应-->
<insert id="addUser2" parameterType="map">
    insert into mybatis.user (id,name,pwd) value (#{userId},#{UserName},#{password})
</insert>
<insert id="addUser2" parameterType="map">
    insert into mybatis.user (name,pwd) value (#{username},#{password})
</insert>
```

step3.  编写测试累验证一下

```java
@Test
public void addUser2(){
    //1.获取我们的sqlSession
    SqlSession sqlSession = MyBatisUtils.getSqlSession();
    //2.拼接一个HashMap，把对应的key值和UserMapper.xml对应起来
    Map<String, Object> stringObjectHashMap = new HashMap<String, Object>();
    stringObjectHashMap.put("userId",7);
    stringObjectHashMap.put("UserName","helloworld");
    stringObjectHashMap.put("password","123123");
    //3.调用我们的mapper方法
    UserDao mapper = sqlSession.getMapper(UserDao.class);
    mapper.addUser2(stringObjectHashMap);
    //4.事务要提交
    sqlSession.commit();
	//5.关闭sqlSession
    sqlSession.close();
}
```



1.Map传递参数，直接在sql的 #{} 中使用key即可 例如  insert into mybatis.user (id,name,pwd) value (#{userId},#{UserName},#{password})

```xml
<insert id="addUser2" parameterType="map">
insert into mybatis.user (id,name,pwd) value (#{userId},#{UserName},#{password})
</insert>
```

2.对象传递参数，直接在sql的#{}中使用对象的属性即可 insert into mybatis.user (id,name,pwd) values (#{id},#{name},#{pwd});

```xml
<insert id="addUser" parameterType="com.kuang.pojo.User">
    insert into mybatis.user (id,name,pwd) values (#{id},#{name},#{pwd});
</insert>
```



3.只有额基本类型参数的情况，可以直接在sql中#{}使用参数即可，例如  select * from mybatis.user where id = #{id};

```xml
<select id="getUserById" parameterType="int" resultType="com.kuang.pojo.User">
    select * from mybatis.user where id = #{id};
</select>
```

### 7.模糊查询的使用

模糊查询怎么写？

​	1、java代码执行的时候，传递通配符%%



```java
//模糊查询接口
List<User> getUserLike(String value);

@Test
public void getUserLike(){
    SqlSession sqlSession = MyBatisUtils.getSqlSession();
    UserDao mapper = sqlSession.getMapper(UserDao.class);


    List<User> users = mapper.getUserLike("%张三%");
    for (User user : users) {
        System.out.println(user);
    }

    sqlSession.close();
}
```

​	2、在sql拼接中使用通配符!

```xml
<!--模糊查询-->
<select id="getUserLike" resultType="com.kuang.pojo.User">
    select * from mybatis.user where name like "%"#{value}"%"
</select>
```



## 配置文件

严格的顺序

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration><!--配置-->
	<properties/><!--属性-->
	<settings/><!--设置-->
	<typeAliases/><!--类型别名--> 
	<typeHandlers/><!--类型处理器--> 
	<objectFactory/><!--对象工厂-->  
	<plugins/><!--插件--> 
	<environments><!--配置环境--> 
		<environment><!--环境变量--> 
		<transactionManager/><!--事务管理器--> 
			<dataSource/><!--数据源--> 
		</environment>
	</environments>
	<databaseidProvider/><!--数据库厂商标识-->  
	<mappers/><!--映射器--> 
</configuration>
```



### 1核心配置文件

![image-20201212141847626](img/image-20201212141847626.png)

 - mybatis-config.xml   这个名字可以随便起，官方建议叫mybatis-config.xml

### 2 环境配置(environments)

MyBatis 可以配置成适应多种环境 ,尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境

默认使用的环境 ID（比如：default="development"）

每个 environment 元素定义的环境 ID（比如：id="development"）

事务管理器的配置（比如：type="JDBC"）  一共两种 也就是 type="[JDBC|MANAGED]

- JDBC – 这个配置直接使用了 JDBC 的提交和回滚设施，它依赖从数据源获得的连接来管理事务作用域
- MANAGED – 这个配置几乎没做什么。它从不提交或回滚一个连接，而是让容器来管理事务的整个生命周期

数据源的配置（比如：type="POOLED"） 有三种内建的数据源类型（也就是 type="[UNPOOLED|POOLED|JNDI]"   数据源 有 dbcp c3p0

	- UNPOOLED 这个数据源的实现会每次请求时打开和关闭连接
	- POOLED 这种数据源的实现利用“池”的概念将 JDBC 连接对象组织起来，避免了创建新的连接实例时所必需的初始化和认证时间
	- JNDI 这个数据源实现是为了能在如 EJB 或应用服务器这类容器中使用，容器可以集中或在外部配置数据源，然后放置一个 JNDI 上下文的数据源引用

```xml
<environments default="development">
    <environment id="development">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
            <property name="driver" value="com.mysql.jdbc.Driver"/>
            <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;characterEncoding=UTF-8&amp;useUnicode=True"/>
            <property name="username" value="root"/>
            <property name="password" value="123456"/>
        </dataSource>
    </environment>
    
    <environment id="test">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
            <property name="driver" value="com.mysql.jdbc.Driver"/>
            <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;characterEncoding=UTF-8&amp;useUnicode=True"/>
            <property name="username" value="root"/>
            <property name="password" value="123456"/>
        </dataSource>
    </environment>
</environments>
```

可以放多个环境



Mybatis默认的事务管理器就是JDBC，连接池是POOLED



### 3 属性(Properties)

我们可以通过Properties属性来实现引用配置文件，这些属性都可以外部配置且可动态替换的，既可以在典型的jva配置文件中配置，也可以通过properties元素的子元素来传递

<Propertise></Properties>需要放在核心配置文件的第一个，不然就会报错，

![image-20201212163648531](img/image-20201212163648531.png)

方式一： 现在项目的resources目录下建立db.properties, 然后在核心配置文件引入 <properties resource="db.properties" />就可以使用了；

```java
	<properties resource="db.properties" />

    <environments default="development">
        <environment id="development">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
            <property name="driver" value="${driver}"/>
            <property name="url" value="${url}"/>
            <property name="username" value="${username}"/>
            <property name="password" value="${password}"/>
        </dataSource>
    </environment>
```



注意1：除了从配置文件获取参数，我们还可以在properties里面设置参数，如果在配置里面设置了username,在db.properties也设置了username，则db.properties的优先级大于配置里面的

```xml
<properties resource="db.properties" >
    <property name="username" value="testuser"/>
    <property name="password" value="123456"/>
</properties>

```

在上述例子，db.properties有username =root, 配置中有  <property name="username" value="testuser"/> 使用的username是db.properties里面的属性



如果一个属性在不只一个地方进行了配置，那么，MyBatis 将按照下面的顺序来加载：

	- 首先读取在 properties 元素体内指定的属性
	- 然后根据 properties 元素中的 resource 属性读取类路径下属性文件，或根据 url 属性指定的路径读取属性文件，并覆盖之前读取过的同名属性
	- 最后读取作为方法参数传递的属性，并覆盖之前读取过的同名属性



### 4 类型别名(typeAliases)



类型别名可为 Java 类型设置一个缩写名字。 它仅用于 XML 配置，意在降低冗余的全限定类名书写。意在减少类完全限定名的冗余

```xml
<typeAliases>
    <typeAlias alias="user" type="com.kuang.pojo.User"/>
</typeAliases>
```

对应的在Mapper里面就可以写

```xml
原来
<select id="getUserList" resultType="com.kuang.pojo.User">
select * from mybatis.user;
</select>
更改后
<select id="getUserList" resultType="user">
select * from mybatis.user;
</select>
```

方式二：可以直接扫描一个包

可以指定一个包名，MyBatis会在包名下面搜索需要的Java Bean,比如： 扫描实体类的包，他的默认别名就为这个类起别名，首字母小写!

```xml
<typeAliases>
    <typeAlias alias="user" type="com.kuang.pojo.User"/>
    <package name="com.kuang.pojo"/>
</typeAliases>
```

在实体类比较少的时候，可以使用第一种方式，

如果实体类较多，十分多，建议使用第二种方式

第一种可以DIY别名，第二种不行，第二种默认自动生成小写字母！



###  5 设置

| 设置名             | 描述                                                         | 有效值        | 默认值 |
| :----------------- | :----------------------------------------------------------- | :------------ | :----- |
| cacheEnabled       | 全局性地开启或关闭所有映射器配置文件中已配置的任何缓存。     | true \| false | true   |
| lazyLoadingEnabled | 延迟加载的全局开关。当开启时，所有关联对象都会延迟加载。 特定关联关系中可通过设置 `fetchType` 属性来覆盖该项的开关状态。 | true \| false | false  |

| useGeneratedKeys         | 允许 JDBC 支持自动生成主键，需要数据库驱动支持。如果设置为 true，将强制使用自动生成主键。尽管一些数据库驱动不支持此特性，但仍可正常工作（如 Derby）。 | true \| false | False |
| ------------------------ | ------------------------------------------------------------ | ------------- | ----- |
| mapUnderscoreToCamelCase | 是否开启驼峰命名自动映射，即从经典数据库列名 A_COLUMN 映射到经典 Java 属性名 aColumn。 | true \| false | False |

| logImpl | 指定 MyBatis 所用日志的具体实现，未指定时将自动查找。 | SLF4J \| LOG4J \| LOG4J2 \| JDK_LOGGING \| COMMONS_LOGGING \| STDOUT_LOGGING \| NO_LOGGING | 未设 |
| ------- | ----------------------------------------------------- | ------------------------------------------------------------ | ---- |
|         |                                                       |                                                              |      |



### 6  其他设置







### 7. 映射器

MapperRegistry :注册绑定我们的Mapper文件

方式1:

```xml
<!-- 使用相对于类路径的资源引用 -->
<mappers>
  <mapper resource="org/mybatis/builder/AuthorMapper.xml"/>
  <mapper resource="org/mybatis/builder/BlogMapper.xml"/>
  <mapper resource="org/mybatis/builder/PostMapper.xml"/>
</mappers>
```

方式2：使用class文件进行绑定

```xml
<!-- 使用映射器接口实现类的完全限定类名 -->
<mappers>
  <mapper class="org.mybatis.builder.AuthorMapper"/>
  <mapper class="org.mybatis.builder.BlogMapper"/>
  <mapper class="org.mybatis.builder.PostMapper"/>
</mappers>
```

注意点：

UserMapper.java和UserMapper.xml尽可能放到一个文件夹，

如果把UserMapper.xml放入到其他文件夹，则使用方式二的时候系统会报找不到对应的Mapper的错误

同时UserMapper.java和UserMapper.xml文件名需要都是UserMapper，如果改成UserDao.java，那么也会出现找不到对应的mapper的错误



- 接口和他的Mapper配置文件必须同名
- 接口和他的Mapper配置文件必须同文件夹



这样也可以

![image-20220522230618183](img/image-20220522230618183.png)

![image-20220522230634941](img/image-20220522230634941.png)

也会出现在相同文件夹





方式三。使用扫描包注入进行绑定，注意事项和方式二一样



练习作业：

	- 将数据库配置文件外部引入
	- 实体类别名
	- 保证UserMapper和UserMapper.xml改为一致并且放在同一个包下面

### 8 声明周期和作用域

生命周期和作用域是至关重要的，，因为错误的使用会导致非常严重的并发问题

![image-20201212183142581](img/image-20201212183142581.png)

**SqlSessionFactoryBuilder**:

	- 一旦创建了SqlSessionFactory, 就不再需要SqlSessionFactoryBuild了，所以可以定于为局部变量

**SqlSessionFactory**

- 说白了就是可以想象为我们的数据库连接池
- 一旦创建了就应该在应用的运行期间一直存在， 没有任何理由丢弃它或者重新创建另一个实例，多次创建**SqlSessionFactory**会导致程序崩溃
- 因此**SqlSessionFactory**的最佳作用域是在应用作用域，程序开始就开始，程序结束再结束
- 最简单的是使用单例模式或者静态单例模式，全局只保存一个对象

**SqlSession**

- 连接到我们连接池的一个请求! 
- 请求完需要完毕，请求前需要开启，最佳的作用域是放到一个方法里面，用完之后就需要赶紧关闭掉，否则资源被占用! 这个关闭的操作是十分重要的!

![image-20201212183934691](img/image-20201212183934691.png)



这里面的每一个mapper，就代表一个具体的业务!

## 解决属性名和字段名不一致的问题

### 5.1 问题模拟



数据库中的字段“

![image-20201212195513882](img/image-20201212195513882.png)

新建一个项目，拷贝之前的,测试实体类字段不一致的情况

```java
public class User {
    private int id;
    private String name;
    private String password;
}
```

测试后发现，因为sql数据库字段和User对象的属性名不同，从而导致出现password为空

```
User{id=4, name='张三丰', password='null'}
```

解决方法一：修改一下sql语句，把pwd as password

```xml
    <select id="getUserById" resultType="com.kuang.pojo.User">
        <!--select * from mybatis.user where id =#{id};-->
        select id,name,pwd as password from mybatis.user where id=#{id};
     </select>
```



### 5.2 resultMap

一个简单的结果集映射例子 ：



```
数据库字段   id   name   pwd
对象的属性   id   name   password
```



使用方法:

第一步，将Mapper中的resultType去掉，加上resultMap，如下图

```java
<select id="getUserById" resultMap="UserMap">
    select * from mybatis.user where id =#{id};
<!--select id,name,pwd as password from mybatis.user where id=#{id};-->
    </select>
```



resultMap = “UserMap”  这个名字自己随便起,但是要和第二步的结果集定义匹配上

第二步，在当前文件里，定义一个映射对

```xml
<resultMap id="UserMap" type="com.kuang.pojo.User">
    <!--column数据库中的字段，property实体类中的属性-->
    <result column="id" property="id" />
    <result column="name" property="name" />
    <result column="pwd" property="password" />
</resultMap>
```

此处的id和 select里面的resultMap对应， type为映射的对象，property   实体类中的属性   column数据库中的字段

### 5.3 结果映射 resultMap

- `resultMap` 元素是 MyBatis 中最重要最强大的元素

- ResultMap 的设计思想是，对简单的语句做到零配置，对于复杂一点的语句，只需要描述语句之间的关系就行了。
- `ResultMap` 的优秀之处——你完全可以不用显式地配置它们, 什么不一样转什么, 上面的那个resultMap也可以写成下面的样子

```xml
    <!--结果集映射-->
    <resultMap id="UserMap" type="com.kuang.pojo.User">
        <!--property   实体类中的属性   column数据库中的字段-->
        <!--<result column="id" property="id" />-->
        <!--<result column="name" property="name" />-->
        <result column="pwd" property="password" />
    </resultMap>
```



## 日志设置

### 6.1 日志工厂

如果 数据库操作出现了异常，我们需要一个拍错，这时候日志就是最好的助手!

曾经:sout  debug

| logImpl | 指定 MyBatis 所用日志的具体实现，未指定时将自动查找。 | SLF4J \| LOG4J \| LOG4J2 \| JDK_LOGGING \| COMMONS_LOGGING \| STDOUT_LOGGING \| NO_LOGGING |
| ------- | ----------------------------------------------------- | :----------------------------------------------------------- |
|         |                                                       |                                                              |

如今:使用日志工厂

- slf4j
- log4j [掌握] 
- log4j2
- jdk-logging
- commons_logging
- STDOUT_LOGGING[掌握] 
- NO_LOGGING

在mybatis中具体使用那个日志，我们可以设置

**STDOUT_LOGGING 标准日志输出**

在mybatis核心配置文件中，配置我们的日志

```xml
<settings>
	<setting name="logImpl" value="STDOUT_LOGGING"/>
</settings>
```



![image-20201212215726401](img/image-20201212215726401.png)



### 6.2 log4j 日志实现

现在Mybatis的配置中设置，记住是大写的，并且格式一定要对，然后导入log4j的包

**什么是log4j：**

​	Log4j是[Apache](https://baike.baidu.com/item/Apache/8512995)的一个开源项目，通过使用Log4j，

​	我们可以控制日志信息输送的目的地是[控制台](https://baike.baidu.com/item/控制台/2438626)、文件、[GUI](https://baike.baidu.com/item/GUI)组件，甚至是套接口服务器、[NT](https://baike.baidu.com/item/NT/3443842)的事件记录器、[UNIX](https://baike.baidu.com/item/UNIX) [Syslog](https://baike.baidu.com/item/Syslog)[守护进程](https://baike.baidu.com/item/守护进程/966835)等；

​	我们也可以控制每一条日志的输出格式；

​	通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程。

​	这些可以通过一个[配置文件](https://baike.baidu.com/item/配置文件/286550)来灵活地进行配置，而不需要修改应用的代码。

log4j的下载：

```xml
<!-- https://mvnrepository.com/artifact/log4j/log4j -->
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```



log4j.properties

```properties
# priority  :debug<info<warn<error
#you cannot specify every priority with different file for log4j
log4j.rootLogger=DEBUG,console,file,info
#file
log4j.appender.file = org.apache.log4j.RollingFileAppender
log4j.appender.file.File = ./log/kuang.log
log4j.appender.file.MaxFileSize=10mb
log4j.appender.file.Threshold=DEBUG
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=[%p][%d{yy-mm-dd}][%c]%m%n
#console
log4j.appender.console=org.apache.log4j.ConsoleAppender
log4j.appender.console.Target=System.out
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.layout=org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=[%c]-%m%n
#日志输出级别
log4j.logger.org.mybatis=DEBUG
log4j.logger.java.sql=DEBUG
log4j.logger.java.sql.Statement=DEBUG
log4j.logger.java.sql.ResultSet = DEBUG
log4j.logger.java.sql.PrepareStatement=DEBUG


#info log
log4j.logger.info=info
log4j.appender.info=org.apache.log4j.DailyRollingFileAppender
log4j.appender.info.DatePattern='_'yyyy-MM-dd'.log'
log4j.appender.info.File=../log/info.log
log4j.appender.info.Append=true
log4j.appender.info.Threshold=INFO
log4j.appender.info.layout=org.apache.log4j.PatternLayout
log4j.appender.info.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss a} [Thread: %t][ Class:%c >> Method: %l ]%n%p:%m%n
#debug log
log4j.logger.debug=debug
log4j.appender.debug=org.apache.log4j.DailyRollingFileAppender
log4j.appender.debug.DatePattern='_'yyyy-MM-dd'.log'
log4j.appender.debug.File=./src/com/hp/log/debug.log
log4j.appender.debug.Append=true
log4j.appender.debug.Threshold=DEBUG
log4j.appender.debug.layout=org.apache.log4j.PatternLayout 
log4j.appender.debug.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss a} [Thread: %t][ Class:%c >> Method: %l ]%n%p:%m%n
#warn log
log4j.logger.warn=warn
log4j.appender.warn=org.apache.log4j.DailyRollingFileAppender 
log4j.appender.warn.DatePattern='_'yyyy-MM-dd'.log'
log4j.appender.warn.File=./src/com/hp/log/warn.log
log4j.appender.warn.Append=true
log4j.appender.warn.Threshold=WARN
log4j.appender.warn.layout=org.apache.log4j.PatternLayout 
log4j.appender.warn.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss a} [Thread: %t][ Class:%c >> Method: %l ]%n%p:%m%n
#error
log4j.logger.error=error
log4j.appender.error=org.apache.log4j.DailyRollingFileAppender
log4j.appender.error.DatePattern='_'yyyy-MM-dd'.log'
log4j.appender.error.File=./src/com/hp/log/error.log 
log4j.appender.error.Append=true
log4j.appender.error.Threshold=ERROR 
log4j.appender.error.layout=org.apache.log4j.PatternLayout
log4j.appender.error.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss a} [Thread: %t][ Class:%c >> Method: %l ]%n%p:%m%n
```



log4j的使用! 直接测试运行刚才的查询

![image-20201212223647843](img/image-20201212223647843.png)

### 6.3 简单使用



1.在要使用Log4j的类中，导入包import org.apache.log4j.Logger

2.日志对象，参数为当前类的class

```java
static Logger logger = Logger.getLogger(UserTest.class);
```

3. 设置日志级别

```java
@Test
public void testLog4j(){
logger.info("info:进入了testLog4j~~~我已经运行到这里了!");
logger.debug("debug:进入了testLog4j~~~我已经运行到这里了!");
logger.error("error:进入了testLog4j~~~我已经运行到这里了!");
}
```

### 6.4 log4j的日志规则

```
#如果使用pattern布局就要指定的打印信息的具体格式ConversionPattern，打印参数如下：

#%m 输出代码中指定的消息

#%p 输出优先级，即DEBUG，INFO，WARN，ERROR，FATAL

#%r 输出自应用启动到输出该log信息耗费的毫秒数

#%c 输出所属的类目，通常就是所在类的全名

#%t 输出产生该日志事件的线程名

#%n 输出一个回车换行符，Windows平台为“rn”，Unix平台为“n”

#%d 输出日志时间点的日期或时间，默认格式为ISO8601，也可以在其后指定格式，比如：%d{yyyy MMM dd HH:mm:ss,SSS}，输出类似：2002年10月18日 22：10：28，921

#%l 输出日志事件的发生位置，包括类目名、发生的线程，以及在代码中的行数。

#[QC]是log信息的开头，可以为任意字符，一般为项目简称。

#输出的信息

#[TS] DEBUG [main] AbstractBeanFactory.getBean(189) | Returning cached instance of singleton bean 'MyAutoProxy'
#
log4j.rootLogger=INFO, stdout

log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{yyyy/MM/dd HH:mm:ss,S} %p [%c]  >>> %m %n
```

输出的结果：

![image-20210214121535889](img/image-20210214121535889.png)



## mybtis分页

思考：为什么要分页？ 减少数据的处理量

使用Limit分页

```
语法: select * from user limit startIndex,pageSize;
 select * from user limit 0,2;  每页显示2个，从第0个开始查，获取0,1
 select * from user limit 2,2;  每页显示2个，从第0个开始查，获取2,3
 select * from user limit 3；    #[0,n] 
```

### 7.1 使用Limit分页

使用Mybatis实现分页，核心就是sql, 下面是一个使用Limit分页的例子



step1、写接口  UserMapper

```java
public interface UserMapper {
    //根据ID查询用户
    User getUserById(int id);
    //分页查询,我们使用万能的map
    List<User> getUserByLimit(Map<String, Integer> map);
}
```



step2、写映射文件UserMapper.xml

```xml
<mapper namespace="com.kuang.dao.UserMapper">

    <!--结果集映射-->
    <resultMap id="UserMap" type="com.kuang.pojo.User">
        <!--property   实体类中的属性   column数据库中的字段-->
        <!--<result column="id" property="id" />-->
        <!--<result column="name" property="name" />-->
        <result column="pwd" property="password" />
    </resultMap>

    <select id="getUserById" resultMap="UserMap" resultType="com.kuang.pojo.User">
        select * from mybatis.user where id =#{id};
        <!--select id,name,pwd as password from mybatis.user where id=#{id};-->
    </select>
    
	<!--分页查询-->
    <select id="getUserByLimit" parameterType="map" resultMap="UserMap">
        select * from mybatis.user limit #{startIndex},#{pageSize};
    </select>

</mapper>
```



step3、测试代码 testGetUserByLimig

```java
    @Test
    public void testGetUserByLimig(){
        SqlSession sqlSession = Mybatis.getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        Map<String, Integer> map = new HashMap<String, Integer>();
        map.put("startIndex",0);
        map.put("pageSize",2);
        List<User> userByLimit = mapper.getUserByLimit(map);
        for (User user : userByLimit) {
            System.out.println(user);
        }

        sqlSession.close();
    }
}
```



### 7.2 RowBounds分页

1、不再使用SQL实现分页，接口

```java
public interface UserMapper {
    //分页2，使用RowBounds
    List<User> getUserByRowBounds();
}
```



2、mapper.xml

```xml
<mapper namespace="com.kuang.dao.UserMapper">

    <!--结果集映射-->
    <resultMap id="UserMap" type="com.kuang.pojo.User">
        <!--property   实体类中的属性   column数据库中的字段-->
        <!--<result column="id" property="id" />-->
        <!--<result column="name" property="name" />-->
        <result column="pwd" property="password" />
    </resultMap>
    <!--分页2 查询 RowBounds-->
    <select id="getUserByRowBounds" resultMap="UserMap">
        select * from mybatis.user;
    </select>
</mapper>
```



3、测试

```java
@Test
public void getUserByRowBounds(){
    SqlSession sqlSession = Mybatis.getSqlSession();

    //RowBounds实现
    RowBounds rowBounds = new RowBounds(1,2);

    //通过Java代码层面实现分页
    List<User> objects = sqlSession.selectList("com.kuang.dao.UserMapper.getUserByRowBounds",null,rowBounds);

    for (User object : objects) {
        System.out.println(object);
    }
    sqlSession.close();
}
```

### 7.3 分页插件 mybatis pageHelper

![image-20201213152533578](img/image-20201213152533578.png)



了解即可，万一以后公司的架构师说，要使用，我们需要知道他是一个什么东西!

## 注解开发

### 8.1 面向接口编程

大家之前都学过面向对象编程，也学习过接口，但是真正的开发中，很多时候我们会选择面向接口编程，

根本原因，``解耦``，可拓展，提高复用，分层开发中，上层不用管具体的实现，大家都遵守共同的标准，使得开发变得容易，规范性更好

在一个面向对象的系统中，系统的各种功能是由许许多多的不同对象协作完成的，在这种情况下，各个对象内部是如何实现自己的，对系统设计人员来讲不那么重要了

而各个对象之间的协作关系则成为了系统设计的关键，小到不同类之间的通信，大到各个模块之间的交互，在系统设计之初都是要着重考虑的，这也是系统设计的主要工作内容，面向

接口编程就是指按照这种思想来编程。



关于接口的理解

接口从更深层的理解，应该是定义(规范，约束)与实现(实名分离的原则)的分离

接口的本身反映了设计人员对系统的抽象理解

接口应该有两类

	- 第一类对一个个体的抽象，他对应为一个抽象体(abstract class)
	- 第二类是一个个体某一方面的抽象，既形成一个抽象面(interface)

一个个体有可能有多个抽象面，抽象提与抽象面是有区别的。



三个面向的区别

面向对象是指，我们考虑问题时，以对象为单位，考虑他的属性及方法

面向过程是指 ，我们考虑问题时，以一个具体的流程（事务过程）为单位，考虑它的实现

接口设计与非接口设计是针对复用技术而言的， 与面向对象(过程)不是一个问题，更多的体现就是对系统整体的架构



### 8.2 使用注解开发

```java
@Select("select * from user")
List<User> getUser();
```

```java
@Test
public void test(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    List<User> userList = mapper.getUser();
    for (User user : userList) {
        System.out.println(user);
    }
    sqlSession.close();
}
```

1、注解就是直接在接口上实现

2、需要在我们的mybatis核心配置文件中绑定接口

3、测试

本质，是我们反射机制实现

底层：动态代理模式

![image-20201213163511707](img/image-20201213163511707.png)

![image-20201213163635965](img/image-20201213163635965.png)

**Mybatis详细的执行流程!**



![image-20201213183347778](img/image-20201213183347778.png)

![image-20201213183359073](img/image-20201213183359073.png)

编写XML——resources加载全局配置文件——build构造器——加载配置文件流——把配置信息交给工厂实例化——进入事务管理器——创建执行器——创建sql持久化对象——实现CRUD——查看是否成功——提交事务——关闭

### 8.3 CRUD注解操作

我们可以在工具类创建的时候，实现自动提交事务, 这样就可以不用每次执行sqlSession.commit()的手动提交

```java
public static SqlSession getSqlSession(){
    //public SqlSession openSession(boolean autoCommit)
    return sqlSessionFactory.openSession(true);//这个地方的true就是autoCommit
}
```



一、查询注解方式

注意，这里面@Select("select * from user where id=#{id} and name=#{name}") 的id和name通 @param("id")是匹配的

```java
//1.通过id,name查询,方法存在多个参数，所有参数前面必须加上@Param注解
@Select("select * from user where id=#{id} and name=#{name}")
User getUserByIdName(@Param("id") int id, @Param("name") String name);
//2.通过id查询
@Select("select * from user where id=#{id}")
User getUserById(@Param("id") int id);
//3.查询用户
@Select("select * from user")
List<User> getUserList();
```

二、添加用户--注解方式

```java
//添加用户，对象类就直接用对象类，不用@param
@Insert("insert into user(id,name,pwd) values (#{id},#{name},#{password})")
int addUser(User user);
```

三、更改用户 -注解方式

```java
//修改用户，对象类直接用对象类，不用@param
@Update("update user set name = #{name}, pwd=#{password} where id =#{id}")
int updateUser(User user);
```



四、删除注解方式

```java
@Delete("delete from user where id =#{uid}")
int deleteUser(@Param("uid") int id);
```

`关于@Param()注解`

- 基本类型的参数或者String类型，需要加上
- 引用类型不需要加
- 如果只有一个基本类型的话，可以忽略，但是建议大家都加上!
- 我们在SQL中引用的就是我们这里@Param("uid")中设定的属性名!



## Lombok

使用步骤

1、在IDEA中安装Lombok

2、在Lombok中导入jar包

```xml
<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.12</version>
    <scope>provided</scope>
</dependency>
```



3、可以使用的注解

```java
Features
@Getter and @Setter
@FieldNameConstants
@ToString
@EqualsAndHashCode
@AllArgsConstructor, @RequiredArgsConstructor and @NoArgsConstructor
@Log, @Log4j, @Log4j2, @Slf4j, @XSlf4j, @CommonsLog, @JBossLog, @Flogger, @CustomLog
@Data
@Builder
@SuperBuilder
@Singular
@Delegate
@Value
@Accessors
@Wither
@With
@SneakyThrows
@val
@var
experimental @var
@UtilityClass
Lombok config system
```

4、在实体类上面加注解

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
@ToString
@EqualsAndHashCode
public class User {
    private int id;
    private String name;
    private String password;

}
```



## 多对一查询

![image-20201213212031483](img/image-20201213212031483.png)

- 多个学生，对应 一个老师
- 对于学生这边而言， **关联**...  多个学生关联一个老师  [多对一] association  is-a,张三是李老师的学生
- 对于老师这边而言，**集合**...一个老师有很多学生 [ 一对多]  collection   has a, 李老师有个学生叫张三

 

测试环境的Sql

```sql
use `mybatis`
create table `teacher`(
	`id` int(10) not null,
	`name` varchar(30) default null,
	primary key(`id`)
)engine=innodb default charset=utf8

insert into `teacher`(`id`,`name`)values(1,'秦老师');

create table `student`(
	`id` int(10) not null,
	`name` varchar(30) default null,
	`tid` int(10) default null,
	primary key(`id`),
	key `fktid`(`tid`),
	constraint `sktid` foreign key(`tid`) references `teacher`(`id`)
)engine=innodb default charset=utf8

insert into `student`(`id`,`name`,`tid`) values('1','小明','1');
insert into `student`(`id`,`name`,`tid`) values('2','小红','1');
insert into `student`(`id`,`name`,`tid`) values('3','小张','1');
insert into `student`(`id`,`name`,`tid`) values('4','小李','1');
insert into `student`(`id`,`name`,`tid`) values('5','小王','1');
```



**搭建测试环境步骤**

1、 导入lombok

2、新建实体类Teacher，Student

```java
@Data
@ToString
public class Teacher {
    private int id;
    private String name;
}
```



3、建立Mapper接口

```java
public interface TeacherMapper {
    //查询教师
    @Select("select * from teacher where id = #{tid}")
    Teacher getTeacherById(@Param("tid") int id);
}
```



4、建立Mapper.xml文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.kuang.dao.TeacherMapper">

</mapper>
```



5、在核心配置文件中绑定注册我们的Mapper接口或者文件![方式很多，随心选择]

```xml
<mappers>
    <mapper class="com.kuang.dao.TeacherMapper"/>
    <mapper resource="com/kuang/dao/StudentMapper.xml"/>
</mappers>
```

6、测试查询是否能够成功

```java
    @Test
    public void getTeacherById(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        TeacherMapper mapper = sqlSession.getMapper(TeacherMapper.class);
        Teacher teacher = mapper.getTeacherById(1);
        System.out.println(teacher);


        sqlSession.close();
    }
```

![image-20220522230952226](img/image-20220522230952226.png)

意思是pojo不一定要和数据库一一对应

### 10.1 按照查询嵌套处理

需求1:获取学生信息以及对应的老师信息

```xml
<mapper namespace="com.kuang.dao.StudentMapper">
    <!--查询所有学生信息及对应的老师信息
        问题:Teacher是一个对象，拿到的是空值
        解决思路:
            1.查询所有的学生信息
            2.根据查询出来的学生的tid，寻找对应的老师
    -->

    <!--<select id="getStudentList" resultType="com.kuang.pojo.Student">-->
    <!--    select s.id,s.name,t.name from student s,teacher t  where s.tid=t.id;-->
    <!--</select>-->
    <!--按照查询，嵌套处理：上面这个方法无法解决我们的问题，因为Teacher是一个对象，而不是一个字段，-->
    <select id="getStudentList" resultMap="StudentTeacher">
        select * from student;
    </select>

    <resultMap id="StudentTeacher" type="com.kuang.pojo.Student">
        <result property="id" column="id"/>
        <result property="name" column="name"/>
        <!--对于Teacher是对象怎么写呢 : 复杂的属性，我们需要单独处理  对象:association 集合:collection-->
        <association property="teacher" column="tid" javaType="com.kuang.pojo.Teacher" select="getTeacher"/>
    </resultMap>

    <select id="getTeacher" resultType="com.kuang.pojo.Teacher">
        select * from teacher where id =#{id};
    </select>
</mapper>

`注意`： select * from teacher where id =#{id}; 这里面的#{id}可以随便填写任意数据，比如#{affsdfasdfasd}都是可以的，因为
<association property="teacher" column="tid" javaType="com.kuang.pojo.Teacher" select="getTeacher"/> 这里只有一个property
```

### 10.2 按照结果嵌套处理

```xml
<!--方式一、按照查询，嵌套处理：上面这个方法无法解决我们的问题，因为Teacher是一个对象，而不是一个字段，-->
<select id="getStudentList" resultMap="StudentTeacher">
    select * from student;
</select>

<resultMap id="StudentTeacher" type="com.kuang.pojo.Student">
    <result property="id" column="id"/>
    <result property="name" column="name"/>
    <!--对于Teacher是对象怎么写呢 : 复杂的属性，我们需要单独处理  对象:association 集合:collection-->
    <association property="teacher" column="tid" javaType="com.kuang.pojo.Teacher" select="getTeacher"/>
</resultMap>

<select id="getTeacher" resultType="com.kuang.pojo.Teacher">
    select * from teacher where id =#{id};
</select>

<!--方式二、按照结果嵌套处理-->
<select id="getStudentList2" resultMap="StudentTeacher2">
    select s.id sid,s.name sname, t.name tname
    from student s, teacher t
    where s.tid = t.id
</select>

<resultMap id="StudentTeacher2" type="com.kuang.pojo.Student">
    <result property="id" column="sid"/>
    <result property="name" column="sname"/>
    <association property="teacher" javaType="com.kuang.pojo.Teacher">
        <result property="name" column="tname"/>
    </association>
</resultMap>
```



回顾Mysql多对一查询方式；

一种叫做子查询

```sql
select id,name,tid from student
    where tid=(select tid from teacher)
```



一种叫做连表查询

```sql
select s.id sid,s.name sname, t.name tname
from student s, teacher t
where s.tid = t.id;
```



## 一对多查询

比如：一个老师拥有多个学生，对于老师而言，就是1对多的关系，集合

### 11.1 按照结果嵌套处理

1、环境搭建，和刚才一样

老师的实体类和学生的实体类改变一下

```java
//学生实体类
public class Student {
    private int id;
    private String name;
    private int tid;
}
```

```java
//老师的实体类
public class Teacher {
    private int id;
    private String name;
    //一个老师拥有多个学生
    private List<Student> students;
}
```

**和多对一不同地方**

- Student实体类，在多对一，关联的时候， 学生的实体放入的是 private Teacher teacher; 现在变为了  private int tid;
- Teacher实体类，在多对一，关联的时候，老师的实体类放入的只有id和name，现在变成了新加一个学生集合：private List<Student> students;



需求：获取指定老师下的所有学生及老师的信息

接口信息：

```java
public interface TeacherMapper {
    //获取老师
    // List<Teacher> getTeacher();
    //获取指定老师下的所有学生及老师信息
    Teacher getTeacher(@Param("tid") int id);
    //方式2 子查询方式
    Teacher getTeacher2(@Param("tid") int id);
}
```

接口映射文件信息

```xml
<mapper namespace="com.kuang.dao.TeacherMapper">
    <!--方案一：按照结果嵌套查询  获得所有老师-->
    <select id="getTeacher" resultMap="TeacherStudent">
        select s.id sid,s.name sname,t.name tname, t.id tid
        from student s,teacher t
        where s.tid=t.id and t.id=#{tid}
    </select>
    
    <resultMap id="TeacherStudent" type="com.kuang.pojo.Teacher">
        <result property="name" column="tname"/>
        <result property="id" column="tid"/>
        <!--复杂的属性，我们需要单独处理，对象association 集合 collection
            association  使用javaType 指定一个java类型的属性类型
            collection   使用list 集合中的泛型信息，我们使用 ofType获取
         -->
        <collection property="students" ofType="com.kuang.pojo.Student">
            <result property="id" column="sid"/>
            <result property="name" column="sname"/>
            <result property="tid" column="tid"/>
        </collection>
    </resultMap>
    
</mapper>
```

测试类

```
    @Test
    public void getTeacher(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        TeacherMapper mapper = sqlSession.getMapper(TeacherMapper.class);
       Teacher teacher = mapper.getTeacher(1);

       System.out.println(teacher);
       
        sqlSession.close();
    }
```

测试结果:

```verilog
Teacher(id=1, name=秦老师, students=[Student(id=1, name=小明, tid=1), Student(id=2, name=小红, tid=1), Student(id=3, name=小张, tid=1), Student(id=4, name=小李, tid=1), Student(id=5, name=小王, tid=1)])
```



### 11.2 按照查询嵌套处理

方式二： 子查询方式使用

```xml
    <!--======================-->
    <!--方案二：子查询方式-->
    <select id="getTeacher2" resultMap="TeacherStudent2">
        select * from teacher where id = #{tid}
    </select>

    <resultMap id="TeacherStudent" type="com.kuang.pojo.Teacher">
        <!--记住集合有javaType-->
        <collection property="students" column="id" javaType="ArrayList" ofType="com.kuang.pojo.Student" select="getStudentTByTeacherID"/>
        <!--这里记住，这个里面的column是上面select查询结果的id，返回给下面select语句作为参数 tid-->
    </resultMap>

    <select id="getStudentTByTeacherID" resultType="com.kuang.pojo.Student">
        select * from student where tid = #{tid}
    </select>

`注意`： select * from teacher where id =#{id}; 这里面的#{id}可以随便填写任意数据，比如#{affsdfasdfasd}都是可以的，因为
<association property="teacher" column="tid" javaType="com.kuang.pojo.Teacher" select="getTeacher"/> 这里只有一个property
```





### 11.3 一对多小结

​	1、关联 association  多个学生关联一个老师，多对一  

​	2、集合 collection  一个老师包含多个学生  1对多

​	3、javaType & ofType

​			javaType用来指定实体类型中属性的类型

​	  	 ofType用来指定映射到List或者集合里面的pojo类型，类似泛型中的约束类型





注意点

	- 保证SQL的可读性，尽量保证通俗一度
	- 注意一对多和多对一种，属性名和字段的问题
	- 如果问题不好排查错误，可以使用日志，建议使用log4j



慢SQL  别人查询1s，你查询可能需要1000S，可能直接就被开除了，

面试必问的：

​	mysql innodb和其他引擎底层原理和区别， 

​	索引及索引的优化 存储的过程





## 动态SQL

什么是动态SQL    动态SQL就是指根据不同的条件生成不同的SQL语句

借助功能强大的基于 OGNL 的表达式，MyBatis 3 替换了之前的大部分元素，大大精简了元素种类，现在要学习的元素种类比原来的一半还要少。

- if
- choose (when, otherwise)
- trim (where, set)
- foreach



### 12.1 搭建开发环境

准备sql语句

```sql
use `mybatis`

create table `blog`(
	`id` varchar(50) not null comment '博客id',
	`title` varchar(100) not null comment '博客标题',
	`author` varchar(30) not null comment '博客作者',
	`create_time` datetime not null comment '创建时间',
	`views` int(30) not null comment '浏览量'
)engine=innodb default charset=utf8


```



创建一个基础工程

1、导包

2、编写核心配置文件

3、编写实体类

4、编写实体类对应的Mapper接口及和实体类丢应的Mapper.xml

### 12.2 if 动态sql

dao接口

```java
public interface BlogMapper {
    //插入数据
    int addBlog(Blog blog);
    //查询博客
    List<Blog> queryBlogIF(Map map);
}
```

xml配置文件

```xml
<mapper namespace="com.kuang.dao.BlogMapper">
    <insert id="addBlog" parameterType="Blog">
        insert into mybatis.blog (id,title,author,create_time,views)
        values (#{id},#{title},#{author},#{createTime},#{views});
    </insert>

    <select id="queryBlogIF" parameterType="map" resultType="Blog">
        select * from blog where 1=1
        <if test="title!=null">
            and title = #{title}
        </if>
        <if test="author!=null">
            and author =#{author}
        </if>
    </select>

</mapper>
```





测试代码

```java
public class TestBlogMapper {
    @Test
    public void test(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
        Blog blog = new Blog();


        blog.setId(UUIDUtils.getUUID());
        blog.setTitle("Mybatis如此简单");
        blog.setAuthor("狂神说");
        blog.setCreateTime(new Date());
        blog.setViews(9999);
        //System.out.println("是否乱码"+blog);
        mapper.addBlog(blog);

        blog.setId(UUIDUtils.getUUID());
        blog.setTitle("JAVA如何简单");
        mapper.addBlog(blog);

        blog.setId(UUIDUtils.getUUID());
        blog.setTitle("SPring如何简单");
        mapper.addBlog(blog);

        blog.setId(UUIDUtils.getUUID());
        blog.setTitle("微服务如此简单");
        mapper.addBlog(blog);

        sqlSession.close();
    }
    @Test
    public void queryBlogIF(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
        Map map = new HashMap();
        //map.put("title","JAVA如何简单");
        map.put("author","狂神说");

        List<Blog> blogs = mapper.queryBlogIF(map);
        for (Blog blog : blogs) {
            System.out.println(blog);
        }

        sqlSession.close();
    }
}
```



带有where的语句

*where* 元素只会在子元素返回任何内容的情况下才插入 “WHERE” 子句。而且，若子句的开头为 “AND” 或 “OR”，*where* 元素也会将它们去除。

```xml
<select id="findActiveBlogLike"  resultType="Blog">
  SELECT * FROM BLOG
  <where>
    <if test="state != null">
         state = #{state}
    </if>
    <if test="title != null">
        AND title like #{title}
    </if>
    <if test="author != null and author.name != null">
        AND author_name like #{author.name}
    </if>
  </where>
</select>
```

### 12.3 choose(when,otherwise)

接口

```java
    //查询博客
    List<Blog> queryBlogChoose(Map map);
```





```xml
    <select id="queryBlogChoose" parameterType="map" resultType="blog">
        select * from blog
        <where>
            <choose>
                <when test="title!=null">
                    title =#{title}
                </when>
                <when test="author!=null">
                    and author=#{author}
                </when>
                <otherwise>
                    and views = #{views}
                </otherwise>
            </choose>
        </where>
    </select>
```

测试语句

```java
    @Test
    public void queryBlogChoose(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
        Map map = new HashMap();
        //map.put("title","JAVA如何简单");
        //map.put("author","狂神说");
        //map.put("author","狂神说");
        map.put("views",9999);

        List<Blog> blogs = mapper.queryBlogChoose(map);

        for (Blog blog : blogs) {
            System.out.println(blog);
        }

        sqlSession.close();
    }
```

作用总结：



### 12.4 trim(where ,set)



解释：*set* 元素会动态地在行首插入 SET 关键字，并会删掉额外的逗号（这些逗号是在使用条件语句给列赋值时引入的），*set* 元素可以用于动态包含需要更新的列，忽略其它不更新的列



例子： 我们更新一个博客

```java
//更新一个博客
int updateBlog(Map map);
```



配置

```xml
<update id="updateBlog" parameterType="map">
    <!--update blog set id=#{id},name=#{name} where id=#{id}-->
    update blog
    <set>
        <if test="title!=null">
            title =#{title},
        </if>
        <if test="author!=null">
            author =#{author},
        </if>
    </set>
    where id=#{id}
</update>
```

测试代码

```java
    @Test
    public void updateBlog(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
        Map map = new HashMap();
        map.put("title","update JAVA如何简单");
        map.put("author","update狂神说");
        //map.put("views",9999);
        map.put("id","e08bf90edb6f4983b09c0cad995be57c");
        int i = mapper.updateBlog(map);
        System.out.println(i);
        sqlSession.close();
    }
```

set元素会动态前置set关键字，同时也会删除掉无关的逗号!

所谓的动态SQL，本质还是SQL语句，只是我么可以在sql外面，去执行一个逻辑 if  where chooe set when

### 12.5 Foreach语句及Sql片段

```sql
select * from user where 1=1 and(id=1 or id =2 or id =3)  //查询id为1，或者2，或者3的用户，这种我们就可以用foreach处理
```



**sql片段**

有的时候，我们可能将一些功能的公共部分抽取出来，方便通用

使用sql片段，需要先定义，后饮用

定义

```xml
<sql id="if-title-author">
    <if test="title!=null">
        title =#{title},
    </if>
    <if test="author!=null">
        author =#{author},
    </if>
</sql>
```

引用形式:

```xml
<sql id="if-title-author">
    <if test="title!=null">
        title =#{title},
    </if>
    <if test="author!=null">
        author =#{author},
    </if>
</sql>
<update id="updateBlog" parameterType="map">
    <!--update blog set id=#{id},name=#{name} where id=#{id}-->
    update blog
    <set>
        <include refid="if-title-author"></include>
    </set>
    where id=#{id}
</update>
```

注意事项：

​	最好基于单表来定义SQL片段，这样复用性更高

​	不要提where标签，因为where会自定优化我们的sql,去掉and等字符。所以不适合放入到sql片段中





**ForEach**

```xml
<select id="selectPostIn" resultType="domain.blog.Post">
  SELECT *
  FROM user u
  WHERE 1=1 and
  <foreach item="id" index="index" collection="ids"
      open="(" separator="or" close=")">
        #{id}
  </foreach>
</select>

(id=1 or id=2 or id=3)


```

对应接口方法

```java
    //查询第1-2-3号记录的博客
    List<Blog> queryBlogByForeach(Map map);
```



测试接口配置

```xml
    <!--select * from blog where 1=3 and (id=1 or id=2 or id=3)
        我们现在传递一个万能的map,这个map中的可以存在一个集合
    -->
    <select id="queryBlogByForeach" parameterType="map" resultType="blog">

        select * from blog
        <where>
            <foreach collection="ids" item="id" open="and(" close=")" separator="or">
                id = #{id}
            </foreach>
        </where>
    </select>
```

测试代码

```java
@Test
public void queryBlogByForeach(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
    Map map = new HashMap();
    List<Integer> ids = new ArrayList<Integer>();
    ids.add(1);
    ids.add(2);
    ids.add(3);

    map.put("ids",ids);

    List<Blog> blogs = mapper.queryBlogByForeach(map);
    sqlSession.close();
}
```

**动态sql就是在拼接sql语句，我们只要保证sql的正确性，按照sql的格式，去排列组合就可以了!**

建议

​	先在mysql中写出完整的sql,再对应的去修改成为我们的动态sql，实现通用即可；

## 缓存

### 13.1 简介

>  查询，连接数据库，耗费资源
>
>  ​	字词查询的结构，给他暂存在一个可以直接取到的地方---内存；
>
>  我们再次查询相同数据的时候，直接走缓存，就不用走数据库了



1、什么是缓存[cache]

​	存在内存中的临时数据

​	将用户经常查询的数据放在缓存(内存)中，用户去查询数据就不用从磁盘上(关系型数据库数据文件)查询，从缓存中查询，从而提高查询效率，解决了高并发系统的性能问题

2、为什么使用缓存

​	减少和数据库的交互次数，减少系统的开销，提高系统的效率

3、什么样子的数据库能使用缓存

​	经常查询并且不经常改变的数据。



### 13.2 Mybatis缓存

mybatis包含一个非常强大的查询缓存特性，他可以非常方便的定制和配置缓存，缓存可以极大的提升查询效率

mybatis系统中默认定义了两级缓存，一级缓存和二级缓存

​	- 默认情况下，只有一级缓存开启，sqlsession级别的缓存，也成为了本地缓存

​	- 二级缓存需要手动开启和配置，他是基于namespace级别的缓存, 也就是在一个mapper里面，这个缓存都是有效的

​	- 为了提高扩展性，mybatis定义了缓存接口Cache，我们可以通过Cache来自定义二级缓存



### 13.3 一级缓存

一级缓存也叫本地缓存，生命周期就是一个sqlSession内

​	与数据库同一次会话期间查询到的数据会放在本地缓存中；

​	以后如果需要获取相同的数据，直接从缓存中拿，就没必须再去查询数据库；



可以测试一下，测试步骤：

开启日志

测试在一个Session中查询两次相同的记录

查看日志输出的情况

![image-20201215160555080](img/image-20201215160555080.png)

缓存失效的情况：

​	映射语句文件中的所有 insert、update 和 delete 语句会刷新缓存

​	缓存会使用最近最少使用算法（LRU, Least Recently Used）算法来清除不需要的缓存

​	缓存不会定时进行刷新（也就是说，没有刷新间隔）

​	缓存会保存列表或对象（无论查询方法返回哪种）的 1024 个引用

​	缓存会被视为读/写缓存，这意味着获取到的对象并不是共享的，可以安全地被调用者修改，而不干扰其他调用者或线程所做的潜在修改



1、增删改操作，可能会改变原来的数据，所以必定会刷新缓存!

2、查询不同的东西

3、查询不同的Mapper.xml

4、手动删除缓存  sqlSession.clearCache(); //清理缓存，会导致重新查询 缓存失效



一级缓存默认开启，只在一次SqlSession中有效，也就是拿到连接到关闭连接这个区间段!

一级缓存就是一个bug



### 13.4 二级缓存

二级缓存也叫全局缓存，一级缓存作用域太低了，所以诞生了二级缓存，

基于Namespace级别的缓存，一个名称空间，对应一个二级缓存

工作机制：

​	一个绘画查询一条数据，这个数据就会被放入到当前会话的一级缓存中；

​	如果当前会话关闭了，这个会话对应的一级缓存就没有了，但是我们想要的是，会话关闭了，一级缓存中数据被保存到了二级缓存中；

​	新的绘画查询信息，就可以从二级缓存中获取内容；

​	不同的mapper查出来的数据会放入自己对应的缓存(map)中

使用二级缓存的步骤：

1、先去核心配置中，设置开启核心缓存

```xml
<settings>
    <!--显示的开启全局缓存-二季缓存-->
    <setting name="cacheEnabled" value="true"/>
    <!--指定 MyBatis 所用日志的具体实现-->
    <setting name="logImpl" value="STDOUT_LOGGING"/>
</settings>
```

2、到需要开启二级缓存的Mapper.xml二级缓存的配置文件中增加<cache/> 标签，即可使用

```xml
<cache/>
```



也可以自定义一些参数

```xml
<cache
  eviction="FIFO"
  flushInterval="60000"
  size="512"
  readOnly="true"/>
```

![image-20201215162632872](img/image-20201215162632872.png)



测试：

```java
    @Test
    public void test2(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        SqlSession sqlSession2 = MybatisUtils.getSqlSession();
        
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        UserMapper mapper2 = sqlSession2.getMapper(UserMapper.class);

        User user = mapper.queryUserById(1);
        System.out.println(user);
        System.out.println("====================");

        User user2 = mapper2.queryUserById(1);
        System.out.println(user2);
        System.out.println("====================");

        sqlSession.close();
        sqlSession2.close();
    }
```

小结：

​	只要开启了二级缓存，在同一个mapper下就有效

​	所有的数据都会先放入一级缓存

​	只有当绘画提交或者关闭，这时候才会提交到耳机缓存

### 13.5 缓存原理

![image-20201215183826712](img/image-20201215183826712.png)



### 13.6 自定义缓存-ehcache



要在程序中使用ehcache，需要先导入包!

```pom
<dependency>
<groupId>org.mybatis.caches</groupId>
<artifactId>mybatis-ehcache</artifactId>
<version>1.1.0</version>
</dependency>
```

在mapper.xml中进行配置

```xml
<mapper namespace="com.kuang.dao.UserMapper">
    <!--在当前Mapper.xml中使用ehcache-->
    <cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
    
    <select id="queryUserById" parameterType="_int" resultType="user">
        select * from user where id = #{id}
    </select>
</mapper>
```





ehcache的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"
         updateCheck="false">
     <!--
 5         磁盘存储:将缓存中暂时不使用的对象,转移到硬盘,类似于Windows系统的虚拟内存
 6         path:指定在硬盘上存储对象的路径
 7      -->
     <diskStore path="./tmpdir/Tmp_EhCache" />


     <!--
         defaultCache:默认的缓存配置信息,如果不加特殊说明,则所有对象按照此配置项处理
         maxElementsInMemory:设置了缓存的上限,最多存储多少个记录对象
        eternal:代表对象是否永不过期
         timeToIdleSeconds:最大的发呆时间
        timeToLiveSeconds:最大的存活时间
         overflowToDisk:是否允许对象被写入到磁盘
     -->
     <defaultCache
             eternal="false"
             maxElementsInMemory="10000"
             overflowToDisk="false"
             diskPersistent="false"
             timeToIdleSeconds="1800"
             timeToLiveSeconds="259200"
             memoryStoreEvictionPolicy="LRU" />

     <!--
         cache:为指定名称的对象进行缓存的特殊配置
         name:指定对象的完整名
      -->
     <cache name="cloud_user"
            eternal="false"
            maxElementsInMemory="5000"
            overflowToDisk="false"
            diskPersistent="false"
            timeToIdleSeconds="1800"
            timeToLiveSeconds="1800"
            memoryStoreEvictionPolicy="LRU"
     />

 </ehcache>
```

## mybatis作业

非常感谢这位同学写的作业

https://github.com/ljingen/kuangstudy.git

```
#1 //通过UserCode获取User
public User getLoginUser(@Param("userCode") String userCode) throws Excepti
```

碰到的错误:



### 练习3 

```java
public List<User> getUserList(@Param("userName") String userName,
                              @Param("useRole") Integer useRole,
                              @Param("from") Integer currentPageNo,
                              @Param("pageSize") Integer pageSize) throws Exception;
                              
    <select id="getUserList" resultType="user">
        <!--select * from smbms_user where userName=userName and useRole= useRole limit currentPageNo=currentPageNo and pageSize=pageSize-->
        select * from smbms_user
        <where>
            <if test="userName!=null">
                userName = #{userName}
            </if>
            <if test="useRole!=null">
                and userRole= #{useRole}
            </if>
        </where>
        limit
        <if test="from!=null">
           #{from}
         </if>
        <if test="pageSize!=null">
           , #{pageSize}
        </if>
    </select>                              
                              
# 碰到的错误
1、参数使用了@param，但是我在测试脚本使用map，导致提醒参数数量不一致，从而得到结论： @Param 需要直接传递给Mapper.xml，接口定义的不是Map，就不能用map
2、useRole这个参数，在数据库里面名字是userRole,但是参数定义为useRole， 需要在Mapper.xml里面  结论：@Param的名称和Mapper的要对应
3、传递的是4个参数，但是分页要用limit，并且分页的from和pageSize中间有个 逗号，记住得加上。
4、接口的形参名称，不影响测试方法和Mapper配置文件的名字，形参可以任意写，但是@Param的名称是传递到Mapper配置文件的
5、parameterType 这个是可加可不加，但遇到复杂类型，是需要加，不加就没法获取到对象或者map的属性
```

### 练习4

```
//通过条件查询-用户记录数
 public int getUserCount(@Param("userName") String userName,@Param("useRole") Integer useRole) throws Exception;
    
   <select id="getUserCount" resultType="int">

        select count(id) from smbms_user
        <where>
            <if test="userName!=null">
                userName =#{userName}
            </if>
            <if test="useRole!=null">
                and userRole =#{useRole}
            </if>
        </where>
    </select>

# 碰到的错误，
1、 我在上一个练习3，写了一个parameterType="" 空的值，在练习三的参数类型中，然后执行练习4，出现了错误日志： Could not resolve type alias ''.  Cause: java.lang.ClassNotFoundException: Cannot find class: 
   以后遇到类似这种无法解析 '' 可能就是参数填写空值了!
2、返回用户的年龄，因为birthday在数据库为空值，导致出现了错误，所以后续数据库数据，得校验一下是否是空
3、resultType="int" 这个在select语句是必填项，ExecutorException: A query was run and no Result Maps were found for the Mapped Statement 'com.kuang.dao.user.UserMapper.getUserCount'.  It's likely that neither a Result Type
```

### 练习5 

```java
//通过userId删除user
public int deleteUserById(@Param("id") Integer id) throws Exception;

<delete id="deleteUserById">
   delete from smbms_user where id =#{id}
</delete>
    
碰到错误：
    在select标签，写删除语句，会出现这个错误：Mapper method 'com.kuang.dao.user.UserMapper.deleteUserById attempted to return null from a method with a primitive return type (int).



Mapper method 'com.kuang.dao.user.UserMapper.deleteUserById attempted to return null from a method with a primitive return type (int).
```

### 练习6

```java
//通过userId获取user
public User getUserById(@Param("id") Integer id) throws Exception;


    <!--获取用户列表-->
    <select id="getUserById" resultMap="userMap">
        select u.*,r.roleName rname
        from smbms_user u,smbms_role r
        where  u.id = #{id} and u.userRole=r.id
    </select>
    <resultMap id="userMap" type="user">
        <result property="userRoleName" column="rname"/>
    </resultMap>
        
碰到的错误:
1、这里面 userRoleName这个字段，在User实体类，定义的是private String userRoleName, 这个值在Role实体中可以查询到，我以为应该使用关联，一开始我使用了
    <resultMap id="userMap" type="user">
        <association property="userRoleName" javaType="role">
            <result property="roleName" column="rname"/>
        </association>
    </resultMap>
这个是错误的，因为在User实体类，userRoleName并不是一个对象，只是一个基础数据类型，所以应该用下面形式：
     <resultMap id="userMap" type="user">
        <result property="userRoleName" column="rname"/>
    </resultMap>
```

### 练习7 

```java
//修改用户信息
public int modify(User user) throws Exception;

    <!--修改用户信息-->
    <update id="modify" parameterType="user">
        update smbms_user
        <set>
            <if test="userCode != null">userCode=#{userCode},</if>
            <if test="userName != null">userName=#{userName},</if>
            <if test="userPassword != null">userPassword=#{userPassword},</if>
            <if test="gender != null">gender=#{gender},</if>
            <if test="birthday != null">birthday=#{birthday},</if>
            <if test="phone != null">phone=#{phone},</if>
            <if test="address != null">address=#{address},</if>
            <if test="userRole!= null">userRole=#{userRole},</if>
            <if test="createdBy!= null">createdBy=#{createdBy},</if>
            <if test="creationDate != null">creationDate=#{creationDate},</if>
            <if test="modifyBy != modifyBy">modifyBy=#{modifyBy},</if>
            <if test="modifyDate != null">modifyDate=#{modifyDate}</if>
        </set>
        where id=#{id};
    </update>
        
碰到的错误:
1、 <if test="gender != null">gender=#{gender},</if>  少了一个逗号，导致系统插入失败，给出的报错信息
    You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'modifyDate='2020-12-16 14:09:28.322'
```

### 练习8

```java
//修改当前用户的密码
public int modifyPwd(@Param("id") Integer id, @Param("userPassword") String pwd) throws Exception;

<update id="modifyPwd">
        update smbms_user
        set userPassword=#{userPassword}
</update>
    
    
```

### 练习9

```java
//获取角色列表
 public List<Role> getRoleList() throws Exception;

 <select id="getRoleList" resultType="role">
    select * from smbms_role;
</select>
```

### 练习10

```
    //增加角色信息
    public int add(Role role) throws Exception
    
        <insert id="add" parameterType="role">
        insert into smbms_role
         (roleCode,roleName,createdBy,creationDate)
         values (#{roleCode},#{roleName},#{createdBy},#{creationDate});
    </insert>
```

### 练习11

````java
 //通过Id删除role
 public int deleteRoleById(@Param("Id") Integer delId) throws Exception;

    <!--通过Id删除role-->
    <delete id="deleteRoleById" parameterType="int">
        delete from smbms_role where id =${Id}
    </delete>
````

### 练习12 

```java
   //修改角色信息
    public int modify(Role role) throws Exception;


    <update id="modify" parameterType="role">
        update smbms_role
        <set>
            <if test="roleCode!=null">roleCode =#{roleCode},</if>
            <if test="roleName!=null">roleName =#{roleName},</if>
            <if test="createdBy!=null">createdBy =#{createdBy},</if>
            <if test="creationDate!=null">creationDate =#{creationDate},</if>
            <if test="modifyBy!=null">modifyBy =#{modifyBy},</if>
            <if test="modifyDate!=null">modifyDate =#{modifyDate}</if>
        </set>
        where id=#{id};
    </update>
        
碰到的错误:
1、在测试使用的时候，设置了role，但是role 的id未设置，导致修改失败，但是系统未报错
    
```

### 练习13

```java
//通过id获取role
 public Role getRoleById(@Param("id") Integer id) throws Exception;

    <!--通过id获取role-->
    <select id="getRoleById" parameterType="int" resultType="role">
        select * from smbms_role where id = #{id};
    </select>
```

### 练习14

```java
    //根据roleCode,进行角色编码的唯一性校验
    public int roleCodeIsExist(@Param("roleCode") String roleCode) throws Exception;

    
    <select id="roleCodeIsExist" parameterType="string" resultType="int">
        select id from smbms_role where roleCode=#{roleCode};
    </select>

碰到的错误:
1、resultType 填写int默认返回的是当前记录的id
2、Mapper method 'com.kuang.dao.role.RoleMapper.roleCodeIsExist attempted to return null from a method with a primitive return type (int).
    这是因为id可能为空，解决办法
       <select id="roleCodeIsExist" parameterType="string" resultType="int">
        select coalesce(max(id),0) as id from smbms_role where roleCode=#{roleCode};
    </select>
```

### 练习15 

```
    //增加用户信息
    public int add(Provider provider) throws Exception;
    
        <insert id="add" parameterType="provider">
        insert into smbms_provider
        (proCode,proName,proDesc,proContact,proPhone,proAddress,proFax,createdBy,creationDate)
        values (#{proCode},#{proName},#{proDesc},#{proContact},#{proPhone},#{proAddress},#{proFax},#{createdBy},#{creationDate});
    </insert>
```

### 练习16 

```java
//通过条件查询-providerList
public List<Provider> getProviderList(@Param("proName") String proName,@Param("proCode") String proCode,
                                          @Param("from") Integer currentPageNo,@Param("pageSize") Integer pageSize) throws Exception;

    <select id="getProviderList" resultType="provider">
        select * from smbms_provider
        <where>
            <if test="proCode!=null">proCode=#{proCode}</if>
            <if test="proName!=null">and proName like "%"#{proName}"%"</if>
        </where>
        limit
        <if test="from!=null">#{from}</if>
        <if test="pageSize!=null">,#{pageSize}</if>
    </select> 
```

### 练习17

```
   //获取供应商列表
    public List<Provider> getProList() throws Exception;
    
        <select id="getProList" resultType="provider">
        select * from smbms_provider;
    </select>
```



### 练习18

```java
    //通过条件查询-供应商表记录数
    public int getProviderCount(@Param("proName") String proName,@Param("proCode") String proCode) throws Exception
        
        
    <select id="getProviderCount" resultType="int">
        select count(id) from smbms_provider
        <where>
            <if test="proName!=null">
                proName =#{proName}
            </if>
            <if test="proCode!=null">
                and proCode =#{proCode}
            </if>
        </where>
    </select> 
```

### 练习19

```java
    //通过供应商id供应商信息
    public Provider getProviderById(@Param("id") Integer id) throws Exception;


    <!--通过供应商id供应商信息-->
    <select id="getProviderById" resultType="provider">
        select * from smbms_provider where id  =#{id}
    </select>
```

### 练习20

```java
   //修改供应商
    public int modify(Provider provider) throws Exception;


    <update id="modify" parameterType="provider" >
        update smbms_provider
        <set>
            <if test="proCode!=null"> proCode =#{proCode},</if>
            <if test="proName!=null">proName =#{proName},</if>
            <if test="proDesc!=null">proDesc =#{proDesc},</if>
            <if test="proContact!=null">proContact =#{proContact},</if>
            <if test="proPhone!=null">proPhone =#{proPhone},</if>
            <if test="proAddress!=null">proAddress =#{proAddress},</if>
            <if test="proFax!=null">proFax =#{proFax},</if>
            <if test="modifyBy!=null"> modifyBy=#{modifyBy},</if>
            <if test="modifyDate!=null">modifyDate =#{modifyDate}</if>
        </set>
        where id =#{id};
    </update>
```

### 练习21 根据供应商id查询订单量

```java
    //根据供应商id查询订单量
    public int getBillCountByProviderId(@Param("providerId") Integer providerId) throws Exception;

    <!--根据供应商id查询订单量-->
    <select id="getBillCountByProviderId" resultType="int">
        select count(id) from smbms_bill where providerId=#{providerId};
    </select>

```

### 练习22 增加订单

```java
    //增加订单
    public int add(Bill bill) throws Exception;

    <insert id="add" parameterType="bill">
        insert into smbms_bill
        (billCode,productName,productDesc,productUnit,productCount,totalPrice,isPayment,createdBy,creationDate,providerId)
         values (#{billCode},#{productName},#{productDesc},#{productUnit},#{productCount},#{totalPrice},#{isPayment},
         #{createdBy},#{creationDate},#{providerId});
    </insert>

```

### 练习23 通过查询条件后去供应商列表 getBillList

```java
    public List<Bill> getBillList(@Param("productName") String productName, @Param("providerId") Integer providerId,
                                  @Param("ispay") Integer ispay, @Param("from") Integer currentPageNo, @Param("pageSize") Integer pageSize) throws Exception;


    <!--通过查询条件后去供应商列表 getBillList-->
    <select id="getBillList" resultType="bill">
       select * from smbms_bill
       <where>
           <if test="productName!=null">productName=#{productName}</if>
           <if test="providerId!=null">and providerId=#{providerId}</if>
           <if test="ispay!=null">and isPayment=#{ispay}</if>
       </where>
           limit
            <if test="from!=null">#{from}</if>
            <if test="pageSize!=null">,#{pageSize}</if>
    </select>

```

### 练习24 通过条件查询-订单表记录数

```java
    //通过条件查询-订单表记录数
    public int getBillCount(@Param("productName") String productName,@Param("providerId") Integer providerId, @Param("ispay") Integer ispay)throws Exception;


```

### 练习25 通过delId删除Bill

```java
    //通过delId删除Bill
    public int deleteBillById(@Param("id") Integer delId) throws Exception;

    <!--通过delId删除Bill-->
    <delete id="deleteBillById">
        delete from smbms_bill where id =#{id};
    </delete>

```

### 练习26 通过billId获取Bill

```java
    //通过billId获取Bill
    public int getBillById(@Param("id") Integer delId) throws Exception;

    <!--    //通过billId获取Bill-->
    <select id="getBillById" parameterType="int" resultType="bill">
        select * from smbms_bill where id = #{id}
    </select>

```

### 练习27 修改订单信息

```java
    //修改订单信息
    public int modify(Bill bill) throws Exception;

    <!--修改订单信息-->
    <update id="modify" parameterType="bill" >
        update smbms_bill
        <set>
            <if test="billCode!=null"> billCode =#{billCode},</if>
            <if test="productName!=null">productName =#{productName},</if>
            <if test="productDesc!=null">productDesc =#{productDesc},</if>
            <if test="productUnit!=null">productUnit =#{productUnit},</if>
            <if test="productCount!=null">productCount =#{productCount},</if>
            <if test="totalPrice!=null">totalPrice =#{totalPrice},</if>
            <if test="isPayment!=null">isPayment =#{isPayment},</if>
            <if test="providerId!=null">providerId =#{providerId},</if>
            <if test="modifyBy!=null"> modifyBy=#{modifyBy},</if>
            <if test="modifyDate!=null">modifyDate =#{modifyDate}</if>
        </set>
        where id =#{id};
    </update>

```

### 练习28 根据供应商Id删除订单信息

```java
    //根据供应商Id删除订单信息
    public int deleteBillByProviderId(@Param("providerId") Integer providerId) throws Exception;
    
<delete id="deleteBillByProviderId">
        delete from smbms_bill where providerId=#{providerId};
    </delete>

```







# Spring

## 简介

### 1.1 spring历史

Spring 春天---给软件行业带来了春天!

2002年，首次推出了Spring框架的雏形 interface21

Spring框架是以interface21框架为基础，经过重新设计，并不断丰富其内涵，与2004年3月24日，发布1.0

Rod Johnson  SpringFramework的创始人!

目的：解决企业开发的复杂性， 使现有的技术更加容易使用! 本身是一个大杂烩，整合了现有的技术框架!



SSH  Struct2+Spring+Hibernate

SSM  SpringMVC+Spring+ Mybatis

官网地址：https://spring.io/projects/spring-framework

官方下载地址：https://repo.spring.io/release/org/springframework/spring/

 GitHub地址：https://github.com/spring-projects/spring-framework

maven的下载地址

```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.0.RELEASE</version>
</dependency>


<!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.2.0.RELEASE</version>
</dependency>


```

### 1.2 优点

spring是一个开源的免费的框架(容器)，他是一个轻量级的非入侵式的框架!

控制反转(IOC)  什么是控制反转？ 面试必问

面向切面编程(AOP)  什么是面向切面编程? 面试必问

支持事务的处理，对框架整合的支持!



总结一句话：SPring是一个轻量级的控制反转(IOC)和面向切面编程(AOP）的框架!

### 1.3 组成 

![image-20201217094947259](img/image-20201217094947259.png)

### 1.4 拓展

Spring Boot 构建一切

Spring Cloud  协调一切

SpringCloud Data Flow 连接一切





Spring Boot:  一个快速开发的脚手架  基于SpringBoot可以快速的开发单个微服务

Spring Cloud : 基于SpringBoot实现的, 对微服务的整合和协调

因为现在大多数公司，都在使用Spring Boot在进行快速开发! 学习SpringBoot的前提，需要完全掌握Spring及SpringMVC

Spring 和SpringMVC 起到承上启下作用!

弊端：发展了太久之后，违背了原来的理念! 配置十分的繁琐! 人称 "配置地狱!" 直到SpringBoot能得到部分解放! 



## IOC理论的推导

### 2.1 一个ioc原型例子

#### 原来写一个业务

​	UserDao接口

```java
public interface UserDao {
    void getUser();
}
```



​	UserDaoImpl实现类

```java
//UserDaoImpl
public class UserDaoImpl implements UserDao {
    public void getUser() {
        System.out.println("userDaoImpl被调用了!");
    }
}

//MysqlUserDaoImpl
public class MysqlUserDaoImpl implements UserDao {
    public void getUser() {
        System.out.println("mysql userDaoImpl被调用了!");
    }
}
//OrcaleUserDaoImpl
public class OrcaleUserDaoImpl implements UserDao {
    public void getUser() {
        System.out.println("Orcale userDaoImpl被调用了!");
    }
}

```



UserService业务接口

```java
public interface UserService {
    void getUser();
}
```



UserServiceImpl业务实现类

```java 
public class UserServiceImpl implements UserService {

    private UserDao userDao = new UserDaoImpl();
    
    public void getUser() {
        userDao.getUser();
    }
}

```

Test测试方法:

```java
@Test
public void testDao(){
    UserServiceImpl userService = new UserServiceImpl();
    userService.getUser();
}
```

**由此产生一个问题, 在我们业务中，用户的需求可能会影响我们原来的代码，例如，上述例子，我们做完了UserDaoImpl，UserDao 又增加多个类实现了他的接口，但是接下来要求做 MysqlUserDaoImpl的拓展，就需要我们重新修改源码.**



我们需要根据用户的需求去修改源代码，如果程序代码量十分大，修改一次的代价非常大! 

#### IOC

所以，我们在UserService里面做一个setter注入，实现动态的接口注入，这样已经发生了革命性的变化!

```java
public class UserServiceImpl implements UserService{
    ...
    private UserDao userDao;
    //利用set进行动态实现值的注入!
    public void setUserDao(Userdao userDao){
        this.userDao = userDao;
    }
    ...
}
```

之前程序时主动创建对象，控制权在程序员手上! 所以程序每次改动都需要程序员改动代码!

使用了set注入后，程序不在具有主动性，而是变成了被动的接收对象!

我们去使用的时候，就可以在测试里面如下方式实现, 我们如果需要切换不同的UserDao接口实现，只需要在setUserDao()接口设置一下就可以了,如下面在测试类中:

```java
@Test
public void testDao(){
    UserServiceImpl userService = new UserServiceImpl();
    userService.setUserDao(new MysqlUserDaoImpl());
    userService.getUser();
}
```



**这样，当我们比如想扩展一个pgsql实现UserDao, 就只需要实现一个叫做PgsqlUserDaoImpl的类，其他在Service实现类就不需要做任何改变，在测试方法中，直接New PgsqlUserDaoImpl()即可**

这种思想，从本质上解决了问题，我们程序员不用再去管理对象的创建了! 系统的耦合性大大的降低了! 



让我们可以更加专注的在业务的实现上!

上述的例子是一个IOC的简单原型!

### 2.2 ioc的本质

控制反转IoC(Inversion of Control ) 是一种设计思想，DI(依赖注入) 是实现IoC的一种方法，也有人认为DI只是IoC的另一种叫法，没有Ioc的程序中，我们使用面向对象编程，对象的创建和对象间的依赖关系完全硬编码在程序中，程序的创建由程序员自己控制，控制反转后将对象的创建转移给第三方，

所谓控制反转，是指获取对象的方式反转了，由原来用户自己控制自己需要什么对象，控制对象的生成，程序主动生成对象 转换为 由第三方控制对象的生成，用户自己被动接收!

采用xml方式配置Bean的时候，Bean的定义信息和实现分离的，而采用注解的方式可以把两者合为一体，Bean的定义信息直接以注解的形式定义在实现类中，从而达到了零配置的目的!

控制反转(IoC)是一种通过描述(XML或者注解) 并通过第三方去生产或获取特定对象的方式。在Spring中实现控制反转的是IoC容器，其实现方式是依赖注入(Dependency inJection DI)



#### 控制反转

控制反转(IOC)到底为什么要起这么个名字？我们来对比一下：

  软件系统在没有引入IOC容器之前，如图1所示，对象A依赖于对象B，那么对象A在初始化或者运行到某一点的时候，自己必须主动去创建对象B或者使用已经创建的对象B。无论是创建还是使用对象B，控制权都在自己手上。

  软件系统在引入IOC容器之后，这种情形就完全改变了，如图3所示，由于IOC容器的加入，对象A与对象B之间失去了直接联系，所以，当对象A运行到需要对象B的时候，IOC容器会主动创建一个对象B注入到对象A需要的地方。

  通过前后的对比，我们不难看出来：对象A获得依赖对象B的过程,由主动行为变为了被动行为，控制权颠倒过来了，这就是“控制反转”这个名称的由来。

#### 依赖注入

2004年，Martin Fowler探讨了同一个问题，既然IOC是控制反转，那么到底是“哪些方面的控制被反转了呢？”，经过详细地分析和论证后，他得出了答案：“获得依赖对象的过程被反转了”。控制被反转之后，获得依赖对象的过程由自身管理变为了由IOC容器主动注入。于是，他给“控制反转”取了一个更合适的名字叫做“依赖注入（Dependency Injection）”。他的这个答案，实际上给出了实现IOC的方法：注入。所谓依赖注入，就是由IOC容器在运行期间，动态地将某种依赖关系注入到对象之中。

　　所以，依赖注入(DI)和控制反转(IOC)是从不同的角度的描述的同一件事情，就是指通过引入IOC容器，利用依赖关系注入的方式，实现对象之间的解耦。

#### 在spring里ioc的用处

对象由spring创建、管理、装配

#### 缺点

使用IOC框架产品能够给我们的开发过程带来很大的好处，但是也要充分认识引入IOC框架的缺点，做到心中有数，杜绝滥用框架[1]。

  第一、软件系统中由于引入了第三方IOC容器，生成对象的步骤变得有些复杂，本来是两者之间的事情，又凭空多出一道手续，所以，我们在刚开始使用IOC框架的时候，会感觉系统变得不太直观。所以，引入了一个全新的框架，就会增加团队成员学习和认识的培训成本，并且在以后的运行维护中，还得让新加入者具备同样的知识体系。

  第二、由于IOC容器生成对象是通过反射方式，在运行效率上有一定的损耗。如果你要追求运行效率的话，就必须对此进行权衡。

  第三、具体到IOC框架产品(比如：Spring)来讲，需要进行大量的配制工作，比较繁琐，对于一些小的项目而言，客观上也可能加大一些工作成本。

  第四、IOC框架产品本身的成熟度需要进行评估，如果引入一个不成熟的IOC框架产品，那么会影响到整个项目，所以这也是一个隐性的风险。

  我们大体可以得出这样的结论：一些工作量不大的项目或者产品，不太适合使用IOC框架产品。另外，如果团队成员的知识能力欠缺，对于IOC框架产品缺乏深入的理解，也不要贸然引入。最后，特别强调运行效率的项目或者产品，也不太适合引入IOC框架产品，像WEB2.0网站就是这种情况。

## Hello Spring



### 3.1 一个例子

准备：创建一个新的maven项目，并导入spring-webmvc的包，对应pom.xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>spring-study</artifactId>
    <packaging>pom</packaging>
    <version>1.0-SNAPSHOT</version>
    <modules>
        <module>spring-01-ioc1</module>
        <module>spring-02-hello</module>
        <module>spring-03-ioc2</module>
        <module>spring-04-di</module>
        <module>spring-05-autowired</module>
        <module>spring-06-anno</module>
        <module>spring-07-appconfig</module>
    </modules>

    <dependencies>
        <!--SpringFramework5-->
        <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.2.0.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.2.0.RELEASE</version>
        </dependency>
    </dependencies>

</project>
```



首先，我们设计自己的pojo实体类, 记住一定要有setStr（）方法

```java
public class Hello {
    private String str;

    public String getStr() {
        return str;
    }

    public void setStr(String str) {
        this.str = str;
    }
}
```

然后,我们在resources目录下，创建一个applicationContext.xml的spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="hello" class="com.kuang.pojo.Hello">
        <!-- collaborators and configuration for this bean go here -->
        <property name="str" value="我是使用了spring赋值的!"/>
    </bean>

</beans>
```

最后，让我们来测试一下这个创建方式

```java
public class MyTest {
    public static void main(String[] args) {
        //控制 由谁来控制对象的创建，传统的应用程序的程序创建由程序控制，而spring由spring控制对象创建 ，反转就是由程序创建对象变为被动接收对象
        ApplicationContext context = new ClassPathXmlApplicationContext("ApplicationContext.xml");
        Hello hello = (Hello) context.getBean("hello");
        System.out.println(hello.getStr());
    }
}
```



通过上面例子，请问 Hello 这个对象是谁创建的？Hello对象的属性是如何进行设置的？

> 通过学习我们找到，Hello已经被托管给Spring进行创建了，通过配置bean创建了我们的Hello类的对象，并通过 <property name="str" value="我是使用了spring赋值的!"/> 对Hello的属性进行赋值!



这个过程就叫做控制反转

控制：指的是由谁来控制对象的创建。传统应用程序的对象由程序本身控制创建的，使用spring后对象是由Spring来创建的

反转：指的是 程序本身不创建对象，而变成被动的接收对象

依赖注入： 就是利用set方法来进行注入的

Ioc是一种编程思想，由主动的编程变为被动的接收

可以搞过 new ClassPathXmlApplicationContext("bean.xml")去浏览一下底层的源代码。

OK 到了现在，我们就彻底不用在程序中改动了，要实现不同的操作哦，只需要在xml配置文件中进行修改，所谓的Ioc，一句话搞定：

对象由spring来创建、管理、装配!

`我自己的一个小结`

控制反转: 主要就是原来写程序是由程序控制对象的创建，而使用控制反转的思想，是对象的创建并不是由使用者创建，而是由第三方创建，而使用者变成被动接收对象即可。 

控制反转的实现方式 ：  方式1、DI 依赖注射



**没用控制反转**,比如我们当前有一个Dao层接口，实现连接数据库并读取用户，然后service层包含了dao层的接口，并调用dao层读取用户的方法，而使用层，直接创建service层实现类并调用service层的方法；如idea中spring-01-ioc1示例

private UserDao = new UserDaoImpl()

**但是**，随着系统的演进，Dao层需要进行平行拓展，除了支持原来默认的Dao实现，还有mysqlDao实现类，还有OracleDao类的实现，如果还是原来那样在service包含dao层接口，则每次都需要改动大量代码，代价高昂, 人们提出了在Service层动态进行设置具体Dao的实现类，从而实现节省成本，谁用谁来指定

UserServiceImpl

```java
public UserServiceImpl implements UserService{
    ..........
    prinvate UserDao userDao;
    publict void setUserDao(UserDao userDao){
        this.userDao = userDao
    }
    ......
    }
```

Client使用层

```java
public static void main(String [] args){
    UserService userSer = new UserServiceImpl();
    //*************下面这行是重点
    userSer.setUserDao(new OracleUserDaoImpl());
   	//********************
    userSer.getUser();  
}
这样如果换成其他的数据库，很容易更换，如换成Mysql
public static void main(String [] args){
    UserService userSer = new UserServiceImpl();
    //*************下面这行是重点
    userSer.setUserDao(new MysqlUserDaoImpl());
    //********************
    userSer.getUser();  
}
```

**而有了spring**，在上面的过程更加简化，只需要写完实现类，进行配置，然后调用即可

ApplicationContext.xml

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="userDaoImpl" class="com.kuang.dao.UserDaoImpl">
        <!-- collaborators and configuration for this bean go here -->
    </bean>
    <bean id="mysqlDaoImpl" class="com.kuang.dao.MysqlUserDaoImpl">
        <!-- collaborators and configuration for this bean go here -->
    </bean>
    <bean id="oracleDaoImpl" class="com.kuang.dao.OrcaleUserDaoImpl">
        <!-- collaborators and configuration for this bean go here -->
    </bean>

    <bean id="userServiceImpl" class="com.kuang.service.UserServiceImpl">
        <!-- collaborators and configuration for this bean go here -->
        <property name="userDao" ref="mysqlDaoImpl"/>
    </bean>

</beans>
```



client 使用类

```java
    public static void main(String[] args) {
        //用户实际调用的是业务层。dao层他们不需要接触
//        UserServiceImpl userService = new UserServiceImpl();
//        userService.setUserDao(new UserDaoImpl());
//        userService.getUser();
        ApplicationContext context = new ClassPathXmlApplicationContext("ApplicationContext.xml");
        UserServiceImpl userService = (UserServiceImpl) context.getBean("userServiceImpl");
        userService.getUser();

    }
```

**现在，如果要进行更换对应的数据库，我们只需要在ApplicationContext.xml里面，把userServiceImpl的ref换一下，其他任何地方都不改动，就可以解决问题了!**

### 3.2 基于构造器的依赖注入

1、默认使用无参构造创建对象  默认!

2、加入我们使用有参构造对象，可以有多种方式，分别如下：

实例的pojo实体类

```java
public class User {

    private String name;

    public User(String name) {
        System.out.println("User的无参构造!");
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void show(){
        System.out.println("name="+name);
    }
}
```



方式1：按照下标赋值（index从0开始，下面例子报错）

```xml
<bean id="user" class="com.kuang.pojo.User">
        <!-- collaborators and configuration for this bean go here -->
        <constructor-arg index="1" value="秦僵"/>
        <property name="name" value="秦僵"/>
</bean>
```

方式2：按照参数类型匹配（不建议使用）

```xml
    <bean id="user" class="com.kuang.pojo.User">
        <!-- collaborators and configuration for this bean go here -->
        <constructor-arg type="java.lang.String" value="秦僵"/>

        <property name="name" value="秦僵"/>
    </bean>

这个例子： 构造器是传递的String类型
如果两个参数都是String 就没法匹配了，不建议使用
```

方式3：直接通过引用构造器的参数名

```xml
    <bean id="user" class="com.kuang.pojo.User">
        <!-- collaborators and configuration for this bean go here -->
<!--        <constructor-arg ref="java.lang.String"/>-->
        <constructor-arg name="name" value="秦僵/"/>
        <property name="name" value="秦僵"/>
    </bean>
```



一个官网的例子，

首先我们的pojo类如下：

```java
package x.y;
public class Foo {

	public Foo(Bar bar, Baz baz) {
		// ...
	}
}
```

我们可以在spring.xml里面配置如下

```xml
<beans>
	<bean id="foo" class="x.y.Foo">
		<constructor-arg ref="bar"/>
		<constructor-arg ref="baz"/>
	</bean>
    
	<bean id="bar" class="x.y.Bar"/>
	<bean id="baz" class="x.y.Baz"/>
</beans>
```

另一个例子

```java
//对应的pojo对象
package examples;

public class ExampleBean {

	// Number of years to calculate the Ultimate Answer
	private int years;

	// The Answer to Life, the Universe, and Everything
	private String ultimateAnswer;

	public ExampleBean(int years, String ultimateAnswer) {
		this.years = years;
		this.ultimateAnswer = ultimateAnswer;
	}

}

#####//使用类型匹配模式
<bean id="exampleBean" class="examples.ExampleBean">
	<constructor-arg type="int" value="7500000"/>
	<constructor-arg type="java.lang.String" value="42"/>
</bean>
#####//还可以使用index属性进行注入
<bean id="exampleBean" class="examples.ExampleBean">
	<constructor-arg index="0" value="7500000"/>
	<constructor-arg index="1" value="42"/>
</bean>
#####//还可以使用构造器的参数名称
<bean id="exampleBean" class="examples.ExampleBean">
	<constructor-arg name="years" value="7500000"/>
	<constructor-arg name="ultimateAnswer" value="42"/>
</bean>
```

总结：在配置文件加载的时候，容器中管理的对象就已经初始化了!

## spring的配置文件

### 4.1 alias别名

```xml
    <bean id="user" class="com.kuang.pojo.User">
        <!-- collaborators and configuration for this bean go here -->
		<!--<constructor-arg ref="java.lang.String"/>-->
        <constructor-arg name="name" value="秦僵/"/>
        <property name="name" value="秦僵"/>
    </bean>   

<alias name="user" alias="user2123123"/>  将user配置为别名 user2123123
```

注意：别名区分大小写 一般用在类名特别长的地方

### 4.2 bean配置

id 代表要new出来的对象名字， bean的唯一标识符，也就是相当于我们学过的变量名 ，对象名

class bean对象所对应的全限定类名(包名+类名)

name: 也是别名，而且name更高级，可以同时取多个别名

### 4.3 import 

一般用于团队开发使用，可以将多个配置文件导入合并为一个

```xml
<import resource="bean.xml"/>
<import resource="bean1.xml"/>
```

## 依赖注入DI

依赖注入三种方式

### 5.1 构造器注入

https://docs.spring.io/spring-framework/docs/5.2.12.RELEASE/spring-framework-reference/core.html#beans-factory-collaborators

测试的构造器注入的类：

```java
package examples;

public class ExampleBean {

    // Number of years to calculate the Ultimate Answer
    private int years;

    // The Answer to Life, the Universe, and Everything
    private String ultimateAnswer;

    public ExampleBean(int years, String ultimateAnswer) {
        this.years = years;
        this.ultimateAnswer = ultimateAnswer;
    }
}
```

方式一：采用参数类型匹配的方式

```xml
<bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg type="int" value="7500000"/>
    <constructor-arg type="java.lang.String" value="42"/>
</bean>
```

方式二：采用构造器参数索引的方式

```xml
<bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg index="0" value="7500000"/>
    <constructor-arg index="1" value="42"/>
</bean>
```

方式三：采用构造器参数名字的方式

```xml
<bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg name="years" value="7500000"/>
    <constructor-arg name="ultimateAnswer" value="42"/>
</bean>
```









### 5.2 set方式注入[重点]

https://docs.spring.io/spring-framework/docs/5.2.12.RELEASE/spring-framework-reference/core.html#beans-setter-injection

- 依赖注入
  - 依赖  bean对象的创建依赖于容器
  - 注入  bean对象中的所有属性，由容器来注入

测试环境搭建

1、复杂类型

```java
public class Address {
    private String address;

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }
}
```



2、真实测试对象

```java
public class Student {
    private String name;
    private Address address;
    private String [] books;
    private List<String> hobbys;
    private Map<String,String> card;
    private Set<String> games;
    private Properties info;
    private String wife; //是否有妻子
}
```

3、测试配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--pojo address-->
    <bean id="address" class="com.kuang.pojo.Address">
        <property name="address" value="北京海淀福缘门社区"/>
    </bean>
    <!--pojo student-->
    <bean id="student" class="com.kuang.pojo.Student">
        <!--第一种 普通值注入-->
        <property name="name" value="秦僵"/>
        <!--第二种 Bean注入-->
        <property name="address" ref="address"/>
        <!--第三种 数组注入-->
        <!-- results in a setSome Array call -->
        <property name="books">
            <array>
                <value>Django编程大法</value>
                <value>Python编程大法</value>
                <value>Java编程大法</value>
            </array>
        </property>
        <!--第四种 List注入-->
        <!-- results in a setSomeList(java.util.List) call -->
        <property name="hobbys">
            <list>
                <value>玩游戏</value>
                <value>跳舞</value>
                <value>看电影</value>
            </list>
        </property>
        <!--第五种 map注入-->
        <!-- results in a setSomeMap(java.util.Map) call -->
        <property name="card">
            <map>
                <entry key="key" value="12312312312321312312"/>
                <entry key ="address" value="安阿斯加德焚枯食淡金风科技撒附件"/>
            </map>
        </property>
        <!--第六种 set注入-->
        <property name="games">
            <set>
                <value>LoL</value>
                <value>ROB</value>
                <value>COF</value>
            </set>
        </property>
        <!--第七种 null注入-->
        <property name="wife">
            <null/>
        </property>
        <!--第八种 property注入-->
        <!-- the merge is specified on the child collection definition -->
        <property name="info">
            <props>
                <prop key="sales">sales@example.com</prop>
                <prop key="support">support@example.co.uk</prop>
            </props>
        </property>
    </bean>
</beans>
```



### 5.3 拓展方式注入

https://docs.spring.io/spring-framework/docs/5.2.12.RELEASE/spring-framework-reference/core.html#beans-dependency-resolution

我们可以用是P命令空间和C命令空间

官网: P命名空间的意思是，可以引入 下面的约束，则后续bean里面的名字就可以直接使用p:argument来代替!

```xml
xmlns:p="http://www.springframework.org/schema/p"
```

使用

```java
public class Person {
    private String name;
    private Person spouse;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }



    public Person getSpouse() {
        return spouse;
    }

    public void setSpouse(Person spouse) {
        this.spouse = spouse;
    }
    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", spouse=" + spouse +
                '}';
    }
}
```

测试

```xml
    <bean name="jane" class="com.kuang.pojo.Person">
        <property name="name" value="Jane Doe"/>
    </bean>

    <bean name="john-classic" class="com.kuang.pojo.Person">
        <property name="name" value="John Doe"/>
        <property name="spouse" ref="jane"/>
    </bean>

    <bean name="john-modern"
          class="com.kuang.pojo.Person"
          p:name="John Doe"
          p:spouse-ref="jane"/>
```





注意点：

1、P命名和C命令空间，不能直接使用，需要导入xml约束



### 5.4 注入的例子





### 5.5 官网的例子

https://docs.spring.io/spring-framework/docs/5.2.12.RELEASE/spring-framework-reference/core.html#beans-factory-properties-detailed

```xml
<bean id="exampleBean" class="examples.ExampleBean">
    <!-- setter injection using the nested ref element -->
    <property name="beanOne"> 
        <ref bean="anotherExampleBean"/>
    </property>

    <!-- setter injection using the neater ref attribute -->
    <property name="beanTwo" ref="yetAnotherBean"/>
    <property name="integerProperty" value="1"/>
</bean>

<bean id="anotherExampleBean" class="examples.AnotherBean"/>
<bean id="yetAnotherBean" class="examples.YetAnotherBean"/>
```



对应的ExampleBean类

```java
public class ExampleBean {

    private AnotherBean beanOne;

    private YetAnotherBean beanTwo;

    private int i;

    public void setBeanOne(AnotherBean beanOne) {
        this.beanOne = beanOne;
    }

    public void setBeanTwo(YetAnotherBean beanTwo) {
        this.beanTwo = beanTwo;
    }

    public void setIntegerProperty(int i) {
        this.i = i;
    }
}
```





### 5.6 bean的作用域 Bean Scope



1.单例模式(singleton) SPring默认机制,  Singleton Scope   表示只要使用同一个bean，那么只有那么一个对象

```java
<bean name="john-classic" class="com.kuang.pojo.Person">
    <property name="name" value="John Doe"/>
    <property name="spouse" ref="jane"/>
</bean>

@Test
public void singletonScope(){
    ApplicationContext context = new ClassPathXmlApplicationContext("bean.xml");
    Person bean = context.getBean("john-classic", Person.class);
    Person bean2 = context.getBean("john-classic", Person.class);

    System.out.println(bean.hashCode());
    System.out.println(bean2.hashCode());
    System.out.println("bean==bean2?:"+( bean==bean2));

}

结果:
1956710488
1956710488
bean==bean2?:true
        
```



2.原型模式（Prototype）:每次从容器中都会get的时候，都会产生一个新对象

```java
<bean name="john-classic" class="com.kuang.pojo.Person">
    <property name="name" value="John Doe"/>
    <property name="spouse" ref="jane"/>
    </bean>

 <bean name="john-modern"
    class="com.kuang.pojo.Person"
        p:name="John Doe"
            p:spouse-ref="jane"
                scope="prototype"/>


@Test
public void prototypeScope(){
        ApplicationContext context = new ClassPathXmlApplicationContext("bean.xml");
        Person bean = context.getBean("john-modern", Person.class);
        Person bean2 = context.getBean("john-modern", Person.class);

        System.out.println(bean.hashCode());
        System.out.println(bean2.hashCode());
        System.out.println("bean==bean2?:"+( bean==bean2));

}

retult:
1956710488
603856241
bean==bean2?:false
```

```txt
Bean中 id和name的区别
1)id与name 属性在作用上基本没有区别。推荐使用id。
 
2)id取值要求严格些，必须满足XML的命名规范。id是唯一的，配置文件中不允许出现两个id相同的<bean>。
 
3)name取值比较随意，甚至可以用数字开头。在配置文件中允许出现两个name相同的<bean>，在用getBean()返回实例时，后面一个Bean被返回。
 
4)如果没有id，name，则用类的全名作为name，如<bean class="test.Test">,可以使用getBean("test.Test")返回该实例。
```



3.其余的request、session、application 这些个作用域只能在web开发中使用到!

## bean的自动装配

自动装配 是spring满足bean依赖的一种方式!  

spring会在上下文中自动寻找，并自动给bean装配属性!

他的优点：

自动装配可以大大减少指定属性或构造函数参数的需要。

自动装配可以随着对象的发展而更新配置。

自动装配有4中模式

No   默认是No,这时候bean的引用必须使用ref来定义，



在spring有三种装配的方式

​	1、在xml中显示的配置

​	2、在java中显示的配置

​	3、隐式的自动装配bean【重要掌握】



### 6.1 方式1---在xml中显示的配置Autowired

#### 1.测试环境

1、环境搭建： 一个人有两个宠物! 这种形式一般就是组合

```java
package com.kuang.pojo;

public class People {
  
    private Cat cat;
    private Dog dog;
    private String name;

    public Cat getCat() {return cat;}

    public void setCat(Cat cat) {
        this.cat = cat;
    }

    public Dog getDog() {
        return dog;
    }

    public void setDog(Dog dog) {
        this.dog = dog;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
        @Override
    public String toString() {
        return "People{" +
                "cat=" + cat +
                ", dog=" + dog +
                ", name='" + name + '\'' +
                '}';
    }
}
```



####  2.  ByName

原理，会自动在容器的上下文查找，和自己对象 set 方法后面的值 对应的beanid! 

本例子中，people会自动装配一些值，装配的值根据 people里面的set方法确定， setCat(Cat cat) , setDog(Dog dog)

由于在手动配置xml过程中，常常发生字母缺漏和大小写等错误，而无法对其进行检查，使得开发效率 降低。
采用自动装配将避免这些错误，并且使配置简单化。

没有使用自动装配的配置, 我们需要为People的每一个属性进行手动装配 如下面的例子：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd" >

    <bean id="dog" class="com.kuang.pojo.Dog"/>
    <bean id="cat" class="com.kuang.pojo.Cat"/>
    <bean id="people" class="com.kuang.pojo.People" >
        <property name="name" value="张三"/>
        <property name="dog" ref="dog"/>
        <property name="cat" ref="cat"/>
    </bean>
</beans>
```



使用@AutoWire 注解的，就可以自动进行装配，Spring配置文件像下面这个样子

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="dog" class="com.kuang.pojo.Dog"/>
    <bean id="cat" class="com.kuang.pojo.Cat"/>
    <!--pojo people-->
    <bean id="people" class="com.kuang.pojo.People" autowire="byName">
        <property name="name" value="qinjiang"/>
    </bean>
</beans>
```

​	通过设置autowire=byName，在people中就不用设置dog和cat的<property name="name" ref="dog"/> , spring会自动在上下文里面找到和自己setDog后面同名的，找到就设置进去了。



测试：

```java
   
@Test
    public void testPeople(){
        ApplicationContext context = new ClassPathXmlApplicationContext("bean.xml");
        People people = context.getBean("people", People.class);
        people.getCat().shut();
        people.getDog().shut();
    }
```

结果：

```
喵喵
旺旺!
```

1. 再次测试，结果依旧成功输出！
2. 我们将 cat 的bean id修改为 cat22,cat33,
3. 再次测试， 执行时报空指针java.lang.NullPointerException。因为按byName规则找不对应set方 法，真正的setCat就没执行，对象就没有初始化，所以调用时就会报空指针错误。

**小结：**
当一个bean节点带有 autowire byName的属性时。

- 将查找其类中所有的set方法名，例如setCat，获得将set去掉并且首字母小写的字符串，即cat。
- 去spring容器中寻找是否有此字符串名称id的对象。
- 如果有，就取出注入；如果没有，就报空指针异常



#### 3. ByType

autoWire byType (按类型自动装配)
使用autowire byType首先需要保证：同一类型的对象，在spring容器中唯一。如果不唯一，会报不唯一 的异常。NoUniqueBeanDefinitionException

本例子中，people会自动装配一些值，装配的值根据 people里面的set方法确定， setCat(Cat cat) , setDog(Dog dog)

1、将user的bean配置修改一下 autowire="byType"

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

       xmlns:context="http://www.springframework.org/schema/context"

       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd

        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd" >
    <!--开启注解支持-->
    <context:annotation-config/>
    <bean id="dog" class="com.kuang.pojo.Dog"/>
    <bean id="cat" class="com.kuang.pojo.Cat"/>
    <bean id="people" class="com.kuang.pojo.People" autowire="byType"/>
</beans>
```

byType,会自动的在容器上下文中查找，和自己对象属性类型相同的bean！

2、测试正常输出

```xml
喵喵
旺旺!
People{cat=com.kuang.pojo.Cat@1372ed45, dog=com.kuang.pojo.Dog@6a79c292, name='null'}
```



3、再注册一个dog的bean对象

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

       xmlns:context="http://www.springframework.org/schema/context"

       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd

        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd" >
    <!--开启注解支持-->
    <context:annotation-config/>
    <bean id="dog" class="com.kuang.pojo.Dog"/>
    <bean id="dog2" class="com.kuang.pojo.Dog"/>
    <bean id="cat" class="com.kuang.pojo.Cat"/>
    <bean id="cat2" class="com.kuang.pojo.Cat"/>
    <bean id="people" class="com.kuang.pojo.People" autowire="byType"/>
</beans>
```

1. 测试，报错：NoUniqueBeanDeﬁnitionException
2. 删掉dog2，将dog的bean名称改掉！测试！因为是按类型装配，所以并不会报异常，也不影响后 的结果。甚至将id属性去掉，也不影响结果。
   这就是按照类型自动装配！

小结：

- 在byName的时候，需要保证所有bean的id唯一，并且这个bean需要和自动注入的属性的set方法的值一致~
- 在byType的时候，需要保证所有Bean的calss唯一，并且这个bean需要和自动注入的属性的类型一致!



上述这些是通过xml配置，实现自动装配的方式，在spring中实现自动装配有两种方式，下面就是通过注解方式实现自动装配



### 6.2 方式2---使用注解



jdk1.5支持的注解，spring从2.5就支持了注解



要使用注解须知

1、导入约束

2、配置注解的支持

```xml
<context:annotation-config/>
```



一个使用注解进行自动装配的案例

首先，编辑我们对应的xml配置文件，在这里我们需要把注解装配开关打开 <context:annotation-config/>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

       xmlns:context="http://www.springframework.org/schema/context"

       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd

        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd" >
    <context:annotation-config/>
    <bean id="dog" class="com.kuang.pojo.Dog"/>
    <bean id="cat" class="com.kuang.pojo.Cat"/>
    <bean id="people" class="com.kuang.pojo.People" />
</beans>
```

然后，到我们的People.java里使用@Autowired注解， 如下面的代码，就代表  People类的实例，将自动注解Cat cat和Dog dog这两个对象!

```java
public class People {
    @Autowired
    private Cat cat;
    @Autowired
    private Dog dog;
    private String name;

    public Cat getCat() { return cat;}
    public void setCat(Cat cat) {this.cat = cat;}
    public Dog getDog() {return dog;}
    public void setDog(Dog dog) { this.dog = dog;}
    public String getName() {return name;}
    public void setName(String name) { this.name = name;}
    @Override
    public String toString() {
        return "People{" +
                "cat=" + cat +
                ", dog=" + dog +
                ", name='" + name + '\'' +
                '}';
    }
}
```

然后，我们输入测试：

```java
@Test
public void testProple(){
    ApplicationContext context = new ClassPathXmlApplicationContext("bean.xml");
    People people = context.getBean("people", People.class);
    people.getCat().shut();
    people.getDog().shut();
    System.out.println(people.toString());
}
```

测试结果：

```
喵喵
旺旺!
People{cat=com.kuang.pojo.Cat@71a794e5, dog=com.kuang.pojo.Dog@76329302, name='null'}
```

小结:

1、通过使用@AutoWired 注解，比xml配置文件更省事，这样能让bean.xml里面对每个bean的定义更加简单

2、需要记住开启注解：<context:annotation-config/>

3、注解需要在对象上，比如private Cat cat; 不能用到private String name;

4、@AutoWired注解可以放在类的属性或者set方法上；

5、使用Autowired我们可以不用编写Set方法，前提是你这个自动装配的属性在IoC(Spring)容器中存在且符合名字byName

科普：

> @Nullable  字段标记了这个注解，说明这个字段可以是null;

```
@Autowired(required = false)  如果显示的改为false后，就说明这个对象可以为Null,否则不可以为空，false表示这个属性可以在配置文件中不设置
```

> @Qualifier(value="dog222")  这个意思是当前属性指定后面哪个bean。 
>
> 例如
>
> @Autowired
>
> @Qualifier(value="dog222")
>
> 而此时的xml配置文件为：
>
> ```
> <beans xmlns="http://www.springframework.org/schema/beans"
>     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
> 
>     xmlns:context="http://www.springframework.org/schema/context"
> 
>     xsi:schemaLocation="http://www.springframework.org/schema/beans
>      https://www.springframework.org/schema/beans/spring-beans.xsd
> 
>      http://www.springframework.org/schema/context
>      https://www.springframework.org/schema/context/spring-context.xsd" >
>  <context:annotation-config/>
>  <bean id="dog22" class="com.kuang.pojo.Dog"/>
>  <bean id="dog222" class="com.kuang.pojo.Dog"/>
>  <bean id="cat2" class="com.kuang.pojo.Cat"/>
>  <bean id="cat222" class="com.kuang.pojo.Cat"/>
>  <bean id="people" class="com.kuang.pojo.People" />
> </beans>
> ```
>
> @Autowired 这个注解就可以根据指定的dog222找到需要的了 
>
> 如果@Autowired自动装备的环境比较复杂，自动装备无法通过一个注解【@Autowired】完成的时候，我们可以用@Qualifier(value="xxx")去配合@Autowired的使用，指定一个唯一的bean对象注入!

**@Resource(name="cat2") 这样也可以实现，我们直接就找到了cat2**

```java
pojo实体类代码
public class People {
    @Resource(name="cat2")
    private Cat cat;
    @Autowired
    @Qualifier("dog222")
    private Dog dog;
    private String name;
    
    xml配置
    <context:annotation-config/>
    <bean id="dog22" class="com.kuang.pojo.Dog"/>
    <bean id="dog222" class="com.kuang.pojo.Dog"/>
    <bean id="cat2" class="com.kuang.pojo.Cat"/>
    <bean id="cat222" class="com.kuang.pojo.Cat"/>
    <bean id="people" class="com.kuang.pojo.People" />
    
    测试代码
        @Test
    public void testProple(){
        ApplicationContext context = new ClassPathXmlApplicationContext("bean.xml");
        People people = context.getBean("people", People.class);
        people.getCat().shut();
        people.getDog().shut();
        System.out.println(people.toString());
    }
```



小结



@Resource和@Autowired的区别

- 都是用来自动装配的，都可以放在属性字段上
- @Autowired 单独只按照byType注入，也可以按照名称进行匹配，但是比较麻烦，要和另外一个注解结合使用：@Autowired @Qualifier("XXX")。
- @Resource默认是通过byname方式实现，如果找不到名字，就通过byType实现，如果两个都找不到的情况下就报错。



### 6.3 方式3-隐式自动装配bean



<待学习>

## 使用注解开发

在spring4之后，要使用注解开发，必须要保证AOP的包导入

使用注解需要导入context约束，增加注解支持!

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

       xmlns:context="http://www.springframework.org/schema/context"

       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd

        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd" >
    <!--开启注解支持-->
    <context:annotation-config/>

</beans>
```

可以添加支持扫描注解

```xml
<!--指定要扫描的包，这个包下面的注解就会生效-->
<context:component-scan base-package="com.kuang.pojo"/>
```

1、bean

```java
@Component
public class User {
    //相当于  <property name="name" value="秦僵"/>
    @Value("狂神")
    public String name;

    @Value("狂神2")
    public void setName(String name) {
        this.name = name;
    }
}
```



2、属性如何注入

```java
@Component
public class User {
    //相当于  <property name="name" value="秦僵"/>
    @Value("狂神")
    public String name;

    @Value("狂神2")
    public void setName(String name) {
        this.name = name;
    }
}
```



3、衍生的注解

@Component有几个衍生注解，我们在web开发中，会按照mvc三层架构分层!

	- dao层----> @Repository  和Conponent一样，
	- service层 --->@Service   
	- controller层  --->@Controller  代表这个类被spring托管

这四个注解功能都是一样的，都是代表将某个类注册到Spring容器中，自动装配bean





4、自动装配

```
@Autowired 自动装配通过类型，名字，如果Autowired不能唯一装配上属性，就用@Qualifier("dog222")
@Nullable 字段标记了这个注解，说明这个字段可以为null
@Resource: 自动装配铜鼓类型。名字  使用方式  @Resource(name="cat2")
```

5、作用域

```java
@Component
@Scope("singleton")  //标记为单例模式
public class User {
    //相当于  <property name="name" value="秦僵"/>
    @Value("狂神")
    public String name;

    @Value("狂神2")
    public void setName(String name) {
        this.name = name;
    }
}
```

6、小结

xml与注解: 

- xml 更加万能，适用于任何场合，维护简单方便

- 注解 不是自己的类使用不了，维护相对复杂!

xml和注解的最佳实践：

	- xml用来管理bean;
	- 注解只负责完成属性的注入
	- 我们在使用的过程中，只需要注意一个问题：必须让注解生效，必须要在xml里面开启注解支持(扫描+开启)

## 使用java的方式配置Spring

我们现在要**完全不使用Spring的xml配置**了，全权交给java来做。 

JavaConfig 是Spring 的一个子项目，在Spring 4 之后，他成为了一个核心功能。

首先，编写pojo的User实体类, 注意，我们使用@Component  代表Spring组件 @Value("秦僵") 代表赋值

```java
//这里这个注解的意思，就是说明这个类被Spring接管了，注册到了容器中
@Component
public class User {
    @Value("秦僵")
    private String name;


    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

```

然后编写一个KuangConfig.java, 编写配置文件  @Configuration 代表这是一个配置服务类， @Bean代表这是一个spring的bean 

```java
@Configuration  //这个也会被Spring容器托管，注册到Spring容器中，因为他本身就是一个@Component。
// @Configuration 代表这是一个配置类，就是和我们之前看的beans.xml一样的
public class KuangConfig {
    @Bean  //注册一个bean，就相当于我们之前写的一个bean标签，
    //这个方法的名字，就相当于bean标签中的id使用,这个方法的返回值就相当于bean标签中的class属性
    public User getUser(){
        return new User(); //就是要返回要注入到bean的对象!
    }
}

```

最后测试类使用, 这里使用的是KuangConfig.getUser作为bean的id

```java
    @Test
    public void testAnnotation(){
        ApplicationContext context = new AnnotationConfigApplicationContext(KuangConfig.class);
        User getUser = context.getBean("getUser", User.class);
        System.out.println(getUser.getName());
    }
```



这种纯java的配置方式，在springboot中随处可见!

## IoC配置spring小结

一共有3种方式，分别为：

### 方式一: [Java配置](http://docs.spring.io/spring/docs/5.0.0.M5/spring-framework-reference/html/beans.html#beans-java)  这种方式，是定一个AppConfig配置类，

```java
第一步 编写一个AppCOnfig的配置类
@Configuration
public class AppConfig {

	@Bean
	public User user() {
		return new User();
	}
}
bean 的id就是方法名是user,bean的class是 User
第二步：编写我们的pojo类User
@Component
public class User {
    @Value("秦僵") //属性注入
    private String name;


    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}        
    
第三步：Instantiating the Spring container using AnnotationConfigApplicationContext
public static void main(String[] args) {
	ApplicationContext ctx = new AnnotationConfigApplicationContext(AppConfig.class);
	MyService myService = ctx.getBean(user.class);
	myService.doStuff();
}
```



### 方式二：[基于注解配置](http://docs.spring.io/spring/docs/5.0.0.M5/spring-framework-reference/html/beans.html#beans-annotation-config)

```java
第一步: 编写注解支持的xml配置文件，重点是加入 <context:annotation-config/> 支持注解
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
		http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context
		http://www.springframework.org/schema/context/spring-context.xsd">

	<context:annotation-config/>

</beans>

第二步：在需要被Spring控住注入的pojo 添加注解
@Component
public class User {
    //相当于  <property name="name" value="秦僵"/>
    @Value("狂神")
    public String name;

    @Value("狂神2")
    public void setName(String name) {
        this.name = name;
    }
}

第三步: 在xml配置文件，加入bean
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
		http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context
		http://www.springframework.org/schema/context/spring-context.xsd">

	<context:annotation-config/>

	<bean class="example.SimpleMovieCatalog">
		<!-- inject any dependencies required by this bean -->
	</bean>
</beans>

第四步：可以使用ClassPathXmlApplicationContext解析注解
    @Test
    public void testUser(){
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        User user = context.getBean("user", User.class);
        System.out.println(user.name);
    } 
        
```

### 方式三： 基于XML配置 [xml配置](https://docs.spring.io/spring-framework/docs/5.0.0.M5/spring-framework-reference/html/beans.html#beans-java)

```java
第一步: 编写支持的xml文件  applicationContext.xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="user" class="com.kunag.pojo.User">
        <!-- 在这里写 bean 的配置和相关引用 -->
        <property name="name" value="秦僵"/>
    </bean>
    </bean>

    <bean id="..." class="...">
        <!-- 在这里写 bean 的配置和相关引用 -->
    </bean>

    <!-- 在这里配置更多的bean -->

</beans>

第二步、编写我们的User类
public class User {
    private String name;

    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
} 
第三步: 用测试类使用测试
    @Test
    public void testUser(){
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        User user = context.getBean("user", User.class);
        System.out.println(user.name);
    }  
```

Spring的使用属性

1.所有的类都需要装配到spring里面，

2.所有的bean都需要通过容器去取

3.容器里面取出来的bean，拿出来就是一个具体的对象





## 设计模式之代理模式

为什么要学代理模式？因为这就是spring aop 和spring mvc 的底层设计模式!



代理模式的分类-23中设计模式之一

URL关系模式 

聚合和组合的区别：

组合是直接在Proxy中new Host(), Proxy的对消亡，Host对象一起跟随消亡

聚合是传参，不会随着Proxy对象的消亡而消亡

![image-20201220104024457](img/image-20201220104024457.png)

### 10.1 静态代理

角色分析：

- 抽象角色  一般会使用接口或者抽象类来解决
- 真实角色， 被代理的角色
- 代理角色  代理真实的角色，代理真实角色后，我们一般会做一些附属操作
- 客户 访问代理对象的人!

对应的代码：

```java
//步骤1、接口：租房接口，真实角色和代理角色要实现的
public interface RentHourse {
    public void rent();
}

//步骤2：真实角色  房东实现类，直接租房
public class Hourse implements RentHourse {
    public void rent() {
        System.out.println("房东:我出租房子!");
    }
}
//步骤三：代理角色  代理租房
public class Proxy implements RentHourse {
    private Hourse hourse;

    public Proxy() {
    }

    public Proxy(Hourse hourse) {
        this.hourse = hourse;
    }

    public void rent() {
        seeHouse();
        hourse.rent();
        hetong();
        fare();
    }

    //看房
    public void seeHouse() {
        System.out.println("代理:带你看房!");
    }

    //合同
    public void hetong() {
        System.out.println("代理:签订合同");
    }

    //收中介费
    public void fare() {
        System.out.println("代理:收中介费!");
    }
}
//## 步骤四 客户端访问代理角色 测试客户端
public class Client {
    public static void main(String[] args) {
        //房东要租房子
        Hourse hourse = new Hourse();
        //代理，中介帮房东租房子，但是呢，代理角一般会有一些附属操作!
        hourse.rent();

        Proxy proxy = new Proxy(hourse);
        proxy.rent();
    }
}
>>>结果：
房东:我出租房子!
代理:带你看房!
房东:我出租房子!
代理:签订合同
代理:收中介费!    
```

代理模式的好处：

	- 使得真实角色的操作更加纯粹，不用去关注一些公共的事情，业务
	- 公共业务交给代理角色!  实现了业务的分工!
	- 公共业务发生扩展的时候，方便集中管理!

代理模式的缺点：

​	一个真实角色就会产生一个代理角色，代码量会翻倍，开发效率会变低~

### 10.2 加深理解

示例代码

```java
### 首先，第一步，设计一个UserService接口，定义 一个增删改查接口
package com.kuang.demo002;
//抽象接口，这个抽象接口
public interface UserService {
    public void add();
    public void delete();
    public void update();
    public void query();
}

### 然后，第二步，设计一个真实角色，这个真实角色实现了UserService
//真是角色UserServiceImpl，实现UserSercie
public class UserServiceImpl implements UserService {
    public void add() {
        System.out.println("UserServiceImpl.add()");
    }

    public void delete() {
        System.out.println("UserServiceImpl.delete()");
    }

    public void update() {
        System.out.println("UserServiceImpl.update()");
    }

    public void query() {
        System.out.println("UserServiceImpl.query()");
    }
}

### 然后第三步，实现我们一个代理类，一些基本的方法、公共方法可以放在这里
public class UserServiceProxy implements UserService {
    private UserService userService;

    public void setUserService(UserService userService) {
        this.userService = userService;
    }

    public void add() {
        log("add()");
        userService.add();
    }

    public void delete() {
        log("delete()");
        userService.delete();
    }

    public void update() {
        log("update()");
        userService.update();
    }

    public void query() {
        log("query()");
        userService.query();
    }

    public void log(String msg){
        System.out.println("[debug] 当前执行方法为:"+msg);
    }
}

### 最后，第四步，我们使用这个代理类效果可以在client中
public class Client {
    public static void main(String[] args) {
        UserService userService = new UserServiceImpl();

        //代理模式
        UserServiceProxy userServiceProxy = new UserServiceProxy();
        userServiceProxy.setUserService(userService);
        userServiceProxy.add();


        UserService userService2 = new ProductServiceImpl();
        //代理模式
        ProductServiceProxy productServiceProxy = new ProductServiceProxy();
        productServiceProxy.setProductService(userService2);
        productServiceProxy.delete();

    }
} 
```



聊聊AOP，代码对应08-demo02

![image-20201220115719259](img/image-20201220115719259.png)



[细说spring-AOP详解](https://blog.csdn.net/q982151756/article/details/80513340) 经典好文，解释这个概念很好

### 10.3 动态代理

为了解决静态代理，每个真实角色都需要一个代理的缺点，引入了动态代理的概念，也就是反射!

动态代理和静态代理的角色一样，分别为 抽象角色，真实角色，代理角色，使用类

动态代理的代理类是动态生成的，不是我们直接写好的!

动态代理按照事先方式分为两大类： a）基于接口的动态代理  b)基于类的动态代理

-基于接口-jdk动态搭理

-基于类:cglib

-javassist 字节码类库



需要了解两个类：Proxy 代理   InvocationHandler  调用处理程序

动态代理例子代码：

```java
### 接口
package com.kuang.demo05;

public interface UserService {
    public void select();
    public void update();
    public void add();
    public void delete();
}

### UserService的实现
package com.kuang.demo05;

public class UserServiceImpl implements UserService{
    @Override
    public void select() {
        System.out.println("UserServiceImpl.select()");
    }

    @Override
    public void update() {
        System.out.println("UserServiceImpl.update()");
    }

    @Override
    public void add() {
        System.out.println("UserServiceImpl.add()");
    }

    @Override
    public void delete() {
        System.out.println("UserServiceImpl.delete()");
    }
}
### 动态代理类
package com.kuang.demo05;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.util.Date;

public class UserServiceProxy implements InvocationHandler {

    Object target; //被代理的对象，实际的方法执行者

    public UserServiceProxy(Object target) {
        this.target = target;
    }


    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        before();
        Object result = method.invoke(target, args);//调用target的method方法 这是反射机制 这里记住，proxy代表的是动态生成的UserService的代理类，target才是实际类。
        after();

        return result;//返回方法的执行结果
    }

    //调用invoke方法之前执行
    private void before() {
        System.out.println(String.format("log start time [%s]", new Date()));
    }

    //调用invoke方法之后执行
    private void after() {
        System.out.println(String.format("log end time [%s]", new Date()));
    }


}
### 测试类 Client（中间的代码可以封装，看最下面的代码）
public class Client {
    public static void main(String[] args) {
        // 设置变量可以保存动态代理类，默认名称以 $Proxy0 格式命名
        // System.getProperties().setProperty("sun.misc.ProxyGenerator.saveGeneratedFiles", "true");
        //1.创建被代理的对象，UserService 的接口实现类
        UserServiceImpl userServiceImpl = new UserServiceImpl();
        //2.获取需要传递给Proxy的ClassLoader, 获取UserServiceImpl对应的 ClassLoader
        ClassLoader classLoader = userServiceImpl.getClass().getClassLoader();
        //3.获取需要传递给Proxy的interfaces,这里的UserServiceImpl只实现了一个接口UserService，
        Class [] interfaces = userServiceImpl.getClass().getInterfaces();
        //4.生成需要传递给Proxy的IncovationHandler实现类, 须传入实际的执行对象 userServiceImpl
        UserServiceProxy userServiceProxy = new UserServiceProxy(userServiceImpl);
        //5 .至此，我们生成了我们需要的UserServiceImpl的代理类
        /*
        *根据上面提供的信息，创建代理对象 在这个过程中，
        *  a.JDK会通过根据传入的参数信息动态地在内存中创建和.class 文件等同的字节码
        *  b.然后根据相应的字节码转换成对应的class，
        *  c.然后调用newInstance()创建代理实例
        * */

        UserService proxy  = (UserService) Proxy.newProxyInstance(classLoader, interfaces, userServiceProxy);

        //如同使用静态代理一样代理类，调用方法
        proxy.add();
        proxy.select();
        proxy.update();
        // 保存JDK动态代理生成的代理类，类名保存为 UserServiceProxy
        // ProxyUtils.generateClassFile(userServiceImpl.getClass(), "UserServiceProxy");
    }
}
```





- 动态代理和静态代理角色一样
- 动态代理的代理类是动态生成的，不是我们直接写好的！
- 动态代理也分为两大类：基于接口的动态代理，基于类的动态代理
  - 基于接口----JDK动态代理
  - 基于类：cglib
  - java字节码实现：javasist

需要了解两个类：Proxy（代理）、InvocationHandler（调用处理程序）

**InvocationHandler**

动态代理的好处：

- 可以使真实角色的操作更加纯粹！不用关注一些公共的业务

- 公共事情就交给代理角色！实现了业务的分工

- 公共业务发生扩展的时候，方便集中管理

- 一个动态代理类代理的是一个接口，一般就是对应的一类业务

- 一个动态代理类可以代理多个类，只要是实现了同一个接口即可

  

**万能动态代理类**

```java
/**
 * 万能动态代理类
 * 
 */
//用这个类自动生成代理类
public class ProxyInvocationHandler implements InvocationHandler {

    //被代理的接口
    private Object target;

    public void setTarget(Object target) {
        this.target = target;
    }

    //生成得到代理类
    public Object getProxy(){
        return Proxy.newProxyInstance(this.getClass().getClassLoader(),target.getClass().getInterfaces(),this);
    }

    //处理代理示例，并返回结果
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        log(method.getName());
        Object result = method.invoke(target, args);
        return result;
    }

    public void log(String msg){
        System.out.println("执行了"+msg+"方法");
    }

}

```

测试

```java
public class Client {
    public static void main(String[] args) {
        //真实角色
        UserServiceImpl userService = new UserServiceImpl();
        //代理角色，不存在
        ProxyInvocationHandler pih = new ProxyInvocationHandler();
        //设置需要代理的对象
        pih.setTarget(userService);
        //动态生成代理
        UserService proxy = (UserService) pih.getProxy();
        proxy.query();
    }
}
```

## AOP 面向切面编程

### 11.1 什么是AOP

AOP(Aspect oriented progranming) 意思是面向切面编程，通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术，AOP是OOP的延续，是软件开发中的一个热点，也是spring框架中一个重要的内容，是函数式编程的一种衍生泛型。利用AOP可以对业务逻辑的各个部分进行有效的隔离，从而使得业务逻辑各部分之间的耦合度降低，提供程序的可重用性，同时提高了开发的效率。

![image-20201221091912194](img/image-20201221091912194.png)



### 11.2 Aop在spring中的应用

提供声名式事务，允许用户自定义切面!

- 横切关注点： 跨越应用程序多个模块的方法或功能，即是与我们业务逻辑无关，但是我们需要关注的部分，就是横切关注点，如日志，安全，缓存，事务等等....
- `切面(Aspect)`  Aspect 声明类似于 Java 中的类声明，在 Aspect 中会包含着一些 Pointcut 以及相应的 Advice
- `增强(Advice)`  Advice 定义了在 `Pointcut` 里面定义的程序点具体要做的操作，它通过 before、after 和 around 来区别是在每个 joint point 之前、之后还是代替执行的代码
- `目标(Target)`  织入 `Advice` 的目标对象。 
- 代理(Proxy)  向目标对象应用通知之后创建的对象。 （生成的代理类)
- `切入点(PointCut)`  表示一组 joint point，这些 joint point 或是通过逻辑关系组合起来，或是通过通配、正则表达式等方式集中起来，它定义了相应的 Advice 将要发生的地方。
- `连接点(JointPoint)` ` 爪哇的小县城里的百姓: 因为根据定义, `Joint point` 是所有可能被织入 `Advice` 的候选的点, 在 Spring AOP中, 则可以认为所有方法执行点都是 `Joint point`. 而在我们上面的例子中, 命案发生在小县城中, 按理说在此县城中的所有人都有可能是嫌疑人.

>AOP基本概念
>
>**连接点（****Joinpoint****）：**
>
>表示需要在程序中插入横切关注点的扩展点，连接点可能是类初始化、方法执行、方法调用、字段调用或处理异常等等，Spring只支持方法执行连接点，**在****AOP****中表示****为****“****在哪里做****”**；
>
>**切入点（****Pointcut****）：**
>
>选择一组相关连接点的模式，即可以认为连接点的集合，Spring支持perl5正则表达式和AspectJ切入点模式，Spring默认使用AspectJ语法，**在****AOP****中表示为****“****在哪里做的****集合****”**；
>
>**增强（****Advice****）：**或称为增强
>
>在连接点上执行的行为，增强提供了在AOP中需要在切入点所选择的连接点处进行扩展现有行为的手段；包括前置增强（before advice）、后置增强 (after advice)、环绕增强 （around advice），在Spring中通过代理模式实现AOP，并通过拦截器模式以环绕连接点的拦截器链织入增强 ；**在****AOP****中表示为****“****做什么****”****；**
>
>**方面****/****切面（****Aspect****）：**
>
>横切关注点的模块化，比如上边提到的日志组件。可以认为是增强、引入和切入点的组合；在Spring中可以使用Schema和@AspectJ方式进行组织实现；**在****AOP****中表****示为****“****在哪里做和做什么集合****”****；**
>
>**目标对象（****Target Object****）：**
>
>需要被织入横切关注点的对象，即该对象是切入点选择的对象，需要被增强的对象，从而也可称为“被增强对象”；由于Spring AOP 通过代理模式实现，从而这个对象永远是被代理对象，**在****AOP****中表示为****“****对谁做****”**；
>
>**AOP****代理（****AOP Proxy****）：**
>
>AOP框架使用代理模式创建的对象，从而实现在连接点处插入增强（即应用切面），就是**通过代理来对目标对象应用切面**。在Spring中，AOP代理可以用JDK动态代理或CGLIB代理实现，而通过拦截器模型应用切面。
>
>**织入（****Weaving****）：**
>
>织入是一个过程，是将切面应用到目标对象从而创建出AOP代理对象的过程，织入可以在编译期、类装载期、运行期进行。
>
>**引入（****inter-type declaration****）：**
>
>也称为内部类型声明，为已有的类添加额外新的字段或方法，Spring允许引入新的接口（必须对应一个实现）到所有被代理对象（目标对象）, **在****AOP****中表示为****“****做什么****（新增什么）****”**；
>
>
>
>AOP的Advice类型
>
>**前置增强（****Before advice****）：**
>
>在某连接点之前执行的增强，但这个增强不能阻止连接点前的执行（除非它抛出一个异常）。
>
>**后置返回增强（****After returning advice****）：**
>
>在某连接点正常完成后执行的增强：例如，一个方法没有抛出任何异常，正常返回。
>
>**后置异常增强（****After throwing advice****）：**
>
>在方法抛出异常退出时执行的增强。
>
>**后置最终增强（****After (finally) advice****）：**
>
>当某连接点退出的时候执行的增强（不论是正常返回还是异常退出）。
>
>**环绕增强****（****Around Advice****）：**
>
>包围一个连接点的增强，如方法调用。这是最强大的一种增强类型。 环绕增强可以在方法调用前后完成自定义的行为。它也会选择是否继续执行连接点或直接返回它们自己的返回值或抛出异常来结束执行。

![image-20201221095317463](img/image-20201221095317463.png)

![image-20201221095518363](img/image-20201221095518363.png)



### 11.3使用Spring实现Aop

重点，使用AOP植入，需要导入一个依赖包

```xml
<dependency>
    <groupId>org.aspectj</groupId>
      <artifactId>aspectjweaver</artifactId>
       <version>1.9.4</version>
</dependency>
```



### 11.4方式1:使用spring 的api接口

首先，第一步，准备环境，把UserService和UserServiceImpl写好

```java
package com.kuang.service;

public interface UserService {
    public void select();
    public void update();
    public void add();
    public void delete();
}

package com.kuang.service;

public class UserServiceImpl implements UserService{
    public void select() {
        System.out.println("查询了一个用户!");
    }

    public void update() {
        System.out.println("更新了一个用户!");
    }

    public void add() {
        System.out.println("增加了一个用户!");
    }

    public void delete() {
        System.out.println("删除了一个用户!");
    }
}
```

然后，设计我们的切面类

```java
public class AfterLog implements AfterReturningAdvice {
    //returnValue  执行后返回值
    public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
        System.out.println("after: 执行了"+method.getName()+"方法, 返回的结果:"+returnValue);

    }
}

public class BeforeLog implements MethodBeforeAdvice {
    //method 要执行的目标对象的方法
    //args 参数
    //target 目标对象
    public void before(Method method, Object[] args, Object target) throws Throwable {
        System.out.println("before:"+target.getClass().getName()+"的"+method.getName()+"被执行了!");
    }
}
```

接着，在applicationContext.xml里面配置aop

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"

       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd

        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd

        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">
    <!--开启注解支持-->
    <context:annotation-config/>
    <!--指定要扫描的包，这个包下面的注解就会生效-->
    <context:component-scan base-package="com.kuang"/>
    <!--注册bean-->
    <bean id="userService" class="com.kuang.service.UserServiceImpl"/>
    <bean id="log" class="com.kuang.log.BeforeLog"/>
    <bean id="afterLog" class="com.kuang.log.AfterLog"/>
    <!--配置aop,需要导入aop的约束-->
    <aop:config>
        <!--首先需要一个切点  <aop:pointcut>
		execution(要执行的位置)： 定义切点的表达式部分
        第一个*： 表示返回值的类型任意
        com.kuang.service.UserServiceImpl： AOP所切的服务的类名，即，需要进行横切的业务类
        .*(..) ： 表示任何方法名，括号表示参数，两个点表示任何参数类型
        -->
        <aop:pointcut id="pointcut" expression="execution(* com.kuang.service.UserServiceImpl.*(..))"/>
        <!--执行环绕增强-->
        <aop:advisor advice-ref="log" pointcut-ref="pointcut"/> <!--表示将log这个类切入到pointcut这个切入点-->
        <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"/>
    </aop:config>
</beans>
```

最后，就可以在我们的测试客户端使用了

```java
public class MyTest {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        //动态代理代理的是接口
        UserService userService = context.getBean("userService", UserService.class);
        //执行add方法
        userService.add();
    }
}
```

### 11.5 方式2：自定义类实现AOP

首先，先定义一个自己的普通类

```java
public class DiyPointCut {
    public void before(){
        System.out.println("===============方法执行前=============");
    }

    public void after(){
        System.out.println("===============方法执行后=============");
    }
}
```

第二步，我们进入到applicationContext.xml，使用如下aop配置

```xml
    <!--方式二：自定义类-->
    <bean id="diy" class="com.kuang.dit.DiyPointCut"/>
    <aop:config>
        <!--自定义切面，ref要引入的类-->
        <aop:aspect ref="diy">
            <!--切入点-->
            <aop:pointcut id="point" expression="execution(* com.kuang.service.UserServiceImpl.*(..))"/>
            <!--增强 Advisor-->
            <aop:before method="before" pointcut-ref="point"/>
            <aop:after method="after" pointcut-ref="point"/>
        </aop:aspect>
    </aop:config>
```

然后，我们就可以去测试类进行使用测试了

```java
public class MyTest {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        //动态代理代理的是接口
        UserService userService = context.getBean("userService", UserService.class);
        //执行add方法
        userService.add();
    }
}
```

运行的结果

```
===============方法执行前=============
增加了一个用户!
===============方法执行后=============
```

### 11.5 方式3 使用注解实现

注解我们可以直接在代码定义

```java
//方式3，使用注解方式实现AOP

@Aspect  //标注这个类是一个切面
public class AnnotationPointCut {
    //  @Before 表示 public void befor()是一个方法前增强，"execution(* com.kuang.service.UserServiceImpl.*(..))"是一个切点
    @Before("execution(* com.kuang.service.UserServiceImpl.*(..))") 
    public void before(){
        System.out.println("=====方法执行前=====");
    }
    //  @After 表示 public void after()是一个方法前增强，"execution(* com.kuang.service.UserServiceImpl.*(..))"是一个切点
    @After("execution(* com.kuang.service.UserServiceImpl.*(..))") 
    public void after(){
        System.out.println("=====方法执行前=====");
    }
    //在环绕增强中，我们可以给定一个参数，代表我们要获取处理切入的点
    @Around("execution(* com.kuang.service.UserServiceImpl.*(..))") //这是原来配置的连接点
    public void around(ProceedingJoinPoint joinPoint) throws Throwable {
        System.out.println("=====环绕前=====");
        //执行方法
        Object proceed = joinPoint.proceed();

        System.out.println("=====环绕后=====");

        // Signature signature = joinPoint.getSignature(); //获得当前执行方法的签名
        // System.out.println("signature" + signature);
    }
}
```

写完后，我们需要去进入到applicationContext.xml里面进行配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"

       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd

        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd

        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">
    <!--开启注解支持-->
    <context:annotation-config/>
    <!--指定要扫描的包，这个包下面的注解就会生效-->
    <context:component-scan base-package="com.kuang"/>
    <!--注册bean-->
    <bean id="userService" class="com.kuang.service.UserServiceImpl"/>
    <bean id="log" class="com.kuang.log.BeforeLog"/>
    <bean id="afterLog" class="com.kuang.log.AfterLog"/>
    <!--&lt;!&ndash;方式一，使用apring api配置aop,需要导入aop的约束&ndash;&gt;-->
    <!--<aop:config>-->
    <!--    &lt;!&ndash;首先需要一个切入点  execution(要执行的位置)-->
    <!--    第一个*-->
    <!--    第二个 com.kuang.service.UserServiceImpl-->
    <!--    第三个: *(..) 下面的所有方法-->
    <!--    &ndash;&gt;-->
    <!--    <aop:pointcut id="pointcut" expression="execution(* com.kuang.service.UserServiceImpl.*(..))"/>-->
    <!--    &lt;!&ndash;执行环绕增强&ndash;&gt;-->
    <!--    <aop:advisor advice-ref="log" pointcut-ref="pointcut"/> &lt;!&ndash;表示将log这个类切入到pointcut这个切入点&ndash;&gt;-->
    <!--    <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"/>-->
    <!--</aop:config>-->
    <!--方式二：自定义类-->
    <bean id="diy" class="com.kuang.dit.DiyPointCut"/>
    <!--<aop:config>-->
    <!--    &lt;!&ndash;自定义切面，ref要引入的类&ndash;&gt;-->
    <!--    <aop:aspect ref="diy">-->
    <!--        &lt;!&ndash;切入点&ndash;&gt;-->
    <!--        <aop:pointcut id="pointcut" expression="execution(* com.kuang.service.UserServiceImpl.*(..))"/>-->
    <!--        &lt;!&ndash;通知 Advisor&ndash;&gt;-->
    <!--        <aop:before method="before" pointcut-ref="pointcut"/>-->
    <!--        <aop:after method="after" pointcut-ref="pointcut"/>-->
    <!--    </aop:aspect>-->
    <!--</aop:config>-->
    <!--方式三，注解方式实现AOP-->
    <bean id="annotationPointCut2" class="com.kuang.dit.AnnotationPointCut"/>
    <!--必须开启注解支持!-->
    <aop:aspectj-autoproxy/>
</beans>
```

最后，我们来进行测试

```java
public class MyTest {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        //动态代理代理的是接口
        UserService userService = context.getBean("userService", UserService.class);
        //执行add方法
        userService.add();
    }
}
```

## 12 回顾MyBatis

步骤：

第1步 、导入相关jar包

junit

mybatis

mysql数据库的

spring相关的

aop织入器

mybatis-spring[new知识点]

### 12.1 回忆mybatis

1、编写实体类

2、编写核心配置文件

3、编写接口

4、编写mapper.xml, 要注册这个接口

5、编写测试程序

```xml
  <dependencies>
        <!--SpringFramework5-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.2</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.2.0.RELEASE</version>
        </dependency>
        <!--spring操作数据库的话，还需要spring-jdbc-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.2.0.RELEASE</version>
        </dependency>
        <!--AOP织入包-->
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.4</version>
        </dependency>
        <!--mybatis-spring-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>2.0.2</version>
        </dependency>
    </dependencies>
```



第2步、编写配置文件 resources/mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--引入外部配置文件-->
    <properties resource="db.properties" />
    <!--mybatis配置-->
    <settings>
        <setting name="cacheEnabled" value="true"/>
        <setting name="lazyLoadingEnabled" value="true"/>
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>
    <typeAliases>
        <package name="com.kuang.pojo"/>
    </typeAliases>

    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;characterEncoding=UTF-8&amp;useUnicode=True"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <!--<mapper resource="com/kuang/mapper/UserMapper.xml"/>-->
        <mapper class="com.kuang.mapper.UserMapper"/>
    </mappers>

</configuration>
```

3、编写实体类 pojo/User.java

```java
import lombok.Data;

@Data
public class User {
    private int id;
    private String name;
    private String pwd;
}

```

4、编写实体类接口mapper/UserMapper.java

```java
public interface UserMapper {
    //查询用户列表
    public List<User> selectUser();
}
```



5、编写接口对应的配置文件  mapper/UserMapper.xml  要和UserMapper同一个名称和位置

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.kuang.mapper.UserMapper">
    <!--查询所有用户功能-->
    <select id="selectUser" resultType="user">
        select * from mybatis.user;
    </select>
</mapper>
```



6、进行测试

```java
public class MyTest {
    @Test
    public void selectUser() throws IOException {
        String resources = "mybatis-config.xml";
        InputStream in = Resources.getResourceAsStream(resources);
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(in);
        SqlSession sqlSession = sessionFactory.openSession(true);//自动提交事务，加上true

        UserMapper mapper = sqlSession.getMapper(UserMapper.class);

        List<User> users = mapper.selectUser();

        for (User user : users) {
            System.out.println(user);
        }


    }
}
```

静态资源过滤问题

```
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.xml</include>
                <include>**/*.properties</include>
            </includes>
        </resource>

        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.xml</include>
                <include>**/*.properties</include>
            </includes>
        </resource>
    </resources>
</build>
```

### 12.2 整合spring方式一



先准备环境，新建实体类User.java，并创建UserMapper和UserMapper.xml

```java
//com.kuang.pojo.User
@Data
public class User {
    private int id;
    private String name;
    private String pwd;
}

//com.kuang.mapper.UserMapper
public interface UserMapper {
    public List<User> selectUser();
}

//com.kuang.mapper.UserMapper.xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.mybatis.example.BlogMapper">
    <select id="selectUser" resultType="user">
    select * from mybatis.user;
    </select>
</mapper>
```



第一步：编写数据源的配置文件和mybatis的配置文件  spring-dao.xml  mybatis-config.xml。

```xml
### spring-dao.xml的配置
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--配置数据源-->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <!-- collaborators and configuration for this bean go here -->
        <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;characterEncoding=UTF-8&amp;useUnicode=True"/>
        <property name="username" value="root"/>
        <property name="password" value="123456"/>
    </bean>
</beans>

### mybatis  mybatis-config.xml 的配置

<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <settings>
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>
    <typeAliases>
        <package name="com.kuang.pojo"/>
    </typeAliases>
</configuration>

```



第二步：在spring-dao.xml里面，配置加载sqlSessionFactiory

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


    <!--配置数据源-->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <!-- collaborators and configuration for this bean go here -->
        <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;characterEncoding=UTF-8&amp;useUnicode=True"/>
        <property name="username" value="root"/>
        <property name="password" value="123456"/>
    </bean>
    <!--配置sqlSessionFactory-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource" />
        <!--绑定Mybatis配置文件-->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
        <property name="mapperLocations" value="classpath:com/kuang/mapper/*.xml" />
    </bean>
    <!--使用sqlSessionFactory构建sqlSession-->
    <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
        <constructor-arg index="0" ref="sqlSessionFactory" />
    </bean>
</beans>
```



第三步：在spring-dao.xml里面配置加载 SqlSessionTemplate

```xml
    <!--使用sqlSessionFactory构建sqlSession-->
    <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
        <constructor-arg index="0" ref="sqlSessionFactory" />
    </bean>
```



第四步：给接口做实现类

```java
public class UserMapperImpl implements UserMapper{
    
    private SqlSession sqlSession;

    public void setSqlSession(SqlSession sqlSession) {
        this.sqlSession = sqlSession;
    }

    public List<User> selectUser() {
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        List<User> users = mapper.selectUser();
        return users;
    }
}
```

第五步：将自己写的实现类UserMapperImpl注入到spring配置文件 spring-dao.xml中

```xml
<bean id="selectUser" class="com.kuang.mapper.UserMapperImpl"/>
```



第六步：测试使用

```java
    @Test
    public void springSelectUser(){

        ApplicationContext context = new ClassPathXmlApplicationContext("spring-dao.xml");
        UserMapper userMapper = context.getBean("userMapper",UserMapper.class);
        List<User> users = userMapper.selectUser();
        for (User user : users) {
            System.out.println(user);
        }
    }
```





### 12.3 整合spring-mybatis方式二

继承了SqlSessionDaoSupport就可以直接使用getSqlSession()获取sqlSession

`SqlSessionTemplate` 是 MyBatis-Spring 的核心。作为 `SqlSession` 的一个实现，这意味着可以使用它无缝代替你代码中已经在使用的 `SqlSession`。 `SqlSessionTemplate` 是线程安全的，可以被多个 DAO 或映射器所共享使用。

当调用 SQL 方法时（包括由 `getMapper()` 方法返回的映射器中的方法），`SqlSessionTemplate` 将会保证使用的 `SqlSession` 与当前 Spring 的事务相关。 此外，它管理 session 的生命周期，包含必要的关闭、提交或回滚操作。另外，它也负责将 MyBatis 的异常翻译成 Spring 中的 `DataAccessExceptions`。

由于模板可以参与到 Spring 的事务管理中，并且由于其是线程安全的，可以供多个映射器类使用，你应该**总是**用 `SqlSessionTemplate` 来替换 MyBatis 默认的 `DefaultSqlSession` 实现。在同一应用程序中的不同类之间混杂使用可能会引起数据一致性的问题。

可以使用 `SqlSessionFactory` 作为构造方法的参数来创建 `SqlSessionTemplate` 对象。



第一步：编写实现类，并集成SqlSessionDaoSupport

```java
public class UserMapperImpl2 extends SqlSessionDaoSupport implements UserMapper{
    //继承了SqlSessionDaoSupport就可以直接使用getSqlSession()获取sqlSession
    // private SqlSession sqlSession;
    public List<User> selectUser() {
//        sqlSession = getSqlSession();
//        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
//        List<User> users = mapper.selectUser();
//        return users;
        return getSqlSession().getMapper(UserMapper.class).selectUser();
    }
}
```

第二步：进入到spring的bean配置文件，注入

```xml
   <bean id="userMapper2" class="com.kuang.mapper.UserMapperImpl2">
        <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
    </bean>
```

第三步，我们测试一下

```java
public class UserMapperImpl2 extends SqlSessionDaoSupport implements UserMapper{
    //继承了SqlSessionDaoSupport就可以直接使用getSqlSession()获取sqlSession
    private SqlSession sqlSession;
    
    public List<User> selectUser() {
        sqlSession = getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        List<User> users = mapper.selectUser();
        return users;
    }
}
```

## 声明式事务

### 1. 回顾事务

要么都成功，要么都失败

事务在项目开发中，十分重要，涉及到数据的一致性问题，不能马虎

确保完整性和一致性!

事务的ACID原则

A：原子性

C 一致性

I 隔离性  多个业务可能操作同一个资源，是互相隔离的，防止数据损坏，

D 持久性 事务一旦完成，系统不管干嘛，发生什么问题，数据都是存在，结果不再被影响，被持久化写到存储器中



2、Spring中的事务管理

- 声明式事务 AOP

第一步，配置

```xml
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <constructor-arg ref="dataSource" />
        <!--<property name="dataSource" ref="dataSource"/>-->
    </bean>
```

第二步：配置事务管理器, 结合AOP实现事务的织入

```xml
    <!--第二步:结合AOP实现事务的织入-->
    <!--配置事务通知-->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <!--1.给那些方法配置事务-->
        <!--2.配置事务的传播特性 new propagation-->
        <tx:attributes>
            <tx:method name="add*" propagation="REQUIRED" />
            <tx:method name="delete*" propagation="REQUIRED" />
            <tx:method name="update*" propagation="REQUIRED"/>
            <tx:method name="query" read-only="true"/>
            <tx:method name="*"/>   <!--配置所有事务-->
        </tx:attributes>
    </tx:advice>
```

第三步，配置切面

```xml
    <!--第三步 配置事务切入-->

    <aop:config>
        <aop:pointcut id="txPointCut" expression="execution(* com.kuang.mapper.*.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"/>
    </aop:config>
```



- 编程式事务 需要在自己代码中写入事务管理



思考：为什么需要事务

如果不配置事务，可能存在数据提交不一致的情况下!

如果我们不在spring中去配置声明式事务，我们就需要在代码中手动配置事务!

事务在项目开发中十分重要，涉及到数据的一致性完整性



## 总结

Bean创建对象，依赖注入

sqlsession

```
继承了SqlSessionDaoSupport就可以直接使用getSqlSession()获取sqlSession
```



# SpringMVC

## 1. 回顾servlet

JAVASE 认真学习，老师带，入门快

JavaWeb  认真学习，老师带，入门快

SSM框架，研究官方文档，锻炼自学能力，锻炼笔记能力，锻炼项目能力

Spring MVC+VUE+SpringBoot+SpringCloud+Linux

Srping IOC 和AOP

Spring MVC 执行流程特别重要! 需要重点听懂！

Sring mvc ssm框架整合，这个也是重点!

### 什么是MVC？

模型(Dao,service)   视图(jsp)     控制器(Servlet) 是一种软件设计的规范!

是将业务逻辑，数据显示分离的方法来组织代码

职责分析

Controller:控制器

1、取得表单数据

2、调用业务逻辑

3、转向指定的页面

Model： 模型

1、实现业务逻辑

2、保存数据的状态

View 视图

1、显示页面

### 回顾Servlet

如何新建一个servlet项目？

首先，创建一个空的maven父项目，创建后将src目录删除掉。同时加上依赖

```xml
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.2.0.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>servlet-api</artifactId>
            <version>2.5</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.2</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
    </dependencies>
```

第二步：点击项目，创建一个Module，也是不选择wepapp模板，创建一个springmvc-01-serlvet的子项目，添加成功后，在项目添加web Framework support

![`image-20201225121524456`](img/image-20201225121524456-16536396930702.png)

第三步: 编写一个Servlet类，用来处理用户的请求

```java
//实现servlet接口
public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获得参数
        String method = req.getParameter("method");
        if (method.equals("add")&&method!=null){
            req.getSession().setAttribute("msg","执行了add方法");
        }
        if (method.equals("delete")&& method!=null){
            req.getSession().setAttribute("msg","执行了delete方法!");
        }
        //业务逻辑部分

        //视图跳转部分
        req.getRequestDispatcher("/WEB-INF/jsp/hello.jsp").forward(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

第四步： 到web.xml里面配置servlet

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.kuang.servlet.HelloServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>

    <session-config>
        <!--配置session30分钟超市-->
        <session-timeout>30</session-timeout>
    </session-config>
    <!--配置欢迎页-->
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>
</web-app>
```

第五步: 在WEB-INF文件夹下面，创建一个jsp文件夹，并添加hello.jsp文件

> 关于文件放到WEB-INF还是web的知识点：
>
> 如果项目文件让用户不可见，可以放到/web/WEB-INF/下面
>
> 如果共用的文件，可以放到/web/文件夹



> jsp页面取参数的形式  ${msg} 



MVC框架做了哪些事情？

1、将URL映射到JAVA类或者JAVA类的方法

2、封装用户提交的数据

3、处理请求-调用相关的业务处理--封装响应数据。

4、将响应的数据进行渲染 jsp/html等表示层数据

说明：

常见服务器端MVC框架有struts,SpringMVC ASP。net MVC  zend Framework,jsf,常见的mvc前端框架：vue angularjs,react,backbone,由MVC演化出来另外一些模式

比如MVP  MVVM等等....



## 2.初识springmvc及原理

Spring MVC是Spring Framework的一部分，是基于Java实现的MVC的轻量级Web框架!

为什么学习Spring MVC呢

1、轻量级，简单易学

2、高效，基于请求响应的MVC构架

3、与spring兼容性好，无缝结合

4、约定优于配置

5、功能强大RESTFul,数据验证，格式化，本地化，主题等

6、简洁灵活

### 1.springmvc 概述



Spring：大杂烩，我们可以将SpringMVC中所有需要的bean注册到Spring中

Spring的web框架围绕DispatcherServlet设计。DispatcherServlet的作用是将请求分发到不同的处理器，从spring2.5开始，使用java5或者以上版本的用户可以采用基于注释的controller声明方式

Spring mvc框架像许多其他mvc框架一样，以请求为驱动，围绕一个中型Servlet分配请求和提供其他功能，DispatcherServlet实际上也是一个Servlet（它集成自HttpServlet基类）

![image-20201225134130314](img/image-20201225134130314.png)



Spring MVC的原理如下图所示:

​	当发起请求时被前置的控制器拦截到请求，根据请求参数生成代理请求，找到请求对应的实际控制其，控制器处理请求，创建数据类型，访问数据库，将模型响应给中心控制器，控制器使用模型与视图渲染视图结果，将结果返回给中心控制器，再将结果返回给请求者!

![image-20201225134657571](img/image-20201225134657571.png)



### 2.第一个springmvc

首先，创建一个空的项目，项目是个maven子项目

然后，在项目中添加web支持

第3步, 在web.xml中注册DispatcherServlet

```xml
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--1.注册DispathcerServlet-->
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!--关联一个springmvc的配置文件:[servlet-name]-servlet.xml-->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <!--启动级别-1-->
        <load-on-startup>1</load-on-startup>
    </servlet>
    
    <!--/ 匹配所有的请求:不包括.jsp-->
    <!--/* 匹配所有的请求:包括.jsp-->
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

第4步，编写springmvc的配置文件，在src/main/resources 下新建 springmvc-servlet.xml:[servletname]-servlet.xml，说明，这里的名称要求是按照官方来的。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans  
        http://www.springframework.org/schema/beans/spring-beans.xsd">
</beans>
```

第5步： 添加处理映射器

```xml
    <!--添加处理映射器-->
    <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
```

第6步，添加处理适配器

```xml
   <!--添加处理适配器-->
    <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>
```



第7步 添加视图解析器

```xml
    <!--添加视图解析器-->
    <!--视图解析器:DispatcherServlet给他的ModelAndView-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <!--前缀-->
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <!--后缀-->
        <property name="suffix" value=".jsp"/>
    </bean>
```

第8步：编写我们操作业务的Controller，要么实现Controller接口，要么增加注解，需要返回一个ModelAndView,装数据，封视图

```java
package com.kuang.controller;
import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.Controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

//注意 这里我们要先导入Controller接口
public class HelloController implements Controller {
    public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
        // ModelAndView 模型和视图
        ModelAndView mv = new ModelAndView();
        //封装对象，放在ModelAndView中，Model
        mv.addObject("msg","HelloSpringMVC!");
        //封装要跳转的视图，放在ModelAndView中
        mv.setViewName("hello"); //WEB-INF/jsp/hello.jsp
        return mv;
    }
}

```

第9步 将自己的类交给springioc容器，在springmvc-servlet.xml 注册bean, 注意这里的bean id必须以 /开头

```xml
    <!--Handler-->
    <bean id="/hello" class="com.kuang.controller.HelloController"/>
```

第10步 在/web/WEB-INF/jsp/hello.jsp   写要跳转的jsp页面，显示ModelAndView存放的数据，以及我们的正常页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>springmvc</title>
</head>
<body>
    ${msg}
</body>
</html>
```



可能到的问题:访问出现404，排查步骤

1、查看控制台输出，看一下是不是少了什么jar包

2、如果jar报存在 ，显示无法输出，就在IDEA的项目发布中，添加lib依赖

3、重启Tomcat即可解决

小结：看这个估计大部分同学就能理解其中原理了，但是我们实际开发不会这么写，不然就疯了，还学这个玩意干嘛，我们来看注解版实现，这个才是springmvc的精髓，到底多么简单，看这个图就知道了。



### 3. springmvc原理

Spring MVC的原理如下图所示:

​	当发起请求时被前置的控制器拦截到请求，根据请求参数生成代理请求，找到请求对应的实际控制其，控制器处理请求，创建数据类型，访问数据库，将模型响应给中心控制器，控制器使用模型与视图渲染视图结果，将结果返回给中心控制器，再将结果返回给请求者!



![image-20201225154309926](img/image-20201225154309926.png)

​	老师画的精细版SPRINGMVC执行原理，

![image-20201225151715507](img/image-20201225151715507.png)

这个图是spring mvc 的一个完整的流程图，只有虚线才是我们要做的，实现部分都是spring mvc已经帮我们做了的。





简要的分析一下执行的流程：

1、DispatcherServlet表示前置的控制器，是整个spring mvc的控制中心，用户发出请求，DispatcherServlet接受请求并拦截请求

假设url为 http://localhost:8080/springmvc/hello 这个url就可以拆分成3个部分

http://localhost:8080  这是服务器的域名

springmvc部署在服务器上的web站点

hello  表示控制器

通过分析，如上url表示为:请求位于服务器localhost:8080 上的springmvc站点的hello控制器

2、HandlerMapping为处理器映射，由DispathcerServlet自动调用

HandlerMapping根据请求url的控制器去查找在springmvc-config.xml里面的Handler.

3、HandlerExecution表示具体的Handler，其主要作用是根据url查找控制器，如上url被查找的控制器为 hello

4、HandlerExecution 将解析后的信息传递给DispatcherServlet,如解析控制器映射等。

5、HandlerApdapter表示处理器适配器，其按照特定的规则去执行Handler.

6、Handler让具体的Controller执行

7、Controller将具体的执行信息返回给HandlerAdapter,如ModelAndView.

8、HandlerAdapter将试图逻辑名或者模型传递给DispatcherServlet

9、DispatcherServlet调用视图解析器(ViewResolver)来解析HandlerAdapter传递的逻辑视图名

10、试图解析器将解析的逻辑视图名传递给DispatcherServlet.

11、DispatcherServlet根据试图解析器解析后的视图结构，调用具体的视图

12、最终视图呈现给用户，

在这里听一遍原理，不理解么有关系，我们马上来一写一个对应的代码实现大家就明白了，如果不明白，那就写10遍，没有笨人，只有懒人!

> spring mvc中  
>
> ```
> <servlet-mapping>
>  <servlet-name>springmvc</servlet-name>
>  <url-pattern>/</url-pattern>
> </servlet-mapping>
> ```
>
> / 和/* 有区别 
>
> / :只匹配所有的请求，不会去匹配jsp页面
>
> /*: 匹配所有的请求，包括Jsp页面

## 3. 使用注解开发SpringMVC



第1步：创建一个空的maven项目，并加入web支持，此处需要记住，web.xml必须使用4.0及以上版本，不然会出现代码无法运行

![image-20201226011001808](img/image-20201226011001808.png)

第2步: 配置项目的依赖，需要关注project structure，里面需要在项目里面加入lib包

pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>springmvc-study</artifactId>
    <packaging>pom</packaging>
    <version>1.0-SNAPSHOT</version>
    <modules>
        <module>springmvc-01-servlet</module>
        <module>spring-03-hellomvc</module>
        <module>spring-02-practice1</module>
        <module>spring-02-practice2</module>
        <module>springmvc-04-annotation</module>
        <module>springmvc-04-practice1</module>
    </modules>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.2.0.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>servlet-api</artifactId>
            <version>2.5</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.2</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
    </dependencies>
    <build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
    </build>
</project>
```

![image-20201226011358741](img/image-20201226011358741.png)



第3步：配置web.xml，注册DispatcherServlet的servlet

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

第4步：在src/main/resources 下面建立 springmvc-servlet.xml，在这个配置文件需要干如下几件事

​	1、开启包自动扫描

​	2、开启注解驱动，自动加载控制器映射器HandlerMapping和控制器适配器HandlerAdapter

​	3、配置视图解析器

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:context="http://www.springframework.org/schema/context"
      xmlns:mvc="http://www.springframework.org/schema/mvc"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/mvc
       https://www.springframework.org/schema/mvc/spring-mvc.xsd">

	<!-- 自动扫描包，让指定包下的注解生效,由IOC容器统一管理 -->
   <context:component-scan base-package="com.kuang.controller"/>
   <!-- 让Spring MVC不处理静态资源 -->
   <mvc:default-servlet-handler />
   <!--
   支持mvc注解驱动
       在spring中一般采用@RequestMapping注解来完成映射关系
       要想使@RequestMapping注解生效
       必须向上下文中注册DefaultAnnotationHandlerMapping
       和一个AnnotationMethodHandlerAdapter实例
       这两个实例分别在类级别和方法级别处理。
       而annotation-driven配置帮助我们自动完成上述两个实例的注入。
    -->
   <mvc:annotation-driven />

    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="internalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
</beans>
```



第5步: 创建我们的jsp文件夹，在/WEB-INF/下

![image-20201226012221395](img/image-20201226012221395.png)



在视图解析器中我们把所有的视图都存放在/WEB-INF/目录下，这样可以保证视图安全，因为这个目录下的文件，客户端不能直接访问。



第6步：创建Controller,编写一个Java控制类，com.kuang.controller.HelloController, 注意编码规范

```java
@Controller
@RequestMapping("/HelloController")
public class HelloController {
    //真实访问地址: 项目名/HelloController/hello
    @RequestMapping("/hello")
    public String sayHello(Model model){
        //向模型中添加属性msg与值，可以在jsp页面中取出并渲染
        model.addAttribute("msg","hello,Spring MVC");
        //web-inf/jsp/hello.jsp
        return "hello";
    }

}
```



@Controller 是为了让Spring IoC容器初始化时自动扫描到；

@RequestMapping 是为了映射请求路径，这里因为类与方法上都有映射所以访问时应该是 /HelloController/hello

方法中声明Model类型的参数是为了把Action中的数据带到视图中

方法返回的结果是视图的名称hello 加上配置文件中的前后缀就变成了 WEB-INF/jsp/hello.jsp

第7步，创建视图层 hello.jsp

在WEB-INF/jsp目录创建hello.jsp，视图可以直接取出并展示出从Controller带回来的信息，可以通过EL表示取出来的Model中存放的值，或者对象!

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>springmvc-annotation</title>
</head>
<body>
    ${msg}
</body>
</html>
```

第8步 配置tomcat并运行

配置tomcat，开启服务器，访问对应的请求路径



小结：

实现步骤非常简单，分为如下

1、新建一个web项目，子项目

2、导入相关的jar包，配置pom.xml文件

3、编写web.xml,注册我们的DispatcherServlet

4、编写springmvc配置文件

5、接下来就是创建控制类，controller

6、最后完善前端视图和controller之间的对应关系

7、运行测试调试



使用springmvc必须配置三大件

处理映射器，处理器适配器，视图解析器

通常，我们只需要手动配置视图解析器，而处理映射器和处理器适配器只需要开启注解驱动即可<mvc:annotation-driven/>，这样可以省去大段的xml配置文件

和原来的对比

|                       | xml配置方式实现springmvc                                     | Annotation方式实现springmvc                                  |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 创建项目              | 创建一个空白的maven项目                                      | 创建一个空白的maven项目                                      |
| pom.xml               | 相同的类包，都需要添加lib                                    | 相同的类包，都需要添加lib                                    |
| web.xml               | 都需要配置，相同的配置 DispatcherServlet                     | 都需要配置，相同的配置 DispatcherServlet                     |
| springmvc-servlet.xml | 手动配置 处理器映射器 BeanNameUrlHandlerMapping<br />手动配置 处理器适配器 SimpleControllerHandlerAdapter<br /> 手动配置 视图解析器  InternalResourceViewResolver<br /> 手动配置 对应bean id="/hello" 控制器 | 开启自动扫包 <context:component-scan base-package="com.kuang.controller"/><br /> 开启注解驱动 ，自动生成映射器和适配器  <mvc:annotation-driven/> <br /> 开启视图解析器 ，InternalResourceViewResolver |
| Controller            | 实现Controller接口<br />                                     | @Controller<br /><br /> @RequestMapping                      |
|                       |                                                              |                                                              |



## 4.Controller控制器配置总结

控制器 Controller，复杂提供访问应用程序的行为，通常通过接口定义或者注解定义两种方式实现

控制器Controller ： 负责解析用户的请求并将其转换为一个模型

在spring mvc中一个控制器可以包含多个方法

在spring mvc中，对于controller的配置方式有很多种，下面讲述下具体的配置方式



### 1 方式一：实现Controller接口

第1步，新建一个maven子项目，并添加web能力支持，配置项目的lib包内容

![image-20201226130113329](img/image-20201226130113329.png)



第2步，编写web.xml，配置DispatcherServlet, 配置springmvc-servlet.xml,

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

第3步，编写web.xml，配置springmvc-servlet.xml, 配置springmvc-servlet.xml,

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

springmvc-servlet.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
    <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>

    <context:component-scan base-package="com.kuang.controller"/>

    <mvc:annotation-driven/>

    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="internalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>

</beans>
```

第4步 实现Controller，并在springmvc-servlet.xml里面配置一下



```java
import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.Controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class ControllerTest1 implements Controller {
    public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) throws Exception {
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.addObject("msg", "ControllerTest1");
        modelAndView.setViewName("test");
        return modelAndView;
    }
}
```

springmvc-xml.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
    <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>

    <context:component-scan base-package="com.kuang.controller"/>
    <mvc:default-servlet-handler/>
    <mvc:annotation-driven/>

    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="internalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>

    <bean id="/t1" class="com.kuang.controller.ControllerTest1"/>

</beans>
```

第5步，配置tomcat，然后即可进行测试



小结：

1、实现接口controller定义控制器是一个较老的办法

2、缺点是：一个控制器中只有一个方法，如果要多个方法则需要定义多个Controller,定义的方式比较麻烦；

3、我们在springmvc-servlet.xml里面删掉控制器映射器，控制器适配器，一样可以实现，因为springmvc会根据默认的去查找

```xml
springmvc-servlet.xml
    <!--<context:component-scan base-package="com.kuang.controller"/>-->
    <!--<mvc:default-servlet-handler/>-->
    <!--<mvc:annotation-driven/>-->
```





### 2 使用注解方式实现controller

注解的说明：

@Component   代表是spring一个组件

@Service     代表service

@Controller    代表controller

@Repository



@Controller，注解的类，中的所有方法，如果返回值是String,并且有具体的页面可以跳转，那么就会被视图解析器解析！

注解方式必须开启如下三个配置

```xml
<context:component-scan base-package="com.kuang.controller"/>
<mvc:default-servlet-handler/>
<mvc:annotation-driven/>
```





### 3 RequestMapping

用于映射URL到控制器类或一个特定的处理程序方法。可以用于类或者方法上，用于类上，表示类中的所有响应请求的方法都是以该地址作为父路径

我们可以测试下,只在方法上面加RequestMapping

```java
@Controller
public class ControllerTest3 {
    @RequestMapping("/test1")
    public String test(){
        return "test";
    }
}
```

访问路径: http://localhost:8080/项目名/test1

- 同时注解类和方法

```java
@Controller
@RequestMapping("/admin")
public class ControllerTest3 {
    @RequestMapping("/test1")
    public String test(){
        return "test";
    }
}
```

访问路径: http://localhost:8080/项目名/admin/test1

### 4 RestFul风格

RestFul就是一个资源定位和资源操作的风格，不是标准也不是协议，是一种风格，基于这个风格设计的软件可以更加简洁、更有层次、更易于实现缓存的机制

功能

资源：互联网所有的事务都可以抽象为资源

资源操作，使用POST,DELETE,PUT,GET, 使用不同方法对资源进行操作。

分别硬添加、删除、修改、查询

传统是操作资源：通过不同的参数来实现不同的效果!方法很单一，post和get

http://127.0.0.1/item/queryItem.action?id =1 查询，GET

http://127.0.0.1/item/saveItem.action 新增，POST

http://127.0.0.1/item/updateItem.action   更新，POST

http://127.0.0.1/item/deleteItem.action?id =1 删除，GET或者POST



更换为使用RESTFul操作资源，可以通过不同的请求方式来实现不同的效果，例如，请求地址一样，但是功能却不同

http://127.0.0.1/item/1   查询 GET

http://127.0.0.1/item/   新增POST

http://127.0.0.1/item/   更新 PUT

http://127.0.0.1/item/1   删除 DELETE



学习测试一下示例代码

第1步  新建一个类RestFulController

```java
@Controller
public class RestFulController {
    //原来的 http://localhost:8080/add?a=1&b=2
    //RestFul : http://localhost:8080/add/a/b/
    
    @RequestMapping("/add")
    public String test1(int a, int b, Model model){
        int res = a+b;
        model.addAttribute("msg","结果为"+res);
        return "test";
    }
}
```

第2步  在Srping mvc 中可以使用@PathVariable注解，让方法参数的值对应绑定到一个URI模板变量上

```java
@Controller
public class RestFulController {
    //原来的 http://localhost:8080/add?a=1&b=2
    //RestFul : http://localhost:8080/add/a/b/

    @RequestMapping("/add/{a}/{b}")
    public String test1(@PathVariable int a, @PathVariable int b, Model model){
        int res = a+b;
        model.addAttribute("msg","结果为"+res);
        return "test";
    }
}
```

`注意`: 

1、{a}和{b} 需要使用@PathVariable注解的 形参名字

2、http://localhost:8080/add/3/4/ 可以正确调用

3、http://localhost:8080/add/3/demo/  这个就不能正确调用，因为格式要和形参的int格式匹配



第3步  增加对method的支持，

```java
@Controller
public class RestFulController {
    //原来的 http://localhost:8080/add?a=1&b=2
    //RestFul : http://localhost:8080/add/a/b/

    @RequestMapping(path ="/add/{a}/{b}",method= RequestMethod.GET )
    public String test1(@PathVariable int a, @PathVariable int b, Model model){
        int res = a+b;
        model.addAttribute("msg","结果为"+res);
        return "test";
    }
}

```

RequestMapping的参数 ，这里面重点介绍如下几个，

path   or value 就是我们之前的url路径， path ="/add/{a}/{b}"

method  :  这里的method代表前端需要发起的请求，这样就符合了RESTFul method= RequestMethod.GET 



小结：

Spring mvc的@RequestMapping注解能够处理HTTP请求的方法，比如GET PUT DELETE  POST以及PATCH

所有地址栏请求默认都会是 HTTP GET类型的

方法级别的注解变体有如下几个：组合注解

```
@GetMapping   @PostMapping  @PutMapping @DeleteMapping  @PatchMapping
```

@GetMapping就是一个组合注解

他相当于  @ReqeustMapping(mathod=RequestMethod.GET )的一个快捷方式，平时使用的会比较多

```java
@Controller
public class RestFulController {
    //原来的 http://localhost:8080/add?a=1&b=2
    //RestFul : http://localhost:8080/add/a/b/

    @RequestMapping(path ="/add/{a}/{b}",method= RequestMethod.GET )
    public String test1(@PathVariable int a, @PathVariable int b, Model model){
        int res = a+b;
        model.addAttribute("msg","结果为"+res);
        return "test";
    }

    @GetMapping(path ="/add/{a}/{b}")
    public String test2(@PathVariable int a, @PathVariable int b, Model model){
        int res = a+b;
        model.addAttribute("msg","结果为"+res);
        return "test";
    }
    
    @PostMapping(path ="/add/{a}/{b}")
    public String test3(@PathVariable int a, @PathVariable int b, Model model){
        int res = a+b;
        model.addAttribute("msg","结果为"+res);
        return "test";
    }
}
```



思考： 使用路径变量的好处

1、 是路径变得更加简洁

2、获得参数更加方便，框架会自动进行类型转换

3、通过路径变量的类型可以约束访问参数，如果类型不一样，则访问不到对应的请求方法，如这里访问是的路径/commit/1/a，则路径与方法不匹配，则不会是参数转换失败。

###  5.结果跳转ModelAndView

ModelAndView， 根据view的名称,和视图解析器调到指定的页面

页面= {视图解析器前缀}+viewName+{视图解析器后缀}

一个视图解析器

```xml
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="internalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
```

对应Controller类

```java
public class ControllerTest1 implements Controller {
    public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) throws Exception {
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.addObject("msg", "ControllerTest1");
        modelAndView.setViewName("test");
        return modelAndView;
    }
}
```



ServletAPI实现重定向和跳转

通过设置原生的ServletAPI，不需要视图解析器, 我们也能够进行跳转，访问及重定向等操作

1、通过HttpServletResponse进行输出

1、通过HttpServletResponse实现重定向

1、通过HttpServletResponse进行转发

```java
@Controller
public class ForwardController {
    @RequestMapping("/result/t1")
    public void test1(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        resp.getWriter().println("Hello,Spring by Servlet API");
    }
    @RequestMapping("/result/t2")
    public void test2(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        resp.sendRedirect("/index.jsp");
    }
    @RequestMapping("/result/t3")
    public void test3(HttpServletRequest req, HttpServletResponse resp) throws IOException, ServletException {
        //转发
        req.setAttribute("msg","/result/t3");
        req.getRequestDispatcher("/WEB-INF/jsp/test.jsp").forward(req,resp);
    }
}
```

springMVC实现重定向和跳转-无视图解析器



springMVC实现重定向和跳转, 无需视图解析器，测试前，需要将视图解析器注释掉

```java
@Controller
public class ResultSpringMVC {
    @RequestMapping("/rsm/t1")
    //转发
    public String test1() {
        return "/index.jsp";
    }
    @RequestMapping("/rsm/t2")
    //转发二
    public String test2() {
        return "forward:/index.jsp";
    }
    @RequestMapping("/rsm/t3")
    //重定向
    public String test3() {
        return "redirect:/index.jsp";
    }
}

```

spring mvc中，

 "/index.jsp"前面的 /就代表是转发的意思  

"forward:/index.jsp" 就是显示的告诉springmvc转发

这个时候使用的就是原生的HttpServletResponse





springMVC实现重定向和跳转-有视图解析器

重定向，不需要视图解析器，本质就是重新请求一个新地方，所以注意路径的问题

可以重定向到另外一个请求实现

```java
@Controller
public class ResultSpringMVC {
    @RequestMapping("/rsm/t1")
    //转发
    public String test1() {
        return "test";
    }

    @RequestMapping("/rsm/t3")
    //重定向
    public String test3() {
        //重定向
        return "redirect:/index.jsp";
        //return "redirect:hello.do"; //hello.do为另一个请求
    }
}
```

## 5. springmvc处理数据

### 5.1 处理前端请求数据

原来httpservlet获取前端请求数据的方式

request.getParamete("username")



springmvc 处理提交数据

1、提交的域中参数名城和处理的参数名称一致

提交数据为 http://localhost:8080/hello?username=kuang

处理方法:

```java
    @RequestMapping("/test1")
    public String test(String username){

        System.out.println(username);
        return "test";
    }
```

2、提交的域名城和树立的参数名称不一致, 使用@RequestParam

提交数据为 http://localhost:8080/hello?username=kuang

```java
    //@RequestParam("username") username是提交的域的名称。
    @RequestMapping("/test1")
    public String test(@RequestParam("username") String name){

        System.out.println(name);
        return "test";
    }
```

3、前端提交的是一个对象

要求提交的表单和对象的属性名一致，方法参数使用对象即可

1、实体类

```java
public class User {
    private int id;
    private int age;
    private String name;
```

2、提交数据为 http://localhost:8080/mvc03/user?name=kuangshen&id=1&age=20

3、处理方法

```java
    @RequestMapping("/user")
    public String user(User user Model model){
        System.out.println(user);
        //将返回结果传递给前端
        model.setAttribute("msg",name);
        return "hello";
    }
}
```

后台输出 User(id=1,name='kuangshen',age=15)_

1，接手前端用户传递的参数，判断参数名字，假设名字直接在方法上，则可以直接使用

2. 假设传递的是一个对象user，匹配User对象中的字段名，如果名字一致则ok，否则匹配不到

http://localhost:8080/mvc03/user?username=kuangshen&id=1&age=20  如这个请求就无法匹配到，因为username和name不匹配

说明：如果使用对象的话，前端传递的参数和对象名必须一致，否则就是null;



### 5.2 数据显示到前端

1、通过ModelAndView

我们前面一直都是如此，就不用过多解释

```java
public class ControllerTest1 implements Controller {
    public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) throws Exception {
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.addObject("msg", "ControllerTest1");
        modelAndView.setViewName("test");
        return modelAndView;
    }
}
```

2.、通过Model

```java
    @RequestMapping(path ="/add/{a}/{b}",method= RequestMethod.GET )
    public String test1(@PathVariable int a, @PathVariable int b, Model model){
        int res = a+b;
        model.addAttribute("msg","结果为"+res);
        return "test";
    }
```

3、通过ModelMap

```java
    @RequestMapping("/hello")
    public String hello(@RequestParam("username") String name, ModelMap modelMap){
        //封装要显示到视图中的数据
        //相当于req.setAttribute("name",name);
        System.out.println(name);
        return "hello";
    }
```

对于新手而言，简单的来说使用区别就是

Model 知识寥寥几个方法适用于储存数据，简化了新手对于Model对象的操作和理解

ModelMap 继承了LinkedMap, 除了实现了自身的一些方法，同样的继承LinkedMap的方法和特性

ModelAndView 可以在储存数据的同时，可以进行设置返回的逻辑视图，进行控制展示层的的挑战

当然更多的以后开发考虑的跟那更多的是性能和优化，就不能单单仅限于此的了解

请使用80%的时间打好扎实的基础，剩下18%的时间研究框架，2%的时间去学点英文，框架的官方文档永远是最好的教程





>
>
>LinkedHashMap
>
>ModelMap  继承LinkedHashMap， 
>
>Model  精简版

### 5.3 乱码问题

首先我们尝试构造一个乱码

第1步  我们可以在首页编写一个提交的表单

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<form action="${pageContext.request.contextPath}/e/t1" method="post">
    <input type="text" name="username">
    <input type="submit">
</form>
</body>
</html>
```

第2步 后台编写对应的处理类

```java
@Controller
public class EncodingController {
    @RequestMapping("/e/t1")
    public String test(Model model, @RequestParam("username")String name){
        System.out.println("===============/e/t1=========");
        model.addAttribute("msg", name); //获取表单的输入
        return "test"; //跳转到test页面显示输入的值
    }
}
```

第3步 输入中文测试，发现乱码

![image-20201226192120042](img/image-20201226192120042.png)



不得不说，乱码问题是在我们开发中十分常见的问题，也是让我们程序猿比较头大的问题!

以前乱码问题，我们通过过滤器解决，在SpringMVC给我们提供了一个过滤器，可以在web.xml中配置

修改xml文件需要重启服务器

```xml
    <filter>
        <filter-name>encoding</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
    </filter>
    
    <filter-mapping>
        <filter-name>encoding</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```

有些极端情况下，这个过滤器对get的支持不好

修改Tomcat乱码处理方法:

1、修改Tomcat配置，设置编码!

```properties
    <Connector URIEncoding="utf-8" port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443"/>
```



2、自定义过滤器

先编写自定义的过滤器

```java
public class EncodingFilter implements Filter {
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        System.out.println("========执行字符过滤器");
        servletRequest.setCharacterEncoding("utf-8");
        servletResponse.setCharacterEncoding("utf-8");
        servletResponse.setContentType("text/html; charset=utf-8");
        filterChain.doFilter(servletRequest,servletResponse);
    }

    public void destroy() {

    }
}
```

在编辑我们的web.xml注册

```xml
    <!--注册filter-->
    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>com.kuang.filter.EncodingFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```



3、如果各种方式都解决不了，还可用下属的自定义办法

```java
package com.kuang.filter;


import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletRequestWrapper;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.UnsupportedEncodingException;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletRequestWrapper;
import java.util.Map;

/*
* 解决get和post的请求，全部乱码的过滤器
* */
public class GenericEncodingFilter implements Filter {
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws IOException, ServletException {
        //处理response的字符串
        System.out.println("===================doFilter============");
        HttpServletResponse myResp = (HttpServletResponse) resp;
        myResp.setContentType("text/html; charset=UTF-8");

        //转换为与协议相关对象
        HttpServletRequest myReq = (HttpServletRequest) req;
        //对request包装增强
        MyRequest myRequest = new MyRequest(myReq);

        chain.doFilter(myRequest,resp);
    }

    public void destroy() {

    }
}
//自定义request对象，HttpServletRequest的包装类


class MyRequest extends HttpServletRequestWrapper{
    private HttpServletRequest request;
    private boolean flag=true;


    public MyRequest(HttpServletRequest request) {
        super(request);
        this.request=request;
    }

    @Override
    public String getParameter(String name) {
        if(name==null || name.trim().length()==0){
            return null;
        }
        String[] values = getParameterValues(name);
        if(values==null || values.length==0){
            return null;
        }

        return values[0];
    }

    @Override
    /**
     * hobby=[eat,drink]
     */
    public String[] getParameterValues(String name) {
        if(name==null || name.trim().length()==0){
            return null;
        }
        Map<String, String[]> map = getParameterMap();
        if(map==null || map.size()==0){
            return null;
        }

        return map.get(name);
    }

    @Override
    /**
     * map{ username=[tom],password=[123],hobby=[eat,drink]}
     */
    public Map<String,String[]> getParameterMap() {

        /**
         * 首先判断请求方式
         * 若为post  request.setchar...(utf-8)
         * 若为get 将map中的值遍历编码就可以了
         */
        String method = request.getMethod();
        if("post".equalsIgnoreCase(method)){
            try {
                request.setCharacterEncoding("utf-8");
                return request.getParameterMap();
            } catch (UnsupportedEncodingException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
        }else if("get".equalsIgnoreCase(method)){
            Map<String,String[]> map = request.getParameterMap();
            //需要遍历map 修改value的每一个数据的编码
            if(flag){
                for (String key:map.keySet()) {
                    String[] arr = map.get(key);
                    //继续遍历数组
                    for(int i=0;i<arr.length;i++){
                        //编码
                        try {
                            arr[i]=new String(arr[i].getBytes("iso8859-1"),"utf-8");
                        } catch (UnsupportedEncodingException e) {
                            e.printStackTrace();
                        }
                    }
                }
                flag=false;
            }
            return map;
        }

        return super.getParameterMap();
    }

}
```



在做这个的时候，老师在filter的设置 使用了/ ，从而导致乱码无法解决，实际办法是/* 这样才能所有的含jsp被过滤

## 6.springmvc的Json处理

### 6.1 什么是Json

- JSON(JavaScript Object Notation, JS 对象标记) 是一种轻量级的数据交换格式，目前使用特别广泛。
- 采用完全独立于编程语言的**文本格式**来存储和表示数据。
- 简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。
- 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。

在 JavaScript 语言中，一切都是对象。因此，任何JavaScript 支持的类型都可以通过 JSON 来表示，例如字符串、数字、对象、数组等。看看他的要求和语法格式：

- 对象表示为键值对，数据由逗号分隔
- 花括号保存对象
- 方括号保存数组

**JSON 键值对**是用来保存 JavaScript 对象的一种方式，和 JavaScript 对象的写法也大同小异，键/值对组合中的键名写在前面并用双引号 "" 包裹，使用冒号 : 分隔，然后紧接着值：

```java
{"name": "QinJiang"}
{"age": "3"}
{"sex": "男"}
```

很多人搞不清楚 JSON 和 JavaScript 对象的关系，甚至连谁是谁都不清楚。其实，可以这么理解：

JSON 是 JavaScript 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串。

```java
var obj = {a: 'Hello', b: 'World'}; //这是一个对象，注意键名也是可以使用引号包裹的
var json = '{"a": "Hello", "b": "World"}'; //这是一个 JSON 字符串，本质是一个字符串
```

**JSON 和 JavaScript 对象互转**

要实现从JSON字符串转换为JavaScript 对象，使用 JSON.parse() 方法：

```
var obj = JSON.parse('{"a": "Hello", "b": "World"}');
//结果是 {a: 'Hello', b: 'World'}
```

要实现从JavaScript 对象转换为JSON字符串，使用 JSON.stringify() 方法：

```java
var json = JSON.stringify({a: 'Hello', b: 'World'});
//结果是 '{"a": "Hello", "b": "World"}'
```

代码测试

1、新建一个module ，springmvc-05-json ， 添加web的支持

2、在web目录下新建一个 json-1.html ， 编写测试内容

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JSON_秦疆</title>
</head>
<body>

<script type="text/javascript">
    //编写一个js的对象
    var user = {
        name:"秦疆",
        age:3,
        sex:"男"
    };
    //将js对象转换成json字符串
    console.log("------------下面是js对象转换为json字符串---------")
    var str = JSON.stringify(user);
    console.log(str);
    console.log("------------下面是json字符串转换为js对象---------")

    //将json字符串转换为js对象
    var user2 = JSON.parse(str);
    console.log(user2.age,user2.name,user2.sex);

</script>

</body>
</html>
```

3、访问页面，查看控制台输出！

![image-20201227013345801](img/image-20201227013345801.png)

### 6.2 controller实现json



Jackson应该是目前比较好的json解析工具了

当然工具不止这一个，比如还有阿里巴巴的 fastjson 等等,我们这里使用Jackson，使用它需要导入它的jar包；

第1步， 我们需要先导入他的依赖包  jackson

```properties
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-core -->
<dependency>
   <groupId>com.fasterxml.jackson.core</groupId>
   <artifactId>jackson-databind</artifactId>
   <version>2.9.8</version>
</dependency>
```

第2步，配置springmvc需要的配置，web.xml和springmvc-servlet.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
        version="4.0">

   <!--1.注册servlet-->
   <servlet>
       <servlet-name>SpringMVC</servlet-name>
       <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
       <!--通过初始化参数指定SpringMVC配置文件的位置，进行关联-->
       <init-param>
           <param-name>contextConfigLocation</param-name>
           <param-value>classpath:springmvc-servlet.xml</param-value>
       </init-param>
       <!-- 启动顺序，数字越小，启动越早 -->
       <load-on-startup>1</load-on-startup>
   </servlet>

   <!--所有请求都会被springmvc拦截 -->
   <servlet-mapping>
       <servlet-name>SpringMVC</servlet-name>
       <url-pattern>/</url-pattern>
   </servlet-mapping>

   <filter>
       <filter-name>encoding</filter-name>
       <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
       <init-param>
           <param-name>encoding</param-name>
           <param-value>utf-8</param-value>
       </init-param>
   </filter>
   <filter-mapping>
       <filter-name>encoding</filter-name>
       <url-pattern>/</url-pattern>
   </filter-mapping>

</web-app>
```

springmvc-servlet.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:context="http://www.springframework.org/schema/context"
      xmlns:mvc="http://www.springframework.org/schema/mvc"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/mvc
       https://www.springframework.org/schema/mvc/spring-mvc.xsd">

   <!-- 自动扫描指定的包，下面所有注解类交给IOC容器管理 -->
   <context:component-scan base-package="com.kuang.controller"/>

   <!-- 视图解析器 -->
   <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
         id="internalResourceViewResolver">
       <!-- 前缀 -->
       <property name="prefix" value="/WEB-INF/jsp/" />
       <!-- 后缀 -->
       <property name="suffix" value=".jsp" />
   </bean>

</beans>
```

第3步 我们随便编写一个User的实体类，然后去编写我们的测试Controller

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private String name;
    private int age;
    private String sex;
}
```

第4步编写我们的controller，这里使用我们的jackson

这里我们需要两个新东西，一个是@ResponseBody，一个是ObjectMapper对象，我们看下具体的用法



```java
@Controller
public class UserController {
    @RequestMapping("/json1")
    @ResponseBody
    public String json1() throws JsonProcessingException {
        //创建一个jackson的对象映射器，用来解析程序
        ObjectMapper mapper = new ObjectMapper();
        //创建一个对象
        User user = new User("秦僵2号", 3, "男");
        //将我们的对象解析成为json格式
        String str = mapper.writeValueAsString(user);
        //由于@ResponseBody 注解，这里会将str换成json格式返回，十分方便
        return str;
    }
}
```

第5步 配置Tomcat ， 启动测试一下！

http://localhost:8080/json1

![image-20201227014912536](img/image-20201227014912536.png)



### 6.2 解决json乱码的问题



发现出现了乱码问题，我们需要设置一下他的编码格式为utf-8，以及它返回的类型；

解决办法1：通过@RequestMaping的produces属性来实现，修改下代码

```java
//produces:指定响应体返回类型和编码
@RequestMapping(value = "/json1",produces = "application/json;charset=utf-8")
或者
@RequestMapping(path = "/json1",produces = "application/json;charset=utf-8")

```

【注意：使用json记得处理乱码问题】



解决方法2：在springmvc的配置文件解决

上一种方法比较麻烦，如果项目中有许多请求则每一个都要添加，可以通过Spring配置统一指定，这样就不用每次都去处理了！

我们可以在springmvc的配置文件上添加一段消息StringHttpMessageConverter转换配置！

```xml
<mvc:annotation-driven>
   <mvc:message-converters register-defaults="true">
       <bean class="org.springframework.http.converter.StringHttpMessageConverter">
           <constructor-arg value="UTF-8"/>
       </bean>
       <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
           <property name="objectMapper">
               <bean class="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean">
                   <property name="failOnEmptyBeans" value="false"/>
               </bean>
           </property>
       </bean>
   </mvc:message-converters>
</mvc:annotation-driven>
```





在类上直接使用 **@RestController** ，这样子，里面所有的方法都只会返回 json 字符串了，不用再每一个都添加@ResponseBody ！我们在前后端分离开发中，一般都使用 @RestController ，十分便捷！

```java
@RestController
public class UserController {

   //produces:指定响应体返回类型和编码
   @RequestMapping(value = "/json1")
   public String json1() throws JsonProcessingException {
       //创建一个jackson的对象映射器，用来解析数据
       ObjectMapper mapper = new ObjectMapper();
       //创建一个对象
       User user = new User("秦疆1号", 3, "男");
       //将我们的对象解析成为json格式
       String str = mapper.writeValueAsString(user);
       //由于@ResponseBody注解，这里会将str转成json格式返回；十分方便
       return str;
  }

}
```

### 6.4 实现List等集合类型的json输出

在 上面测试基础上，增加一个新的方法

```java
@RequestMapping("/json2")
public String json2() throws JsonProcessingException {

   //创建一个jackson的对象映射器，用来解析数据
   ObjectMapper mapper = new ObjectMapper();
   //创建一个对象
   User user1 = new User("秦疆1号", 3, "男");
   User user2 = new User("秦疆2号", 3, "男");
   User user3 = new User("秦疆3号", 3, "男");
   User user4 = new User("秦疆4号", 3, "男");
   List<User> list = new ArrayList<User>();
   list.add(user1);
   list.add(user2);
   list.add(user3);
   list.add(user4);

   //将我们的对象解析成为json格式
   String str = mapper.writeValueAsString(list);
   return str;
}


```

测试的输出结果

![image-20201227015929096](img/image-20201227015929096.png)

### 6.5 实现日期的管理

```java
@RequestMapping("/json3")
public String json3() throws JsonProcessingException {

   ObjectMapper mapper = new ObjectMapper();

   //创建时间一个对象，java.util.Date
   Date date = new Date();
   //将我们的对象解析成为json格式
   String str = mapper.writeValueAsString(date);
   return str;
}
```

直接使用日期返回无法解决问题，运行的结果如下

![image-20201227020120289](img/image-20201227020120289.png)



解决办法：取消timestamps形式，使用自定义时间格式

```java
@RequestMapping("/json4")
public String json4() throws JsonProcessingException {

   ObjectMapper mapper = new ObjectMapper();

   //不使用时间戳的方式
   mapper.configure(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS, false);
   //自定义日期格式对象
   SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
   //指定日期格式
   mapper.setDateFormat(sdf);

   Date date = new Date();
   String str = mapper.writeValueAsString(date);

   return str;
}
```



### 6.6 抽取为工具类

**如果要经常使用的话，这样是比较麻烦的，我们可以将这些代码封装到一个工具类中；我们去编写下**

```java
package com.kuang.utils;

import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;

import java.text.SimpleDateFormat;

public class JsonUtils {
   
   public static String getJson(Object object) {
       return getJson(object,"yyyy-MM-dd HH:mm:ss");
  }

   public static String getJson(Object object,String dateFormat) {
       ObjectMapper mapper = new ObjectMapper();
       //不使用时间差的方式
       mapper.configure(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS, false);
       //自定义日期格式对象
       SimpleDateFormat sdf = new SimpleDateFormat(dateFormat);
       //指定日期格式
       mapper.setDateFormat(sdf);
       try {
           return mapper.writeValueAsString(object);
      } catch (JsonProcessingException e) {
           e.printStackTrace();
      }
       return null;
  }
}
```

### 6.7 FastJson

fastjson.jar是阿里开发的一款专门用于Java开发的包，可以方便的实现json对象与JavaBean对象的转换，实现JavaBean对象与json字符串的转换，实现json对象与json字符串的转换。实现json的转换方法很多，最后的实现结果都是一样的。

fastjson 的 pom依赖！

```
<dependency>
   <groupId>com.alibaba</groupId>
   <artifactId>fastjson</artifactId>
   <version>1.2.60</version>
</dependency>
```

fastjson 三个主要的类：

**JSONObject  代表 json 对象** 

- JSONObject实现了Map接口, 猜想 JSONObject底层操作是由Map实现的。
- JSONObject对应json对象，通过各种形式的get()方法可以获取json对象中的数据，也可利用诸如size()，isEmpty()等方法获取"键：值"对的个数和判断是否为空。其本质是通过实现Map接口并调用接口中的方法完成的。

**JSONArray  代表 json 对象数组**

- 内部是有List接口中的方法来完成操作的。

**JSON代表 JSONObject和JSONArray的转化**

- JSON类源码分析与使用
- 仔细观察这些方法，主要是实现json对象，json对象数组，javabean对象，json字符串之间的相互转化。



**代码测试，我们新建一个FastJsonDemo 类**

```
package com.kuang.controller;

import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.JSONObject;
import com.kuang.pojo.User;

import java.util.ArrayList;
import java.util.List;

public class FastJsonDemo {
   public static void main(String[] args) {
       //创建一个对象
       User user1 = new User("秦疆1号", 3, "男");
       User user2 = new User("秦疆2号", 3, "男");
       User user3 = new User("秦疆3号", 3, "男");
       User user4 = new User("秦疆4号", 3, "男");
       List<User> list = new ArrayList<User>();
       list.add(user1);
       list.add(user2);
       list.add(user3);
       list.add(user4);

       System.out.println("*******Java对象 转 JSON字符串*******");
       String str1 = JSON.toJSONString(list);
       System.out.println("JSON.toJSONString(list)==>"+str1);
       String str2 = JSON.toJSONString(user1);
       System.out.println("JSON.toJSONString(user1)==>"+str2);

       System.out.println("\n****** JSON字符串 转 Java对象*******");
       User jp_user1=JSON.parseObject(str2,User.class);
       System.out.println("JSON.parseObject(str2,User.class)==>"+jp_user1);

       System.out.println("\n****** Java对象 转 JSON对象 ******");
       JSONObject jsonObject1 = (JSONObject) JSON.toJSON(user2);
       System.out.println("(JSONObject) JSON.toJSON(user2)==>"+jsonObject1.getString("name"));

       System.out.println("\n****** JSON对象 转 Java对象 ******");
       User to_java_user = JSON.toJavaObject(jsonObject1, User.class);
       System.out.println("JSON.toJavaObject(jsonObject1, User.class)==>"+to_java_user);
  }
}
```

这种工具类，我们只需要掌握使用就好了，在使用的时候在根据具体的业务去找对应的实现。和以前的commons-io那种工具包一样，拿来用就好了！



Json在我们数据传输中十分重要，一定要学会使用！

## 7 整合SSM

整合SSM，首先对于环境我们需要具备如下的情况



>IDEA   + MySQL 5.7.19 + Tomcat 9 + Maven 3.6

要求： 需要熟练掌握MySQL数据库，spring,javaweb以及MyBatis知识，简单的前端知识!

###  章节1 准备数据库的环境和测试数据

> 第1步，准备数据库及测试数据

```mysql
create database `ssmbuild`;
use `ssmbuild`;
drop table if exists `books`;

create table `books`(
	`bookID` int(10) not null auto_increment comment '书id',
	`bookName` varchar(100) not null comment '书名',
	`bookCounts` int(11) not null comment '数量',
	`detail` varchar(200) not null comment '描述',
	key `bookID`(`bookID`)
)engine=innodb default charset=utf8

insert into `books`(`bookID`,`bookName`,`bookCounts`,`detail`) 
values (1,'Java',1,'从入门到放弃!'),
(2,'Mysql',10,'从删库到跑步!'),
(3,'Linux',5,'从进门到进牢!'),
(4,'Python',1,'从放弃到忘记!');
```

> 第2步 ： 创建一个普通的Maven项目，项目名称为ssmbuild,并导入一个ssm项目的最基础依赖

对应的pom.xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>top.aigoo</groupId>
    <artifactId>ssmbuild</artifactId>
    <version>1.0-SNAPSHOT</version>

    <!--依赖
        junit
        数据库驱动 mysql-connector-java
        连接池 c3p0
        servlet servlet-api
        jsp jsp-api,
        jstl
        mybatis mybatis,
        mybatis-spring,
        spring  spring-webmvc,
        spring-jdbc
    -->
    <dependencies>
        <!--Junit-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <!--mysql数据库驱动-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version>
        </dependency>
        <!--数据库连接池-->
        <dependency>
            <groupId>com.mchange</groupId>
            <artifactId>c3p0</artifactId>
            <version>0.9.5.2</version>
        </dependency>
        <!--servlet-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>servlet-api</artifactId>
            <version>2.5</version>
        </dependency>
        <!--jsp-->
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.2</version>
        </dependency>
        <!--jstl-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
        <!--mybatis-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.2</version>
        </dependency>
        <!--mybatis-spring-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>2.0.2</version>
        </dependency>
        <!--spring-mvc-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.2.0.RELEASE</version>
        </dependency>
        <!--spring-jdbc-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.2.0.RELEASE</version>
        </dependency>
        <!--lombok-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.12</version>
        </dependency>
    </dependencies>

    <!--静态资源导出-->
    <build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
    </build>
</project>
```

> 第3步 创建项目目录结构  controller,dao,pojo,service , 

至此，我们就准备好了一个空的SSM 项目，使用MAVEN构建，这个项目可以作为后续各个项目的模板

### 章节2 整合mybatis和数据库

> 第1步  在resources 添加 mybaits-config.xml  applicationContext.xml, db.properties，并完善各个配置文件的内容，分别如下

其中 ，mybatis-config.xml的内容

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

</configuration>
```

database.properties的内容为

```properties
jdbc.driver=com.mysql.jdbc.Driver
# 如果使用的是mysql8.0+,需要增加一个时区的配置
jdbc.url=jdbc:mysql://localhost:3306/ssmbuild?useSSL=false&characterEncoding=utf8&useUnicode=True
jdbc.username=root
jdbc.password=123456
```

对于database.properties 注意，

1.我们使用的是jdbc.driver，而不是之前一直使用的名字，这里名字需要记住

2.如果使用mysql8.0以上版本，url里面还需要加上一个时区的配置



applicationContext.xml的干净内容如下

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    
</beans>
```

> 第2步 ，配置我们的mybatis，这里我们仅使用setting 和 alias

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--配置数据源，交由spring去做,也就是前面学习的spring-mybatis整合知识-->
    <typeAliases >
        <package name="com.kuang.pojo"/>
    </typeAliases>
    <mappers>
        <mapper class="com.kuang.dao.BookMapper"/>
    </mappers>
</configuration>
```



> 第3步，准备mybatis的工作环境，我们需要分别针对数据库的books表，创建对应的实例，及对应的BookMapper和BookMapper.xml
>
> 去com.kuang.pojo创建实体类Books, 记住保证字段和数据库字段一模一样

a) 创建和数据库字段一一对应的实体类  Books

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Books {
    private int bookID;
    private String bookName;
    private int bookCounts;
    private String detail;
}
```

b）编写对pojo的接口操作  com.kuang.dao.BookMapper.java

```java
package com.kuang.dao;

import com.kuang.pojo.Books;
import org.apache.ibatis.annotations.Param;

import java.util.List;

public interface BookMapper {
    //增加一本书
    int addBook(Books books);
    //删除一本书
    int deleteBookById(@Param("bookId") int id);
    //更新一本书
    int updateBook(Books books);
    //根据id查询一本书
    Books queryBookById(@Param("bookId") int id);
    //查询全部的书
    List<Books> queryAllBook();
}
```

c) 编写 对BookMapper的mybatis实现， com.kuang.dao.BookMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.kuang.dao.BookMapper">
    <!--增加一本书-->
    <insert id="addBook" parameterType="Books">
      insert into ssmbuild.books(bookName,bookCounts,detail)
      values (#{bookName},#{bookCounts},#{detail});
    </insert>
    <!--删除一本书-->
    <delete id="deleteBookById" parameterType="int">
        delete  from ssmbuild.books where bookID=#{bookId};
    </delete>
    <!--更新一本书-->
    <update id="updateBook" parameterType="Books">
       update ssmbuild.books
       set bookName=#{bookName},bookCounts=#{bookCounts},detail=#{detail}
       where bookID =#{bookID}
    </update>
    <!--根据id查询一本书-->
    <select id="queryBookById" resultType="Books">
        select * from ssmbuild.books where bookID=#{bookId};
    </select>
    <!--查询全部的书-->
    <select id="queryAllBook" resultType="Books">
        select * from ssmbuild.books;
    </select>
</mapper>
```

d) 将编写好的BooksMapper注册到mybatis-config.xml中

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
	......
    <mappers>
        <mapper class="com.kuang.dao.BookMapper"/>
    </mappers>
    ......
</configuration>
```

e) 接着，我们完善service层， 首先编写 UserService.java接口

```java
package com.kuang.service;

import com.kuang.pojo.Books;
import org.apache.ibatis.annotations.Param;

import java.util.List;

public interface BookService {
    //增加一本书
    int addBook(Books books);
    //删除一本书
    int deleteBookById(int id);
    //更新一本书
    int updateBook(Books books);
    //根据id查询一本书
    Books queryBookById(int id);
    //查询全部的书
    List<Books> queryAllBook();
}

```

f) 接下来，我们在实现我们的UserService ,com.kuang.service.BookServiceImpl

```java
public class BookServiceImpl implements BookService{
    //service 调用dao层
    private BookMapper bookMapper;

    public void setBookMapper(BookMapper bookMapper) {
        this.bookMapper = bookMapper;
    }

    public int addBook(Books books) {
        return bookMapper.addBook(books);
    }

    public int deleteBookById(int id) {
        return bookMapper.deleteBookById(id);
    }

    public int updateBook(Books books) {
        return bookMapper.updateBook(books);
    }

    public Books queryBookById(int id) {
        return bookMapper.queryBookById(id);
    }

    public List<Books> queryAllBook() {
        return bookMapper.queryAllBook();
    }
}
```

上述工作都是为了完成mybatis层，至此，我们就将mybatis的整合全部完成了， 接下来 我们继续spring层的整合

### 章节3 spring-dao整合业务层接口及服务

第1步，我们先建立一个spring-dao.xml的配置文件，作为整合配置文件，这个配置文件至少要定义如下功能

​	a) 关联数据库配置+数据源

​	b)sqlSessionBeanFactory

​	c)整合sqlSession

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">
    <!--1.关联数据库配置-->
    <context:property-placeholder location="classpath:database.properties"/>
    <!--2.datasource
        dbcp 半自动化操作，不能自动连接 c3p0 自动化操作，自动化加载配置文件，并且可以自动配置到对象中 druid hikari
    -->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="driverClass" value="${jdbc.driver}"/>
        <property name="jdbcUrl" value="${jdbc.url}"/>
        <property name="user" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
        <!--c3p0连接池私有属性-->
        <property name="maxPoolSize" value="30"/>
        <property name="minPoolSize" value="10"/>
        <!--关闭连接后不自动commit-->
        <property name="autoCommitOnClose" value="false"/>
        <!--获取连接超时时间-->
        <property name="checkoutTimeout" value="10000"/>
        <!--获取连接失败的重试次数-->
        <property name="acquireRetryAttempts" value="2"/>
    </bean>
    <!--3.sqlSessionFactory-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <!--绑定mybatis配置文件-->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
    </bean>
    <!--4.新知识: 这里不用sqlSessionTemplate，采用另一种方法 配置DAO接口扫描包 动态实现UserMapper可以注入Spring-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <!--step 1.动态注入sqlSessionFactory-->
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
        <!--step 2. 扫描dao包-->
        <property name="basePackage" value="com.kuang.dao"/>
    </bean>
</beans>
```



### 章节3.spring-service整合业务层接口及服务

在spring这一层，我们主要是扫描包，将业务注入到spring，声明事务，并执行aop切入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
    <!--step 1. 扫描service下的包-->
    <context:component-scan base-package="com.kuang.service"/>
    <!--step 2. 将我们的所有业务类注入到spring 可以通过配置或者注解实现 因为刚讲springmvc 这里用配置实现 -->
    <bean id="BookServiceImpl" class="com.kuang.service.BookServiceImpl">
        <property name="bookMapper" ref="bookMapper"/>
    </bean>
    <!--step 3.声明式事务配置-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <!--注入数据源-->
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <!--step 4 aop事务支持-->

</beans>
```



### 章节4.spring-mvc整合controller层接口及服务

step1， 在idea增加web项目的支持

在项目点击右键---Add  FrameWorkSupport ，选择web支持

step2 . 配置我们的web.xml，后续请求有DispatcherServlet接管，并配置过滤器和Session等信息

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--step 1 .DispathcerServlet-->
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!--整合spring-mvc配置-->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:spring-mvc.xml</param-value>
        </init-param>
        <!--和服务器一起启动-->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

    <!--Step 2 乱码过滤-->
    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    <!--step 3 配置session过期时间-->
    <session-config>
        <session-timeout>60</session-timeout>
    </session-config>
</web-app>
```

step 3. 完成web.xml的配置，我们需要去调整spring-mvc.xml的配置了

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <!--1.注解驱动-->
    <mvc:annotation-driven/>
    <!--2.静态资源过滤-->
    <mvc:default-servlet-handler/>
    <!--3.扫描包 扫描controller-->
    <context:component-scan base-package="com.kuang.controller"/>
    <!--4.视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
</beans>
```

同时，我们配置视图解析器时，就去web/WEB-INF/目录下面把jsp文件夹创建起来

至此，我们就将mybatis+spring+springMVC整合到了一起!  对应配置文件之间关系如下图

![image-20201228211018216](img/image-20201228211018216.png)



### 章节5.测试 实现前台页面 及优化

step1 . 编写一个Controller功能，实现查询图书列表

```java
@Controller
@RequestMapping("/book")
public class BooksController {
    /*
     service层持有Dao层
    *Controller层持有Service层
    * */
    @Autowired
    @Qualifier("BookServiceImpl")
    private BookService bookService;
    /*查询全部书籍并且返回到一个书籍列表页面*/
    @RequestMapping("/allbook")
    public String list(Model model){
        List<Books> books = bookService.queryAllBook();
        model.addAttribute("list", books);
        return "allBook";
    }

}
```

此处需要记住：

​	1 service层持有dao层

​	2、controller层持有service层

Step 2 .在web/WEB-INF/jsp/创建hello.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>allBook</title>
</head>
<body>
    <h1>展示全部书籍列表</h1>
</body>
</html>
```



step3 在测试可以跳转，我们引入bootstrap优化效果

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>allBook</title>
    <%--bootstrap美化界面--%>
    <!-- 新 Bootstrap 核心 CSS 文件 -->
    <link href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <!-- jQuery文件。务必在bootstrap.min.js 之前引入 -->
    <script src="https://cdn.staticfile.org/jquery/2.1.1/jquery.min.js"></script>
    <!-- 最新的 Bootstrap 核心 JavaScript 文件 -->
    <script src="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/js/bootstrap.min.js"></script>
</head>
<body>
<div class="container">
    <div class="row clearfix">
        <div class="col-md-12 column">
            <div class="page-header">
                <h1><small class="center">书籍列表-显示所有书籍列表</small></h1>
            </div>
        </div>
    </div>

    <div class="row clearfix">
        <div class="col-md-12 column">
            <table class="table table-hover table-striped">
                <thead>
                    <tr>
                        <th>书籍编号</th>
                        <th>书籍名称</th>
                        <th>书籍数量</th>
                        <th>书籍详情</th>
                    </tr>
                </thead>
                <%--书籍从数据库中查询出来，从这个list中遍历出来 foreach--%>
                <tbody>
                    <c:forEach var="book" items="${list}">
                        <tr>
                            <td>${book.bookID}</td>
                            <td>${book.bookName}</td>
                            <td>${book.bookCounts}</td>
                            <td>${book.detail}</td>
                        </tr>
                    </c:forEach>
                </tbody>
            </table>
        </div>
    </div>
</div>
</body>
</html>
```



### 7.2 添加书籍功能



step 1 ，我们需要有一个新增图书的按钮,在allBook.jsp里面，增加一个新增图书按钮

```html
        <%--操作按钮--%>
        <div class="row">
            <div class="col-md-4 column">
                <%--toAddPaper--%>
                <a class="btn btn-primary" href="${pageContext.request.contextPath}/book/toAddBookPage">新增书籍</a>
            </div>
        </div>
```

step 2. 编写跳转新增图书页面的功能

```java
public class BooksController {
 	.....
         /*跳转到增加书籍页面*/
    @RequestMapping("/toAddBookPage")
    public String toAddPaper(Model model) {
        return "addBook";
    }
    ....
}
```

step 3. 在/web-inf/jsp/下面新建一个addBook.jsp页面，可以添加图书

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>allBook</title>
    <%--bootstrap美化界面--%>
    <!-- 新 Bootstrap 核心 CSS 文件 -->
    <link href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <!-- jQuery文件。务必在bootstrap.min.js 之前引入 -->
    <script src="https://cdn.staticfile.org/jquery/2.1.1/jquery.min.js"></script>
    <!-- 最新的 Bootstrap 核心 JavaScript 文件 -->
    <script src="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/js/bootstrap.min.js"></script>
</head>
<body>
<div class="container">
    <div class="row clearfix">
        <div class="col-md-12 column">
            <div class="page-header">
                <h1><small class="center">新增书籍</small></h1>
            </div>
        </div>
    </div>
    <%--书籍表单--%>
    <form class="form-horizontal" action="${pageContext.request.contextPath}/book/addBook" method="post">
        <div class="form-group">
            <label for="inputEmail3" class="col-sm-2 control-label">书籍名称</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" id="inputEmail3" placeholder="书籍名称" name="bookName" required>
            </div>
        </div>

        <div class="form-group">
            <label for="bkcount" class="col-sm-2 control-label">书籍数量</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" id="bkcount" placeholder="书籍数量" name="bookCounts" required>
            </div>
        </div>

        <div class="form-group">
            <label for="bkdetail" class="col-sm-2 control-label">书籍详情</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" id="bkdetail" placeholder="书籍详情" name="detail" required>
            </div>
        </div>

        <div class="form-group">
            <input type="submit" value="添加" class="form-control btn btn-primary">
        </div>
    </form>

</div>
</body>
</html>
```

注意点

1、 name必须和实体类Books属性字段一一匹配，不然后端读取不到

### 7.3 修改删除书籍

step 1. 首先，在书籍列表，增加 修改删除的连接, 我们要实现先能跳进到修改页面

```java
<tbody>
    <c:forEach var="book" items="${list}">
        <tr>
        <td>${book.bookID}</td>
        <td>${book.bookName}</td>
        <td>${book.bookCounts}</td>
        <td>${book.detail}</td>
        <td>
        <a href="${pageContext.request.contextPath}/book/toUpdateBookPage?id=${book.bookID}">修改</a> &nbsp; | &nbsp;
		<a href="#">删除</a>
        </td>
    </tr>
    </c:forEach>
</tbody>
```



step2 . 进入/WEB-INF/jsp/，添加我们的jsp页面  updateBook.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>updateBook</title>
    <%--bootstrap美化界面--%>
    <!-- 新 Bootstrap 核心 CSS 文件 -->
    <link href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <!-- jQuery文件。务必在bootstrap.min.js 之前引入 -->
    <script src="https://cdn.staticfile.org/jquery/2.1.1/jquery.min.js"></script>
    <!-- 最新的 Bootstrap 核心 JavaScript 文件 -->
    <script src="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/js/bootstrap.min.js"></script>
</head>
<body>

<div class="container">
    <div class="row clearfix">
        <div class="col-md-12 column">
            <div class="page-header">
                <h1><small class="center">修改书籍</small></h1>
            </div>
        </div>
    </div>
    <%--书籍表单--%>
    <form class="form-horizontal" action="${pageContext.request.contextPath}/book/updateBook" method="post">
        <%--出现问题：我们提交了修改sql的请求，但是修改失败，初次考虑，是事务问题，配置完毕事务，依旧失败--%>
        <%--看一下sql语句，能否执行成功:sql执行失败，修改未完成--%>
            <%--前端传递隐藏域--%>
        <input type="hidden" name="bookID", value="${books.bookID}">
        <div class="form-group">
            <label for="inputEmail3" class="col-sm-2 control-label">书籍名称</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" id="inputEmail3" placeholder="书籍名称" name="bookName" required value="${books.bookName}">
            </div>
        </div>

        <div class="form-group">
            <label for="bkcount" class="col-sm-2 control-label">书籍数量</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" id="bkcount" placeholder="书籍数量" name="bookCounts" required value="${books.bookCounts}">
            </div>
        </div>

        <div class="form-group">
            <label for="bkdetail" class="col-sm-2 control-label">书籍详情</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" id="bkdetail" placeholder="书籍详情" name="detail" required value="${books.detail}">
            </div>
        </div>

        <div class="form-group">
            <input type="submit" value="修改" class="form-control btn btn-primary">
        </div>
    </form>

</div>

</body>
</html>
```



Step3.先在controller里面，添加一个跳转到修改页面的功能

```java
/*跳转到修改书籍页面*/
@RequestMapping("/toUpdateBookPage")
public String toUpdatePaper(Model model, int id) {
    Books books = bookService.queryBookById(id);
    model.addAttribute("books",books);
    return "updateBook";
}
```

step4 . 在controller，编写处理修改删除书籍的信息



```java
/*修改书籍*/
@RequestMapping("/updateBook")
public String updateBook(Model model, Books book) {
    System.err.println("updateBook=>"+book);

    bookService.updateBook(book);
    return "redirect:/book/allbook";
}
```

在做这个的时候碰到两个错误

1、BookMapper.xml里面配置错误

```xml
    <!--/*修改一本书*/-->
    <update id="updateBook" parameterType="books">
        update ssmbuild.books
        set bookName =#{bookName},bookCounts=#{bookCounts},detail=#{detail}
        where bookID=#{bookID};
    </update>
刚开始   where bookID=#{bookId}; 导致一直报错
```

2.添加事务处理器

```xml
    <!--step 3.声明式事务配置-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <!--注入数据源-->
        <property name="dataSource" ref="dataSource"/>
    </bean>
    <!--结合AOP实现事务的织入，配置事务通知-->
    <tx:advice id="txAdvice"  transaction-manager="transactionManager" >
        <tx:attributes>
            <tx:method name="add" propagation="REQUIRED"/>
            <tx:method name="delete" propagation="REQUIRED"/>
            <tx:method name="update" propagation="REQUIRED"/>
            <tx:method name="query" read-only="true"/>
            <tx:method name="*" propagation="REQUIRED"/>
        </tx:attributes>
    </tx:advice>
    <!--step 4 aop事务支持-->
    <aop:config>
        <aop:pointcut id="txPointCut" expression="execution(* com.kuang.dao.*.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"/>
    </aop:config>
```

3. 我们修改页面，前台未传递BookID,导致无法更新

4. 配置mybatis-conf.xml的日志， 不能有空格，刚开始写的有空格，导致启动报错

   ```
   <settings>
       <setting name="logImpl" value="STDOUT_LOGGING"/>
   </settings>
   ```



> 删除图书，我们使用restFule风格	

step1 controller里面

```java
    /*删除数据*/
    /*复习一下restFul风格*/
    //@RequestMapping("/deleteBook")
    @RequestMapping("/deleteBook/{bookId}")
    public String deleteBook(@PathVariable("bookId") int id){
        bookService.deleteBookById(id);
        return "redirect:/book/allbook";
    }
```

step2 在前端调用里面

```jsp
 <a href="${pageContext.request.contextPath}/book/deleteBook/${book.bookID}">删除</a>
```

### 7.4 做一个搜索功能

step 1 , 需要做搜索，我们就先把搜索jsp页面整合进allBook.jsp

```jsp
    <div class="row clearfix">
        <div class="col-md-12 column">
            <div class="page-header">
                <h1><small class="center">书籍列表-显示所有书籍列表</small></h1>
            </div>
        </div>
        <%--操作按钮--%>
        <div class="row">
            <div class="col-md-4 column">
                <%--toAddPaper--%>
                <a class="btn btn-primary" href="${pageContext.request.contextPath}/book/toAddBookPage">新增书籍</a>
            </div>
            <div class="col-md-4 column pull-right">
                <%--查询书籍--%>
                    <form action="${pageContext.request.contextPath}/book/queryBook" method="post" class="form-inline pull-right ">
                        <label class="sr-only" for="inlineFormInputName2">Name</label>
                        <input type="text" class="form-control mb-2 mr-sm-2" id="inlineFormInputName2" name="queryBookName" value="${queryBookName}" placeholder="请输入书籍名称">
                        <button type="submit" class="btn btn-primary mb-2">搜索</button>
                    </form>
            </div>
        </div>
    </div>
```



step 2 , 我们因为之前没有这个功能，所以我们需要从底层开始，先编写我们的BookMapper.java

```java
public interface BookMapper {
    .....
	/*通过书名查询图书*/
    List<Books> queryBookByName(@Param("bookName") String bookName);
    .....
}
```

step 3. 接着我们去设计我们的BookMapper.xml文件

```xml
<!--/*通过书名查询书籍
    复习回忆mybatis里面的 模糊查询，动态sql知识*/-->
<select id="queryBookByName" resultType="books">
    select * from ssmbuild.books
    <where>
        <if test="bookName!=null">
            bookName like "%"#{bookName}"%"
        </if>
    </where>
</select>
```

step 4. 开始完善我们的BookService.java

```java
.....
/*通过书名查询图书*/
List<Books> queryBookByName( String bookName);
.....
```

step 5. 实现我们的BookServiceImpl.java

```java
......
public List<Books> queryBookByName(String bookName) {
    return bookMapper.queryBookByName(bookName);
}
.....
```

step 6. 最后实现我们Controller事件

```java
/*通过名字查询书籍*/
@RequestMapping("/queryBook")
public String queryBook(String queryBookName,Model model){
    List<Books> booksList = bookService.queryBookByName(queryBookName);
    model.addAttribute("list", booksList);
    model.addAttribute("queryBookName",queryBookName);
    return "allBook";
}
```



这个案例，复习了mybatis.xml的 模糊查询和动态sql语句。

## 8 springmvc:Ajax技术

AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。

AJAX 不是新的编程语言，而是一种使用现有标准的新方法。

AJAX 是与服务器交换数据并更新部分网页的艺术，在不重新加载整个页面的情况下。

Google Suggest

在 2005 年，Google 通过其 Google Suggest 使 AJAX 变得流行起来。

Google Suggest 使用 AJAX 创造出动态性极强的 web 界面：当您在谷歌的搜索框输入关键字时，JavaScript 会把这些字符发送到服务器，然后服务器会返回一个搜索建议的列表。



### 8.1 Ajax请求的5个步骤

1、建立XMLHttpRequest对象；

2、设置回调函数；

3、使用open方法与服务器建立链接；

4、向服务器发送数据；

5、在回调函数中针对不同的响应状态进行处理；

Ajax ：异步无刷新请求, 示例代码如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>iframe</title>
    <script>
        function a1(){
            //所有的值，变量，提前获取
            var url = document.getElementById("url").value;
            console.log(url)
            // document.getElementById("iframe1").src="http://www.baidu.com";
            document.getElementById("iframe1").src=url;
        }
    </script>
</head>
<body>
    <div>
        <p>请输入地址:</p>
        <p>
            <input type="text" id="url" value="http://www.baidu.com" >
            <input type="submit" value="提交" onclick="a1()">
        </p>

    </div>
    <div>
        <iframe id="iframe1" src="" frameborder="0" style="width: 100% ;height:400px"></iframe>
    </div>
</body>
</html>
```

利用ajax可以做到：

- 注册时，输入用户名自动检测用户是否已经存在。
- 登陆时，提示用户名密码错误
- 删除数据行时，将行ID发送到后台，后台在数据库中删除，数据库删除成功后，在页面DOM中将数据行也删除。
- ....等等



> 配置环境要先确认环境可以跑起来，再往下写功能!



### 8.2 Jquery使用

JQuery是一个库，里面是一系列js函数

下载地址：https://code.jquery.com/jquery-3.5.1.js

![image-20201230135733424](img/image-20201230135733424.png)

通过 jQuery AJAX 方法，您能够使用 HTTP Get 和 HTTP Post 从远程服务器上请求文本、HTML、XML 或 JSON – 同时您能够把这些外部数据直接载入网页的被选元素中。

jQuery 不是生产者，而是大自然搬运工。

jQuery Ajax本质就是 XMLHttpRequest，对他进行了封装，方便调用！

```
jQuery.ajax(...)
      部分参数：
            url：请求地址
            type：请求方式，GET、POST（1.9.0之后用method）
        headers：请求头
            data：要发送的数据
    contentType：即将发送信息至服务器的内容编码类型(默认: "application/x-www-form-urlencoded; charset=UTF-8")
          async：是否异步
        timeout：设置请求超时时间（毫秒）
      beforeSend：发送请求前执行的函数(全局)
        complete：完成之后执行的回调函数(全局)
        success：成功之后执行的回调函数(全局)
          error：失败之后执行的回调函数(全局)
        accepts：通过请求头发送给服务器，告诉服务器当前客户端可接受的数据类型
        dataType：将服务器端返回的数据转换成指定类型
          "xml": 将服务器端返回的内容转换成xml格式
          "text": 将服务器端返回的内容转换成普通文本格式
          "html": 将服务器端返回的内容转换成普通文本格式，在插入DOM中时，如果包含JavaScript标签，则会尝试去执行。
        "script": 尝试将返回值当作JavaScript去执行，然后再将服务器端返回的内容转换成普通文本格式
          "json": 将服务器端返回的内容转换成相应的JavaScript对象
        "jsonp": JSONP 格式使用 JSONP 形式调用函数时，如 "myurl?callback=?" jQuery 将自动替换 ? 为正确的函数名，以执行回调函数
```



我们来做个简单的例子测试，使用最原始的HttpServletResponse处理，。最简单，最通用

step1 配置web.xml和springmvc的配置文件，【记得静态资源过滤和注解驱动需要配置上】

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:context="http://www.springframework.org/schema/context"
      xmlns:mvc="http://www.springframework.org/schema/mvc"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/mvc
       https://www.springframework.org/schema/mvc/spring-mvc.xsd">

   <!-- 自动扫描指定的包，下面所有注解类交给IOC容器管理 -->
   <context:component-scan base-package="com.kuang.controller"/>
   <mvc:default-servlet-handler />
   <mvc:annotation-driven />

   <!-- 视图解析器 -->
   <beanclass="org.springframework.web.servlet.view.InternalResourceViewResolver"
         id="internalResourceViewResolver">
       <!-- 前缀 -->
       <property name="prefix" value="/WEB-INF/jsp/" />
       <!-- 后缀 -->
       <property name="suffix" value=".jsp" />
   </bean>

</beans>
```

step2  编写index.jsp, 响应的js代码，要导入jquery，可以使用在线的，也可以下载导入

```jsp
<script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
<script src="${pageContext.request.contextPath}/statics/js/jquery-3.1.1.min.js"></script>
```





```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>$Title$</title>
    <script src="${pageContext.request.contextPath}/statics/js/jquery-3.5.1.js"></script>
    <script>
        function test2() {
            $.post({
                url: "${pageContext.request.contextPath}/test2",
                data: {"name": $("#username").val()},
                success: function (data,status) {
                    console.log("data="+data);
                    console.log("status="+status);
                }
            });
        }

    </script>
</head>
<body>
<%--失去焦点的时候，发起一个请求(携带信息)到后台--%>
用户名 : <input type="text" id="username" onblur="test2()">
</body>
</html>
```

step3,后台接口Controller, 编写一个 AjaxTestController

```java
package com.kuang.controller;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@RestController
public class AjaxTestController {
    @RequestMapping("/test1")
    public String test1() {
        return "Hello";
    }

    @RequestMapping("/test2")
    public void test2(String name, HttpServletResponse response) throws IOException {

        System.out.println("test2:param=>" + name);

        if ("kuangshen".equals(name)) {
            response.getWriter().print("true");
        } else {
            response.getWriter().print("false");
        }
    }
}
```

step4 .启动tomcat测试！打开浏览器的控制台，当我们鼠标离开输入框的时候，可以看到发出了一个ajax的请求！是后台返回给我们的结果！测试成功！



ajax原理

![image-20201230152226681](img/image-20201230152226681.png)

学习ajax需要 html+css(略懂)+js(精通，超级熟练)

js需要熟练掌握":" 

​	= 函数 闭包

​	= 面向对象

​	= 操作DOM元素(id name tag  create  remove)

​	=操作BOM元素(window时间，document事件)

​	ES6 import require 



### 8.3 模拟一个例子，展示json数据

step1 先完善一个pojo 实体类 User.java

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
public class User implements Serializable {
    private String name;
    private int age;
    private String sex;
}
```

step2 . 完善controller

```java
@RequestMapping("/test3")
public List<User> test3(){

    System.out.println("test3:param=>");
    List<User> userList = new ArrayList<User>();
    //添加数据
    userList.add(new User("狂神说java",1,"男"));
    userList.add(new User("狂神说前团",1,"女"));
    userList.add(new User("狂神说运维",1,"男"));
    userList.add(new User("狂神说测试",1,"男"));
    userList.add(new User("狂神说产品",1,"男"));

    return userList;
}
```

step3 编写我们的前端页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <script src="${pageContext.request.contextPath}/statics/js/jquery-3.5.1.js"></script>
    <script>
        $(document).ready(function (){
            /*点击按钮*/
            $("#btn").click(function () {
                console.log("test3.jsp 点击了!")
                /*
                * $.post(url,data(可以省略), function(){});
                * */
                $.post("${pageContext.request.contextPath}/test3",function (data){
                    console.log("data==>"+data);
                    /*动态增加节点*/
                    var html = "";
                    for (let i = 0; i < data.length; i++) {
                        html+="<tr>"+
                            "<td>"+data[i].name+"</td>" +
                            "<td>"+data[i].age+"</td>" +
                            "<td>"+data[i].sex+"</td>" +
                            "</tr>"
                    }
                    $("#content").html(html)
                });


            });
        })

    </script>
</head>
<body>
<input type="button" value="加载数据" id="btn">
<table>
    <thead>
    <tr>
        <td>姓名</td>
        <td>年龄</td>
        <td>性别</td>
    </tr>
    </thead>
    <tbody id="content">
        <%--数据，后台获取--%>

    </tbody>
</table>
</body>
</html>
```



### 8.4 模拟异步用户登录

我们模拟用户登录，当用户输入完信息，失去焦点，就会请求后台验证，如果符合用户名，则返回ok ，不符合，则返回"用户名错误"

step 1. 先设计我们的Controller

```java
    @RequestMapping("/test4")
    public String test4(String name, String pwd){
        String msg="";
        if (name!= null){
            //admin这些数据库应该在数据库中查询
            if ("admin".equals(name)){
                msg = "ok";
            }else {
                msg="用户名有误!";
            }
        }

        if (pwd!= null){
            //admin这些数据库应该在数据库中查询
            if ("123456".equals(pwd)){
                msg = "ok";
            }else {
                msg="密码有误!";
            }
        }
        return msg;
    }
```

step 2. 再去设计我们的jsp站点  login.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <script src="${pageContext.request.contextPath}/statics/js/jquery-3.5.1.js"></script>

    <script>
        function test4() {
            $.post({
                url: "${pageContext.request.contextPath}/test4",
                data: {"name": $("#name").val()},
                success: function (data) {
                    //console.log(data)
                    if (data.toString()==='ok'){
                        $("#userInfo").css("color","green");
                    }else {
                        $("#userInfo").css("color","red");
                    }
                    $("#userInfo").html(data);
                }
            })
        }

        function test5() {
            $.post({
                url: "${pageContext.request.contextPath}/test4",
                data: {"pwd": $("#pwd").val()},
                success: function (data) {
                    //console.log(data)
                    if (data.toString()==='ok'){
                        $("#pwdInfo").css("color","green");
                    }else {
                        $("#pwdInfo").css("color","red");
                    }
                    $("#pwdInfo").html(data);
                }
            })
        }
    </script>
</head>
<%--成功就在info里面追加成功，失败追加失败--%>
<body>
<p>
    用户名:<input type="text" id="name" onblur="test4()">
    <span id="userInfo"></span>
</p>
<p>
    密码:<input type="text" id="pwd" onblur="test5()">
    <span id="pwdInfo"></span>
</p>
</body>
</html>
```

这样就实现了我们的需求

知识点：

1、前端向后端传值，前端的传值参数名字，和后端处理事件的方法 形参名字要一一对应，如果名字不对应，会取不到值

2、通过msg 直接return, 如果用户名存在就返回Ok, 如果不存在就返回错误信息

3、在jsp，为了展示错误信息，用span元素去承载，

4、对两个input设计对应的js，用户焦点失去，就会触发js

5、在js中，通过对msg信息判断，来确认前端怎么处理

## 9.springmvc 拦截器

### 9.1 拦截器的一个概念

什么是拦截器**

springmvc的处理器拦截器类似Servlet开发中的过滤器Filter，用于对处理器金星预处理和后处理，开发者可以自己定义一些拦截器来进行特定的功能。

过滤器和拦截器有的区别：

拦截器是和AOP思想的具体应用。

过滤器 Filter：

servlet规范中的一部分，任何java web工程都可以使用

在url-pattern中配置了/* 之后，可以对所有要访问的资源进行过滤拦截



拦截器：

拦截器是springmvc框架自己的，只有使用了springmvc框架的工程才能使用

拦截器只会拦截访问的控制器方法，如果访问的是jsp/html/css/image/js 是不会进行拦截的



**如何使用拦截器**

想要使用自定义拦截器，必须实现HandlerIntercepter接口

1、新建一个Module,springmvc-07-interceptor,添加web支持，

2、配置web.xml和springmvc-servlet.xml

3、编写一个拦截器

```java
public class MyInterceptor implements HandlerInterceptor {
    //return true 会执行下一个拦截器，放行;
    //return false 拦截不放行
    /*在请求处理的方法之前执行*/
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("---------MyInterceptor 处理前----------");
        return true;
    }
    /*在请求处理方法执行之后执行*/
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("---------MyInterceptor 处理后----------");

    }
    /*在dispatcherServlet处理后执行，做清理工作*/
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("---------MyInterceptor 清理----------");
    }
}
```

我们如果实现拦截器，可以实现 HandlerInterceptor， 实现方法 preHandle就可以

4、在spring-mvc.xml配置文件中配置拦截器

```xml
    <!--关于拦截器配置-->
    <mvc:interceptors>
        <!--可以添加多个拦截器-->
        <mvc:interceptor>
            <!--"  /**   包括路径及其子路径
             /admin/*   拦截的是/admin/adsa等等这种， /admin/add/user不会被拦截 
             /admin/**  拦截的是/admin/下的所有-->
            <mvc:mapping path="/**"/>
    
            <!--bean配置的就是拦截器-->
            <bean class="com.kuang.config.TestInterceptor"/>
        </mvc:interceptor>
       <!-- 登录拦截器-->
        <!--测试拦截器-->
        <mvc:interceptor>
            <mvc:mapping path="/inter/*"/>
            <bean class="com.kuang.config.MyInterceptor"/>
        </mvc:interceptor>
    </mvc:interceptors>
```

5. 编写一个controller，接收请求

```java
/*测试拦截器的控制器*/
@Controller
@RequestMapping("/inter")
public class InterceptorController {
    /*@ResponseBody的作用其实是将java对象转为json格式的数据*/
    @RequestMapping("/interceptor")
    @ResponseBody

    public String testFunction(){
        System.out.println("控制器中方法执行了!");
        return "hello";
    }
}
```

6. 前端index.jsp 测试 一下

```
<p><a href="${pageContext.request.contextPath}/inter/interceptor"> 拦截器测试 </a></p>
```

7 启动tomcat,测试一下

![image-20201231150205834](img/image-20201231150205834.png)



知识点：

​	1、1个拦截器interceptors 可以配置多个 interceptor 

​	2、在 mapping path /**  这个表示包括这个请求下面的所有请求

​	 如果配置admin下面请求 可以配置   <mvc:mapping path="/admin/**" />

​	3、对应的拦截器实现类，我们放在Bean里面

### 9.2 例子 验证用户是否登录(认证用户)



实现思路： 

1、有一个登陆页面，需要写一个controller访问页面

2、登陆页面有一提交表单的动作。需要在controller中处理。判断用户名密码是否正确。如果正确，向session中写入用户信息。*返回登陆成功。*

3、拦截用户请求，判断用户是否登陆。如果用户已经登陆。放行， 如果用户未登陆，跳转到登陆页面

首先，我们设计Controller，这个里面，实现 tologin()  --进入登录页，  login()---实现登录后进入到首页，main() ---去首页  logout()----释放session后到main页面

然后，我们设计拦截器，对含有session信息、login、toLogin进行放行，其他的跳转到登录页面



Step1 . 编写登录页面 login.jsp  /WEB-INF/jsp/login.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Login</title>
</head>
<body>
    <%--在web-inf下所有的页面或者资源，只能通过controller，或者servlet进行访问--%>
    <h1>登录页面</h1>

    <form action="${pageContext.request.contextPath}/user/login">
        用户名:<input type="text" name="username">
        密码:<input type="text" name="pwd">
        <input type="submit" name="提交">
    </form>

</body>
</html>
```

step2  编写 UserController 处理请求

```java
package com.kuang.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

import javax.servlet.http.HttpSession;

@Controller
@RequestMapping("/user")
public class UserController {

   //跳转到登陆页面
   @RequestMapping("/jumplogin")
   public String jumpLogin() throws Exception {
       return "login";
  }

   //跳转到成功页面
   @RequestMapping("/jumpSuccess")
   public String jumpSuccess() throws Exception {
       return "success";
  }

   //登陆提交
   @RequestMapping("/login")
   public String login(HttpSession session, String username, String pwd) throws Exception {
       // 向session记录用户身份信息
       System.out.println("接收前端==="+username);
       session.setAttribute("user", username);
       return "success";
  }

   //退出登陆
   @RequestMapping("/logout")
   public String logout(HttpSession session) throws Exception {
       // session 过期
       session.invalidate();
       return "login";
  }
}
```

step3   编写一个登录页面 success.jsp

```java
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>success</title>
</head>
<body>
    <h1>登录成功页面</h1>
    <hr>
    <span>${user}</span>
    <p><a href="${pageContext.request.contextPath}/user2/logout">注销</a></p>
</body>
</html>
```

step 4. 编写我们的index.jsp页面，放入登录和成功页面的入口，启动tomcat测试下

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
 <head>
   <title>$Title$</title>
 </head>
 <body>
 <h1>首页</h1>
 <hr>
<%--登录--%>
 <a href="${pageContext.request.contextPath}/user/jumplogin">登录</a>
 <a href="${pageContext.request.contextPath}/user/jumpSuccess">成功页面</a>
 </body>
</html>
```



我们会发现，不管是登录页，还是成功页面，我们都可以进入，这是不符合正常业务逻辑，

按照业务逻辑，对于成功页面，需要用户登录才可访问，未登录用户，应该让用户去登录

step 5. 编写用户登录拦截器

```java
public class LoginInterceptor implements HandlerInterceptor {
    /*判断什么情况下没有登录，
    根据session判断
    登录就放行
    没有登录就不放行并跳转到指定页面
    */
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {

        HttpSession session = request.getSession();
        ///*在登录页面也要放行*/
        //if (request.getRequestURI().contains("login")){
        //    System.out.println("---------LoginInterceptor 处理前:login----------");
        //    return true;
        //}
        System.out.println("username is null?==>"+StringUtils.isEmpty(request.getParameter("username")));
        if (!StringUtils.isEmpty(request.getParameter("username"))){
            return true;
        }

        /*session有用户的登录信息也放行*/
        if (session.getAttribute("user")!=null){
            System.out.println("---------LoginInterceptor 处理前: 有userLoginInfo----------");
            return true;//放行，继续执行下面的
        }
        /*如果没有登录或者不在登录页就转发*/
        System.out.println("---------LoginInterceptor 处理前:被拦截----------");
        request.getRequestDispatcher("/WEB-INF/jsp/login.jsp").forward(request,response);
        return false;
    }
}
```





step 6. 在springmvc的配置文件中注册拦截器

```xml
<!--拦截器配置-->
<mvc:interceptors>
    <!--可以添加多个拦截器-->
    <mvc:interceptor>
        <!--"/**"/ 包括这个请求下面的所有请求 /admin/adsa/adsa-->
        <mvc:mapping path="/**"/>
        <bean class="com.kuang.config.MyInterceptor"/>
    </mvc:interceptor>
    <!--登录拦截器-->
    <mvc:interceptor>
        <!--可以只拦截user下面的请求-->
        <mvc:mapping path="/user/**"/>
        <bean class="com.kuang.config.LoginInterceptor"/>
    </mvc:interceptor>
</mvc:interceptors>
```

7、再次重启Tomcat测试！登录拦截功能无误，未登录用户，无法进入登录成功页

### 9.3 例子 文件上传和下载

准备工作： 文件上传是项目开发中最常见的功能之一，springmvc可以很好的支持文件上传，但是springmvc上下文默认没有装配MultipartResolver,因此默认情况下，其不能处理文件上传工作，如果想要使用spring的文件上传功能，则需要在上下文中配置MultipartResolever.

前端表单要求：为了能上传文件，必须将表单的method设置为post，并将enctype设置为 multipart/form-data. 只有在这样的情况下，浏览器CIA会把用户选择的文件以二进制数据发送给服务器。

**对表单中的 enctype 属性做个详细的说明：**

- application/x-www=form-urlencoded：默认方式，只处理表单域中的 value 属性值，采用这种编码方式的表单会将表单域中的值处理成 URL 编码方式。
- multipart/form-data：这种编码方式会以二进制流的方式来处理表单数据，这种编码方式会把文件域指定文件的内容也封装到请求参数中，不会对字符编码。
- text/plain：除了把空格转换为 "+" 号外，其他字符都不做编码处理，这种方式适用直接通过表单发送邮件。

```html
<form action="" enctype="multipart/form-data" method="post">
   <input type="file" name="file"/>
   <input type="submit">
</form>
```

一旦设置了enctype为multipart/form-data，浏览器即会采用二进制流的方式来处理表单数据，而对于文件上传的处理则涉及在服务器端解析原始的HTTP响应。在2003年，Apache Software Foundation发布了开源的Commons FileUpload组件，其很快成为Servlet/JSP程序员上传文件的最佳选择。

- Servlet3.0规范已经提供方法来处理文件上传，但这种上传需要在Servlet中完成。
- 而Spring MVC则提供了更简单的封装。
- Spring MVC为文件上传提供了直接的支持，这种支持是用即插即用的MultipartResolver实现的。
- Spring MVC使用Apache Commons FileUpload技术实现了一个MultipartResolver实现类：
- CommonsMultipartResolver。因此，SpringMVC的文件上传还需要依赖Apache Commons FileUpload的组件。

先来实现一个文件上传的功能

1、导入文件上传的jar包，commons-fileupload,maven会自动帮我们导入他的依赖包commons-io包

```xml
<!--文件上传-->
<dependency>
<groupId>commons-fileupload</groupId>
<artifactId>commons-fileupload</artifactId>
<version>1.3.3</version>
</dependency>
<!--servlet-api导入包-->
<dependency>
<groupId>javax.servlet</groupId>
<artifactId>javax.servlet-api</artifactId>
<version>4.0.1</version>
</dependency>
```

2、配置bean:  multipartResolver

[注意!!!这个bean的id必须为: multipartResolver,否则上传文件会报400的错误，在这里栽过坑，教训!]

```xml
<!--文件上传配置-->
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
    <!--请求的编码格式，必须和jsp的pageEncoding属性一致，以便正确读取表单的内容，默认是ISO-885901-->
    <property name="defaultEncoding" value="utf-8"/>
    <!--文件上传的大小上限，单位为字节(10485760=10M)-->
    <property name="maxUploadSize" value="10485760"/>
    <property name="maxInMemorySize" value="40960"/>
</bean>
```

CommonsMultipartFile的常用方法：

	- String getOriginalFilename()   获取上传文件的原名
	- inputStream getInputStream()  : 获取文件流
	- void transTo(File dest) : 将上传文件保存到一个目录文件中

我们去实际测试一下

3、编写前端页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>$Title$</title>
  </head>
  <body>
    <%--上传文件表单--%>
    <form action="${pageContext.request.contextPath}/upload" enctype="multipart/form-data" method="post">
      <input type="file" name="file"/>
      <input type="submit" value="upload" />
    </form>
  </body>
</html>
```

4、编写Controller

```java
@Controller
public class FileController {
    /*@RequestParam("file")  将前端<input name = file>控件得到的文件封装成CommonsMultipartFile对象  */
    /*如果是批量上传文件，CommonsMultipartFile 为数组即可*/
    @RequestMapping("/upload")
    public String upload(@RequestParam("file") CommonsMultipartFile file, HttpServletRequest request, Model model) throws IOException {
        /*1. 获取文件名 */
        String uploadFileName = file.getOriginalFilename();
        /*2. 如果文件名是空，直接回到首页*/
        if ("".equals(uploadFileName)) {
            model.addAttribute("msg", "文件名为空!");
            return "redirect:/index.jsp";
        }
        System.out.println("上传文件名为:" + uploadFileName);
        /*3. 上传路径保存设置*/
        String uploadPath = request.getServletContext().getRealPath("/upload");
        //如果路径不存在就创建一个
        File realPath = new File(uploadPath);
        if (!realPath.exists()){
            realPath.mkdir();
        }
        System.out.println("上传文件保存地址: "+realPath);
        /*获取输入流*/
        InputStream is = file.getInputStream();  //文件输入流 ，从网络读入内存
        OutputStream os = new FileOutputStream(new File(realPath, uploadFileName));  //文件输出流，从内存写入服务器文件

        /*从网络读取并写出到文件*/
        int len =0;
        byte[] buffer = new byte[1024];
        while ((len=is.read(buffer))!=-1){
            os.write(buffer,0,len);
            os.flush();
        }
        os.close();
        is.close();

        model.addAttribute("msg", "文件上传成功!");
        return "redirect:/index.jsp";
    }
}
```

测试上传文件，ok！

此处有个bug，文件名相同无法第二次上传

>在SpringMvc后台进行获取数据，一般有三种：
>1.request.getParameter(“参数名”)
>2.用@RequestParam注解获取
>3.Springmvc默认支持的数据类型接收参数，可直接通过controller方法参数对应jsp中请求参数name直接获取

**采用file.Transto 来保存上传的文件**

1、编写Controller

```java
    public String fileUpload2(@RequestParam("file") CommonsMultipartFile file, HttpServletRequest request, Model model) throws IOException {
        /*上传路径保存设置*/
        String path = request.getServletContext().getRealPath("/upload");
        File realPath = new File(path);
        if (!realPath.exists()) {
            realPath.mkdir();
        }
        System.out.println("上传文件保存地址" + realPath);
        
        /*通过CommonsMultipartFile的方法直接写文件(注意这个时候)*/
        file.transferTo(new File(realPath+"/"+file.getOriginalFilename()));
        return "redirect:/index.jsp";
    }
}
```

2.前团表单提交地址修改

3.访问提交测试  ok！

### 9.4 文件下载实现

解决思路：

- 设置respose响应头
- 读取文件-inputStream
- 写出文件 OutputStream
- 执行操作
- 关闭流(先开后关)

```java
@RequestMapping("/download")
public String downloads(HttpServletRequest request, HttpServletResponse response) throws IOException {
    /*准备要下载的图片地址*/
    String path = request.getServletContext().getRealPath("/upload");
    String fileName = "1.png";

    /*1. 设置response响应头*/
    response.reset(); //设置页面不缓存，清空buffer
    response.setCharacterEncoding("utf-8");//字符编码
    response.setContentType("multipart/form-data"); //设置二进制传输数据
    response.setHeader("Content-Disposition","attachment;fileName="+ URLEncoder.encode(fileName,"UTF-8"));

    /*2. 操作文件*/
    File file = new File(path, fileName);
    InputStream fin = new FileInputStream(file);    //读取文件输入流
    OutputStream out = response.getOutputStream();  //从内存写入到网络响应

    byte[] buff = new byte[1024];
    int len =0;
    while ((len=fin.read(buff))!=-1){
        out.write(buff,0,len);
        out.flush();
    }

    out.close();
    fin.close();
    return null;
}
```

前端添加入口

```html
<hr>
<h1>测试下载</h1>
<a href="${pageContext.request.contextPath}/download">点击下载</a>
```

测试，文件下载OK，大家可以和我们之前学习的JavaWeb原生的方式对比一下，就可以知道这个便捷多了!



## 10 spring mvc 参数绑定过程

### 10.1 springmvc参数绑定过程

从客户端(网页)请求key/value数据，经过参数绑定，将 key/value数据绑定到controller方法的形参上!

springmvc中，接收页面提交的数据是通过方法的形参来接收的，而不是在controller类定义成员变更接收!



客户端请求 key/value ----->处理器适配器HandlerAdapter调用spring提供的参数绑定组件将 key/value数据转成 controller方法的  形参---

参数绑定组件：

在springmvc早期版本使用PropertyEditor (只能将字符串传成java对象)

后来使用converter(进行任意类型的转换)

springmvc提供了很多converter(转换器)

在特殊情况下需要自定义converter，对日期数据绑定需要自定义converter

### 10.2 springmvc默认支持的类型

- `HttpServletRequest` 
  通过`request`t对象获取请求信息
- `HttpServletResponse` 
  通过`response`处理响应信息
- `HttpSession` 
  通过`session`对象得到`session`中存放的对象
- `Model/ModelMap` 
  `model`是一个接口，`modelMap`是一个接口实现 。 
  作用：将`model`数据填充到`request`域。



### 10.3 简单类型的参数绑定

1. 可以直接传入绑定，但 request传入的参数名称 和 controller方法的形参名称 必须一致，才可绑定成功
2. 通过@RequestParam对简单类型的参数进行绑定，此时 request传入的参数名称 只用和 @RequestParam("value") 的value相同即可，

```java
@RequestMapping(value="/editItems",method={RequestMethod.POST,RequestMethod.GET})
//@RequestParam中的value属性指定request传入的参数名称
//required属性 : 指定这个参数是否必须要传入
//defaultValue属性: 可以设置默认值，如果id参数没有传入，就会将默认值和形参绑定
public String editItems(Model model,@RequestParam(value="id",required=true,defaultValue="1") Integer items_id) throws Exception {
    //调用sercice查询商品信息
    ItemsCustom itemsCustom = itemsService.findItemsById(items_id);
    //通过参数中的model将数据传到页面
    model.addAttribute("itemsCustom",itemsCustom);
    return "items/editItems";
}
```

### 10.4 pojo类的参数绑定

页面中`input`的`name`属性和·controller·的`pojo`形参中的属性名称一致，将页面中数据绑定到`pojo`

step 1. 在前端的jsp页面， 我们的表单name属性必须和controller的pojo形参属性一直

```jsp
<tr>
    <td>商品名称</td>
    <td><input type="text" name="name" value="${itemsCustom.name}"></td>
</tr>
<tr>
    <td>商品名称</td>
    <td><input type="text" name="price" value="${itemsCustom.price}"></td>
</tr>
<tr>
    <td>商品名称</td>
    <td><input type="text" name="pic" value="${itemsCustom.pic}"></td>
</tr>
```

step 2. 我们的Controller

```java
@Controller
public class ItemController {

    //商品信息修改提交
    public String updateItems(Integer id, ItemsCustom itemsCustom){
        //itemsService.updateItems(id,itemsCustom);
        return "success";
    }
}
```

![image-20201231232221613](img/image-20201231232221613.png)



step3 .我们的pojo实体类

![image-20201231232246487](img/image-20201231232246487.png)



step4.我们的前端请求效果

![image-20201231232306742](img/image-20201231232306742.png)、、



### 10.5 自定义参数绑定实现日期类型绑定

对于`controller`形参中`pojo`对象，如果属性中有日期类型，需要自定义参数绑定。 
将请求日期数据串传成日期类型，要转换的日期类型和`pojo`中日期属性的类型保持一致。 
比如我的`Items`类中的`createtime`属性的类型为`java.util.Date`类型： 

![image-20201231232459340](img/image-20201231232459340.png)、、



需要向处理器适配器中注入自定义的参数绑定组件。 
**自定义日期类型绑件**

```java
package com.jiayifan.ssm.controller.converter;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

import org.springframework.core.convert.converter.Converter;

/**
 * 日期转换器
 * @author 贾一帆
 *
 */
public class CustomDateConverter implements Converter<String, Date> {

    @Override
    public Date convert(String source) {
        //实现将日期串转换为Date类型
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        try {
            //绑定成功，返回日期数据
            return simpleDateFormat.parse(source);
        } catch (ParseException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        //如果参数绑定失败，返回空
        return null;
    }

}
```

**配制方法，在`springmvc.xml`中配置**

```xml
<!-- 自定义参数绑定 -->
<bean id="conversionService"
      class="org.springframework.format.support.FormattingConversionServiceFactoryBean">
    <!-- 转换器 -->
    <property name="converters">
        <list>
            <!-- 日期类型的转换 -->
            <bean class="com.jiayifan.ssm.controller.converter.CustomDateConverter"/>
        </list>
    </property>
</bean>
```

## 11 springmvc工作中一些经验

对于`controller`形参中`pojo`对象，如果属性中有日期类型，需要自定义参数绑定。 
将请求日期数据串传成日期类型，要转换的日期类型和`pojo`中日期属性的类型保持一致。 
比如我的`Items`类中的`createtime`属性的类型为`java.util.Date`类型： 

### 1. 解决日期前后台问题的方法

> 方法1，直接在前台使用 <fmt: 格式化标签

[jstl中fmt标签详解](https://blog.csdn.net/lydong_/article/details/79812428)

这种方法直接在前台jsp页面，使用fmt标签即可

```jsp
<tbody>
    <c:forEach var="user" items="${userList}">
        <tr>
            <td>${user.id}</td>
            <td>${user.username}</td>
            <td><fmt:formatDate value="${user.birthday}" type="both" pattern="yyyy年MM月dd日" /> </td>
            <td>${user.sex}</td>
            <td>${user.address}</td>
        </tr>
    </c:forEach>
</tbody>
```

对应的pojo实体类

```java
public class Items {
    private int id;
    private String name;
    private float pice;
    private String pic;

    private Date createtime;

    private String detail;
}
```

结果页面：

![image-20210102124234070](img/image-20210102124234070.png)



> 方法2. 使用日期转换类解决

step 1. 编写MyDateConverter

```java
/*从字符串转日期*/
public class MyDateConverter implements Converter<String, Date> {
    public Date convert(String s) {
        /*1999年6月6日， 创建相对应的日期格式化对象*/
        SimpleDateFormat simpleDateFormat = null;
        if (s.contains("年")) {
            simpleDateFormat = new SimpleDateFormat("yyyy年mm月dd日");
        } else if (s.contains(".")) {
            simpleDateFormat = new SimpleDateFormat("yyyy.mm.dd");
        } else if (s.contains("-")) {
            simpleDateFormat = new SimpleDateFormat("yyyy-mm-dd");
        } else if (s.contains("/")) {
            simpleDateFormat = new SimpleDateFormat("yyyy/mm/dd");
        }

        /*解析*/
        try {
            /*把字符串解析成日期对象*/
            Date date = simpleDateFormat.parse(s);
            /*返回结果*/
            return date;
        }catch (ParseException e){
            e.printStackTrace();
        }
        return null;
    }
}
```

step 2. 进入到springmvc-controller.xml里面配置FormattingConversionServiceFactoryBean

```xml
配置点1.
<mvc:annotation-driven conversion-service="conversionService"/>

配置点2、<!--5.配置日期转换-->
<bean id="formattingConversion" class="org.springframework.format.support.FormattingConversionServiceFactoryBean">
    <property name="converters">
        <list>
            <!--配置自己的转换器-->
            <bean class="com.kuang.utils.MyDateConverter"/>
        </list>
    </property>
</bean>
```



Step 3. 使用@DatetimeFormat和@NumberFormat注解对象属性

```java
public class User {
    private int id;
    private String username;
    @DateTimeFormat(pattern = "yyyy-MM-dd")
    private Date birthday;
    private String sex;
    private String address;
}
```

![image-20210102175454847](img/image-20210102175454847.png)



![image-20210102175506611](img/image-20210102175506611.png)







# SSM

Mybatis：sqlsession

spring：Bean

springMVC：Controller

# 附录

## 常用注解

@Autowired



@Qualifier(value = "dog")



@Resource(name="cat")



@Component

把普通pojo实例化到spring容器中，相当于配置文件中的 `<bean id="" class=""/>`

@Scope("prototype")

@Scope("singleton")  //标记为单例模式

@Repository



@Service



@Controller



@Nullable：字段标记了这个注解，说明这个字段可以为null



@Resource：自动装配通过名字、类型



## 习惯包名

### 1、POJO：

POJO（Plain Ordinary Java Object）简单的Java对象，实际就是普通JavaBeans，是为了避免和EJB混淆所创造的简称。
使用POJO名称是为了避免和EJB混淆起来, 而且简称比较直接。其中有一些属性及其getter setter方法的类，没有业务逻辑，有时可以作为VO(value -object)或dto(Data Transform Object)来使用。当然，如果你有一个简单的运算属性也是可以的，但不允许有业务方法,也不能携带有connection之类的方法。

### 2、DAO：

DAO层叫数据访问层，全称为data access object，某个DAO一定是和数据库的某一张表一一对应的，其中封装了CRUD（增加Create、检索Retrieve、更新Update和删除Delete）基本操作，DAO只做原子操作。无论多么复杂的查询，dao只是封装增删改查。至于增删查改如何去实现一个功能，dao是不管的。
 

DAO(Data Access Object)是一个数据访问接口，数据访问：顾名思义就是与数据库打交道，夹在业务逻辑与数据库资源中间。
DAO模式是标准的J2EE设计模式之一，开发人员使用这个模式把底层的数据访问操作和上层的商务逻辑分开，一个典型的DAO实现有下列几个组件：

一个DAO工厂类；
一个DAO接口；
一个实现DAO接口的具体类；
数据传递对象（有些时候叫做值对象）
具体的DAO类包含了从特定的数据源访问数据的逻辑！



### 3、SERVICE：

Service层叫服务层，被称为服务，粗略的理解就是对一个或多个DAO进行的再次封装，封装成一个服务，所以这里也就不会是一个原子操作了，需要事物控制。**管理具体的功能的。**

一般情况下，Hibernate DAO只操作一个POJO对象，因此一个DAO对应一个POJO对象。 Service层是为了处理包含多个POJO对象（即对多个表的数据操作）时，进行事务管理（声明式事务管理），Service层（其接口的实现类）被注入多个DAO对象，以完成其数据操作。
SSM中Service存放业务逻辑处理，也是一些关于数据库处理的操作，但不是直接和数据库打交道，他有接口还有接口的实现方法，在接口的实现方法中需要导入mapper层，mapper层是直接跟数据库打交道的，它也是个接口，只有方法名字，具体实现在mapper.xml文件里，service是供我们使用的方法。
mapper层等于dao层，现在用mybatis逆向工程生成的mapper层，其实就是dao层。对数据库进行数据持久化操作，他的方法语句是直接针对数据库操作的，而service层是针对我们controller，也就是针对我们使用者。service的impl是把mapper和service进行整合的文件



Service层是为了处理包含多个POJO对象（即对多个表的数据操作）时，进行事务管理（声明式事务管理），Service层（其接口的实现类）被注入多个DAO对象，以完成其数据操作。
Service存放业务逻辑处理，也是一些关于数据库处理的操作，但不是直接和数据库打交道，他有接口还有接口的实现方法，在接口的实现方法中需要导入mapper层，mapper层是直接跟数据库打交道的，它也是个接口，只有方法名字，具体实现在mapper.xml文件里，service是供我们使用的方法。

### 4、Controller层：

Controler负责请求转发，接受页面过来的参数，传给Service处理，接到返回值，再传给页面。**管理业务（Service）调度和管理跳转的。**



### 5、Filter层

Filter对用户请求进行预处理，接着将请求交给Servlet进行处理并生成响应，最后Filter再对服务器响应进行后处理。



# ——底部——