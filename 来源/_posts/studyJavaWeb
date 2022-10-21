# JavaWeb学习
## 1.基本概念
* web,意为网页.如: **www.baidu.com**

* 静态web:
    - html,css
    - 提供给所有人看的数据始终不会发生变化
* 动态Web
    - 例如:淘宝,近乎所有的网站;
    - 提供给所有人的数据会发生变化,每个人在不同的时间不同的地点看到的信息各不相同!
    - 技术站: Servlet/JSP,ASP,PHP

    在java中,动态Web资源开发的技术统称为JavaWeb;

### 1.2Web应用程序

Web应用程序:可以提供浏览器访问的程序;

* a.html,b.html......多个Web资源可以被外界访问,对外界提供服务;

* 我们能访问到的任何一个页面或者资源,都存在于这个世界的某一个角落的计算机上.

* URL

* 这些统一的Web资源会被放在同一个文件夹下,Web应用程序->Tomcat:服务器

* 一个Web应用由多部份组成(静态Web)
    - html,css,js
    - jsp,servlet
    - java程序
    - jar包
    - 配置文件(properties)
Web应用程序编写完毕之后若想提供给外界访问,需要一个服务器来统一管理;

### 1.3静态Web

* *.htm,*.html.这些都是网页的后缀,如果服务器上一直存在这些东西,我们就可以直接进行读取
* 静态Web存在的缺点
    - Web页面无法动态更新,所有用户看到的都是一个页面
        - 轮播图,点击特效,伪动态
        - javascript[实际开发,它用的最多]
        - VBScript
    - 它无法和数据库交互(数据无法持久化,用户无法交互)

### 1.4动态Web
页面会动态展示:"Web的页面展示的效果因人而异";

缺点:
* 假如服务器的动态Web资源出现错误,我们需要重新编写我们的**后台程序**,重新发布;
    * 停机维护

优点:
* Web页面可以动态更新,所有用户看到的都不是一个页面
* 它可以和数据库交互(数据持久化:注册,商品信息,用户信息......)

*** 

## 2 Web服务器

### 2.1 技术讲解
ASP:
* 微软:国内最早流行的就是ASP;
* 在HTML中嵌入了VB的脚本,ASP+COM;
* 在ASP开发中,基本用一个页面都有几千行的业务代码,页面机器混乱
* 维护成本高!
* c#
* IIS

PHP:
* php开发速度很快,功能很强大,跨平台,代码很简单(70%,WP)
* 无法承载大访问量的情况(局限性)

JSP/Servlet:

B/S:浏览和服务器

C/S:客户端和服务器

* sun公司主推的B/S架构
* 基于java语言的(所有大公司,或者一些开源组件,都是用java写的)
* 可以承载**三高**(高性能,高可用,高并发)问题带来的影响
* 语法像ASP,ASP->JSP,加强市场强度;

### 2.2 web服务器

服务器是一种被动的操作,用来处理用户的一些请求和给用户一些响应信息;

IIS:

微软的:ASP.....Windows中自带的

Tomcat:

面向百度编程

Tomcat 是 Apache 软件基金会（Apache Software Foundation）的 Jakarta 项目中的一个核心项目，由Apache、Sun 和其他一些公司及个人共同开发制作。由于有 Sun 的参与和支持，最新的 Servlet 和 JSP Tomcat 5 支持的 2.0.0 技术先进性、性能稳定、免费获得了 Java 和 Tomcat 的广泛认可和支持。成为比较流行的Web应用服务器。

Tomcat代码服务器是很多免费的开放源代码的Web应用服务器，属于轻量级应用服务器，在中小型系统和初访问用户的开发场合下被广泛使用。对于java初学web来说,它是最佳的选择

Tomcat实际上陨星JSP页面和Servlet.Tomcat最新为10.0.14

工作3-5年后,可以尝试手写Tomcat服务器

***

## Tomcat

### 3.1 安装Tomcat    
Tomcat官网:https://tomcat.apache.org/
### 3.2 配置Tomcat文件
可以配置启动的端口号:

Tomcat的默认端口号为:8080   
mysql的默认端口号:3306  
http的默认端口:80   
https的默认端口:443 

```xml
<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```
可以配置的主机的名称:
* 默认的主机名为:localhost->127.0.0.0
* 默认网站应用的存放的位置:webapps
```xml
<Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
```
### 网站应该有的结构:
```java
--webapps: Tomcat服务器的web目录
    -ROOT: 网站的目录名
        -WEB-INf
            -classes: java程序
            -lib: web应用所依据的jar包
            -web.xml: 网站配置文件
        - index.html 默认的首页
        - static
            -css
                -style.css
            -js
            -img
```

***

## 4. HTTP
### 4.1 什么是Http
Http(超文本传输协议)是一个简单的请求-响应协议，它通常运行在TCP之上.
* 文本:html,字符串,-.....
* 超文本:图片,音乐,视频,定位,地图......
* 80    
HTTps : 安全的
* 443   
### 4.2 两个时代
* http1.0
    - http/1.0:客户端可以与web服务器连接,只能获得一个web资源,断开连接
* http2.0
    - http/1.1:客户端可以与web服务器连接,可以获得多个web资源
### 4.3 Http请求
* 客户端->发请求(Request)->服务器    
百度:   
```java
Request URL: https://www.baidu.com/     //请求地址
Request Method: GET                     get方法/post方法
Status Code: 200 OK                     状态码:200
Remote(远程) Address: 39.156.66.18:443        
```
```java
Accept: text/html`  
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9   语言
Connection: keep-alive
```
**1.请求行**    

* 请求行中的请求方式:GET    
* 请求方式:Get,Post,HEAD,DELETE......
    - get:请求能够携带的参数比较少,大小有限制,会在浏览器的URL地址栏显示数据内容,不安全,但高效
    - post:请求能够携带的参数没有限制,大小没有限制,不会在浏览器的URL地址栏显示数据内容,安全,但低效 

**2.消息头**    
```java
Accept 告诉浏览器,它所支持的数据类型
Accept-Encoding     支持那种数据类型 GBK UTF-8 GB2312
Accept-Language     告诉浏览器,它的语言环境
Connection          告诉浏览器,请求完成是断开还是保持连接
HOST:               主机......
```

### 4.4 Http相应
* 服务器->响应->客户端  
百度:
```java
Connection: keep-alive  连接
Content-Encoding: gzip  编码
Content-Type: text/html; charset=utf-8  类型
```
**1.响应体**
```java
Accept 告诉浏览器,它所支持的数据类型
Accept-Encoding     支持那种数据类型 GBK UTF-8 GB2312
Accept-Language     告诉浏览器,它的语言环境
Connection          告诉浏览器,请求完成是断开还是保持连接
HOST:               主机......
Refresh:            告诉客户端,多久刷新一次
Location:           让网页重新定位:
```
**2.响应状态码**

200: 请求相应成功

3xx: 请求重定向
* 重定向:你重新到我给你的新位置

4xx: 找不到资源

5xx: 服务器代码错误

***

## Maven

### 我为什么要学习这个技术?

1. 在javaweb开发中,需要使用大量的jar包,我们需要手动的导入
2. 如何能够让一个东西自动帮我导入和配置这个jar包

    由此,Maven诞生了!   

### 5.1 Maven
我们目前用它来就是方便导入jar包的!  
Maven的核心思想:**约定大于配置**
* 有约束,不要去违反

Maven会规定好你该如何去编写我们的java代码,必须要按照这个规范来

## 6. Servlet
### 6.1 什么是Servlet
* servlet就是sun公司开发动态web的一门技术
* sun在这些API中提供了一些接口叫做:Servlet,如果你想开发一个Servlet程序,只需要完成两个小步骤:
    - 编写一个类,需要Servlet接口
    - 把开发好的java类部署到web服务器中 

把实现了Servlet接口的java程序叫做,Servlet

### 6.2 HelloServlet

Servlet接口在sun公司有两个默认的实现类:HttpServlet,GenericServlet
1. 构建一个普通的maven项目,删掉里边的src目录,以后我们的学习就在这个项目了建立Moudel;这个空的工程就是maven的主工程
2. 关于maven父子工程的理解:         
父项目会有:
```xml
<modules>
        <module>javaweb-servlet</module>
    </modules>
```
子项目会有:
```xml
 <parent>
        <artifactId>javaweb02</artifactId>
        <groupId>org.example</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
```
父项目中的jar包子项目可以直接使用,子项目的父项目不能使用
```java
 son extends father
```

3. maven环境优化
    - 修改web.xml为最新的
    - 将maven的结构搭建完整
4. 编写一个Servlet程序
    1. 编写一个普通类
    2. 实现servlet接口,这里我们直接继承HttpServlet
```java
public class Hello extends HttpServlet {

    //由于Get或者post只是请求实现的不同的方式,可以相互调用,业务逻辑都一样
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //ServletInputStream inputStream = req.getInputStream();
        //ServletOutputStream outputStream = resp.getOutputStream();
        PrintWriter writer = resp.getWriter();//响应流
        writer.print("helloServlet");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}
```
5. 编写servlet的映射    
    为什么需要映射:我们写的是java程序,但是要通过浏览器访问,而浏览器需要连接web服务器,所以我们需要在web服务中注册我们写的servlet,还需要给他一个浏览器能够访问的路径;
```xml
    <!--    注册servlet-->
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>Hello</servlet-class>
    </servlet>
<!--    servlet的请求路径-->
    <servlet>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
```

## 6.3 Servlet原理
    Servlet是由Web服务器调用,Web服务器在收到服务器请求之后,会
    :

6. Mapping问题

    1. 一个Servlet可以指定一个映射路径

    ```xml
    <servlet-mapping>
            <servlet-name>hello</servlet-name>
            <url-pattern>/hello</url-pattern>
        </servlet-mapping>
    ```

    2. 一个Servlet可以指定多个映射路径

    ```xml
        <servlet-mapping>
            <servlet-name>hello</servlet-name>
            <url-pattern>/hello</url-pattern>
        </servlet-mapping>
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

    3. 一个Servlet可以指定通用映射路径
    ```xml
        <!--默认请求路径-->
    <servlet-mapping>
            <servlet-name>hello</servlet-name>
            <url-pattern>/hello/*</url-pattern>
        </servlet-mapping>
    ```
    4. 指定后缀或前缀等
    ```xml
        <!--可以自定义后缀实现请求映射
        注意点: *前面不能加项目映射路径
        hello/salwjqwio.hanhan
        -->
    <servlet-mapping>
            <servlet-name>hello</servlet-name>
            <url-pattern>*.hanhan</url-pattern>
        </servlet-mapping>
    ```

    5. 优先级问题   
    指定了固有的映射路径优先级最高,如果找不到就会找默认的处理请求
    ```xml
    <!--    404-->
        <servlet>
            <servlet-name>error</servlet-name>
            <servlet-class>ErrorServlet</servlet-class>
        </servlet>
        <servlet-mapping>
            <servlet-name>error</servlet-name>
            <url-pattern>/*</url-pattern>
        </servlet-mapping>
    ```

    ## 6.4 ServletContext
    web容器在启动的时候,它会为每个web程序都创建一个对应的ServletContext对象,它代表了当前的web应用
   1. 共享数据
        - 我在这个Servlet保存的数据,可以在另外一个Servlet中拿到
    ```java
    public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        
    //        this.getInitParameter(); 初始化参数
    //        this.getServletConfig(); Servlet配置
    //        this.getServletContext(); Servlet上下文
        
        ServletContext context = this.getServletContext();

        String username = "憨包";//数据=
        context.setAttribute("username",username);//将一个数据保存在了ServletContext中，名字为username,值username


        System.out.println("Hello Servlet!");
    }
    }
    ```
    ```xml
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.han.HelloServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>

    <servlet>
        <servlet-name>getc</servlet-name>
        <servlet-class>com.han.GetServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>getc</servlet-name>
        <url-pattern>/getc</url-pattern>
    </servlet-mapping>
    ```
    测试访问结果;

    2. 获取初始化参数
```xml
<!--配置一些web应用的初始化参数-->
    <context-param>
        <param-name>url</param-name>
        <param-value>jdbc:mysql://localhost:3306/mybatis</param-value>
    </context-param>
```
```java
public class ServletDemo03 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();

        String url = context.getInitParameter("url");
        resp.getWriter().print(url);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```
3. 请求转发
```java
 @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        System.out.println("进入了ServletDemo04");

//        RequestDispatcher requestDispatcher = context.getRequestDispatcher("/gp"); //转发的请求路径
//        requestDispatcher.forward(req,resp);  //调用forword实现请求转发
        context.getRequestDispatcher("/gp").forward(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
```
4. 读取资源文件
Piroperties
* 在java目录下新建properties
* 在resources目录下新建properties   

发现:都被打包在了同一个路径下:classes,我们俗称这个路径为类路径(classpath)

**此处额外添加** 

```xml
<!--在build中配置resources,来防止我们资源导出失败的问题-->

<build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
        </resources>
    </build>
```
思路:需要一个文件流;
```properties
username=root12122
password=acccaasb
```

```java
public class ServletDemo05 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        InputStream is = this.getServletContext().getResourceAsStream("/WEB-INF/classes/com/han/aa.properties");
        Properties prop = new Properties();
        prop.load(is);
        String user = prop.getProperty("username");
        String pwd = prop.getProperty("password");

        resp.getWriter().print(user+":"+pwd);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```
访问测试即可;

## 6.5 HttpServletResponse
web服务器接收到客户端的http请求,针对这个请求,分别创建一个代表请求的HttpServletRequest对象,代表响应一个HttpServletResponse;
* 如果要获取客户端请求过来的参数:找HttpServletRequest
* 如果要给客户端响应一些信息:找HttpServletResponse

### 1. 简单分类
**负责向浏览器发送数据的方法**
```java
    ServletOutputStream getOutputStream() throws IOException;
    PrintWriter getWriter() throws IOException;
```
**负责向浏览器发送一些响应流**
```java
    void setCharacterEncoding(String var1);

    void setContentLength(int var1);

    void setContentLengthLong(long var1);

    void setContentType(String var1);

    void setDateHeader(String var1, long var2);

    void addDateHeader(String var1, long var2);

    void setHeader(String var1, String var2);

    void addHeader(String var1, String var2);

    void setIntHeader(String var1, int var2);

    void addIntHeader(String var1, int var2);
```
**响应的状态码**
```java
    int SC_CONTINUE = 100;
    int SC_SWITCHING_PROTOCOLS = 101;
    int SC_OK = 200;
    int SC_CREATED = 201;
    int SC_ACCEPTED = 202;
    int SC_NON_AUTHORITATIVE_INFORMATION = 203;
    int SC_NO_CONTENT = 204;
    int SC_RESET_CONTENT = 205;
    int SC_PARTIAL_CONTENT = 206;
    int SC_MULTIPLE_CHOICES = 300;
    int SC_MOVED_PERMANENTLY = 301;
    int SC_MOVED_TEMPORARILY = 302;
    int SC_FOUND = 302;
    int SC_SEE_OTHER = 303;
    int SC_NOT_MODIFIED = 304;
    int SC_USE_PROXY = 305;
    int SC_TEMPORARY_REDIRECT = 307;
    int SC_BAD_REQUEST = 400;
    int SC_UNAUTHORIZED = 401;
    int SC_PAYMENT_REQUIRED = 402;
    int SC_FORBIDDEN = 403;
    int SC_NOT_FOUND = 404;
    int SC_METHOD_NOT_ALLOWED = 405;
    int SC_NOT_ACCEPTABLE = 406;
    int SC_PROXY_AUTHENTICATION_REQUIRED = 407;
    int SC_REQUEST_TIMEOUT = 408;
    int SC_CONFLICT = 409;
    int SC_GONE = 410;
    int SC_LENGTH_REQUIRED = 411;
    int SC_PRECONDITION_FAILED = 412;
    int SC_REQUEST_ENTITY_TOO_LARGE = 413;
    int SC_REQUEST_URI_TOO_LONG = 414;
    int SC_UNSUPPORTED_MEDIA_TYPE = 415;
    int SC_REQUESTED_RANGE_NOT_SATISFIABLE = 416;
    int SC_EXPECTATION_FAILED = 417;
    int SC_INTERNAL_SERVER_ERROR = 500;
    int SC_NOT_IMPLEMENTED = 501;
    int SC_BAD_GATEWAY = 502;
    int SC_SERVICE_UNAVAILABLE = 503;
    int SC_GATEWAY_TIMEOUT = 504;
    int SC_HTTP_VERSION_NOT_SUPPORTED = 505;
```
### 2. 下载文件
1. 向浏览器输出消息(一直在讲)
2. 下载文件
    1. 要获取下载文件的路径
    2. 下载的文件名是什么
    3. 设置想办法让浏览器支持下载我们需要的东西
    4. 获取下载文件的输入流
    5. 创建缓冲区
    6. 获取OutputStream对象
    7. 将FileOutputStream流 写入到buffer缓冲区
    8. 使用OutputStream将缓冲区中的数据输出到客户端
```java
public class FIleServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
//        1. 要获取下载文件的路径
        String realPath = "E:\\Study\\Idea\\JavawebServlet\\Response\\target\\classes\\1.jpg";
        System.out.println("下载文件的路径"+realPath);
//        2. 下载的文件名是什么
        String filename = realPath.substring(realPath.lastIndexOf("\\" + 1));
//        3. 设置想办法让浏览器支持下载我们需要的东西,中文文件名URLEncoder.encode编码,否则可能乱码
        resp.setHeader("Content-disposition","attachment;filename="+ URLEncoder.encode(filename,"UTF-8"));
//        4. 获取下载文件的输入流
        FileInputStream in = new FileInputStream(realPath);
//        5. 创建缓冲区
        int len = 0;
        byte[] buffer = new byte[1024];
//        6. 获取OutputStream对象
        ServletOutputStream out = resp.getOutputStream();
//        7. 将FileOutputStream流 写入到buffer缓冲区
//        8. 使用OutputStream将缓冲区中的数据输出到客户端
        while ((in.read(buffer)) > 0){
            out.write(buffer,0,len);
        }
        in.close();
        out.close();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```
### 3.验证码功能
* 前端实现
* 后端实现,需要用到java的图片类,生成一个图片
```java
public class ImageServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //如何让浏览器五秒钟自动刷新一次;
        resp.setHeader("refresh","3");

        //在内存中创建一个图片
        BufferedImage image = new BufferedImage(80,20,BufferedImage.TYPE_INT_RGB);
        //得到图片
        Graphics2D g = (Graphics2D) image.getGraphics();//笔
        //设置图片的背景颜色
        g.setColor(Color.white);
        g.fillRect(0,0,80,20);
        //给图片写数据
        g.setColor(Color.blue);
        g.setFont(new Font(null,Font.BOLD,20));
        g.drawString(makeNumber(),0,20);

        //告诉浏览器,这个请求用图片的方式打开
        resp.setContentType("image/jpeg");
        //网站存在缓存,不让浏览器缓存
        resp.setDateHeader("expires",-1);
        resp.setHeader("Cache-Control","no-cache");
        resp.setHeader("pragma","no-cache");

        //把图片写给浏览器
        ImageIO.write(image,"jpg",resp.getOutputStream());
    }

    //生成随机数
    private String makeNumber(){
        Random random = new Random();
        String num = random.nextInt(9999999)+"";
        StringBuffer sb = new StringBuffer();
        for (int i = 0; i < 7 - num.length(); i++) {
            sb.append("0");
        }
        String s = sb.toString() + num;
        return num;
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```
## 6.6 HttpServletRequest
