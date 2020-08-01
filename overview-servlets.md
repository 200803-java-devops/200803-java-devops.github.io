# Client-Server communication
## HTTP
Hypertext Transport Protocol, or HTTP, is a common standard for delivering content across the internet, especially between users and servers. An HTTP request should include a url destination, an HTTP method, and content such as metadata and a payload carried by its headers and body. A response will then be sent back with a status code and its own headers and body.

## HTTP Status Codes
- 100-199: INFO
- 200-299: OK/Success
- 300-399: Redirect
- 400-499: Error/Request Incomplete
- 500-599: Server Error

## HTTP Methods (Verbs)
 - GET: retrieves information, sends info in the URL itself, empty body
 - POST: delivers content in body, usually for creating new resources
 - PUT: update content
 - DELETE: delete content
 - PATCH
 - UPDATE
 - TRACE
 - HEAD
 - OPTIONS

# JavaEE
Java Enterprise Edition, this is a community driven collection of Specifications, APIs and Frameworks which provide enterprise functionality. We will start with Java Servlets, a JavaEE API for communicating between a Java code base and HTTP.

Found in `javax.servlet` and `javax.http` the Servlet API provides a Servlet Interface which is implemented by the GenericServlet Abstract Class, then the HTTPServlet Abstract Class, and then finally allows you to extend the HTTPServlet.

In a normal servlet process:
- The client sends an HTTP Request to a (Servlet) Web Container, which is a Java Server that is running your application. We will be using Apache Tomcat, which is Apache's lightweight implementation of the JavaEE Server and Servlet Container spec.
- Your Tomcat server will have your application in its webapps folder (as a war, usually), and this application will have the following:
    - *src/*: for the servlet and other business logic code
    - *webapp/*: for any hosted HTML-related files, as well as:
    - **Deployment Descriptor**: commonly a *web.xml* file that maps incoming requests to your Servlets.
- Java application on Tomcat will handle Request as well as the Response by creating Java objects to model the Request/Response.

## Servlet - Lifecycle
The Tomcat server will handle the control flow of your application through a servlet lifecycle process.
1. When a request comes in, the container instantiates any appropriate servlets
1. Once instantiated the container initializes the servlet by invoking its `init()` method
1. After initialization (or existing servlet is found), the container invokes `service()` to process the request.
    1. public void service (ServletRequest req, ServletResponse resp) {...} ->
    1. protected void service (HttpServletRequest req, HttpServletResponse resp) {...} ->
    1. protected void doGet (HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {...} //You write this
1. Response object is returned to client
1. When the container shuts down or needs to conserve memory or just because a servlet's stated lifespan is reached, the container will call the `destroy()` method of your servlet.

tl;dr Container calls init() once, service() many times, and eventually destroy() once.

## WAR
JEE web applications are usually packaged as `.war` files, a web archive similar to a `.jar` but with some minor changes to folder heirarchy. A `src/main/webapp` folder becomes the root directory, and the archive is usually hosted on a Java web server such as **Apache Tomcat**. Be sure to set the `packaging` property in your `pom.xml` to `war`:
#### pom.xml
```xml
...
<packaging>war</packaging>
...
```

## Dependencies
To begin using Java Servlets, include the following dependency to your Maven `pom.xml`:
#### pom.xml
```xml
...
<groupId>javax.servlet</groupId>
<artifactId>servlet-api</artifactId>
<version>2.5</version>
...
```
`Servlet` is a JEE specification which is not included in Java's standard library, so it must be imported or the project must use a JDK with JEE libraries included already.

## Deployment Descriptor
A Java server like Tomcat will deploy a web archive and register all servlets according to the *deployment descriptor* found in `src/main/webapp/WEB-INF/web.xml`:
#### web.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" version="2.5">

...

</web-app>
```
Servlets, Filters, Context parameters, and other configurations are declared and defined in the `web.xml` 

## Servlet Mapping
Servlet classes are registered in the `web.xml` by assigning a name to both a url mapping and the fully qualified class name of the Servlet:
#### web.xml
```xml
...
<servlet>
    <servlet-name>myServlet</servlet-name>
    <servlet-class>servlets.MyServlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>myServlet</servlet-name>
    <url-pattern>/myServlet</url-pattern>
</servlet-mapping>
...
```
This will provide access to the servlet through its url mapping, in the above case at `http:[hostname]:[port]/[app-context]/myServlet`

## Servlet
The Servlet API provides the `HttpServlet` abstract class which can be extended to define your own custom behavior:
#### MyServlet.java
```java
package servlets;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class MyServlet extends HttpServlet {
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp)
		throws ServletException, IOException {
            // Implements GET behavior
	}
	
	@Override
	protected void doPost(HttpServletRequest req, HttpServletResponse resp)
		throws ServletException, IOException {
            // Implements POST behavior
	}
}
```
The `HttpServletRequest` object provides useful methods such as `getParameter(String name)` which returns the value of a Query or post body parameter. `HttpServletResponse` provides a `getWriter()` method which returns a `PrintWriter` object to append data to the response body.

## Servlet 3+
More recent versions of the Servlet API offer convenience annotations that allows configuration in a decorator over the Servlet class itself, leaving the `web.xml` blank for the most part:

#### pom.xml
```xml
...
<groupId>javax.servlet</groupId>
<artifactId>javax.servlet-api</artifactId>
<version>3.0.1</version>
<scope>provided</scope>
...
```

#### MyServlet.java
```java
package servlets;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/myServlet")
public class MyServlet extends HttpServlet {
	protected void doGet(HttpServletRequest req, HttpServletResponse resp)
		throws ServletException, IOException {
            // Implements GET behavior
	}
}
```

## ServletContext vs ServletConfig
A servlet container like Tomcat creates a singleton instance for each servlet, each sharing a ServletContext where certain initialization parameters are shared. These can be set in the Deployment Descriptor with the `context-param` tag:
```xml
...
<welcome-file-list>
    <welcome-file>index.html</welcome-file>
</welcome-file-list>
<context-param>
    <param-name>key</param-name>
    <param-value>value</param-value>
</context-param>
<servlet>
    <servlet-name>myServlet</servlet-name>
    <servlet-class>servlets.MyServlet</servlet-class>
</servlet>
...
```
The parameter can be accessed through a servlet's ServletContext delegate method:
>getServletContext().getInitParameter("key");

Each servlet meanwhile has its own local instance for its own configuration, its ServletConfig, which can be given initialization parameters with the `init-param` tag:
```xml
...
<servlet>
    <servlet-name>myServlet</servlet-name>
    <servlet-class>servlets.MyServlet</servlet-class>
    <context-param>
        <param-name>key</param-name>
        <param-value>value</param-value>
    </context-param>
</servlet>
...
```
This parameter can be accessed directly from the servlet:
>getInitParameter("key");

# Tomcat Web Server
Download [Tomcat](http://tomcat.apache.org/) and extract the archive somewhere.

## Deploying a Java web app to Tomcat
### Manual deployment
Package the project into a `war` file, then move the file into your Tomcat server's webapp folder. Tomcat should unpack and deploy the application automatically.

### IDE debug server
Eclipse and other IDEs can deploy an application onto a debug server for testing. Use the Eclipse server view to install Tomcat then add the project to the workspace.

## Embedded Tomcat
### Tomcat Maven Plugin
Add the `tomcat7-maven-plugin` to the `pom.xml`:
```xml
<build>
    <pluginManagement>
        <plugins>
            <plugin>
                <groupId>org.apache.tomcat.maven</groupId>
                <artifactId>tomcat7-maven-plugin</artifactId>
                <version>2.2</version>
                <configuration>
                    <path>/${project.build.finalName}</path>
                    <finalName>executable.jar</finalName>
                </configuration>
            </plugin>
        </plugins>
    </pluginManagement>
</build>
```
Then run the project with Maven:
>mvn tomcat7:run

If Tomcat is installed, with the CATALINA_HOME environment variable set, the same plugin can be used to deploy the application to the server with:
>mvn tomcat7:deploy

### Tomcat Embedded API
Tomcat embed is a library that allows for programmatic configuration and deployment of an embedded server within a Java application. In the `pom.xml`:
```xml
<dependency>
    <groupId>org.apache.tomcat.embed</groupId>
    <artifactId>tomcat-embed-core</artifactId>
    <version>8.5.23</version>
</dependency>
```

Then in a main method:
```java
import org.apache.catalina.Context;
import org.apache.catalina.startup.Tomcat;

import javax.servlet.http.HttpServlet;
import java.io.File;

public class App {
    public static void main(String[] args) throws Exception {
        Tomcat tomcat = new Tomcat();
        tomcat.setPort(8080);

        // Set context path and root folder
        String contextPath = "/";
        String docBase = new File(".").getAbsolutePath();

        Context context = tomcat.addContext(contextPath, docBase);

        // Declare, define, and map servlets
        HttpServlet helloServlet = new HttpServlet(){
            @Override
            protected void doGet(HttpServletRequest req, HttpServletResponse resp)
                    throws ServletException, IOException {
                PrintWriter out = resp.getWriter();
                out.write("<html><title>Example</title><body><h1>Hello, World!</h1></body></html>");
                out.close();
            }
        };

        String servletName = "HelloServlet";
        String urlPattern = "/hello";

        // Register servlets with Tomcat
        Tomcat.addServlet(context, servletName, helloServlet);
        context.addServletMappingDecoded(urlPattern, servletName);

        // Start the server
        tomcat.start();
        tomcat.getServer().await();
    }
}
```

## Resources
#### Documentation
- [RFC 2616 - Hypertext Transfer Protocol](https://tools.ietf.org/html/rfc2616)
- [MDN - HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)
- [Java EE 7](https://docs.oracle.com/javaee/7/JEETT.pdf)
- [JSR 369: JavaTM Servlet 4.0 Specification](https://jcp.org/en/jsr/detail?id=369)
- [Apache Tomcat 9.0](https://tomcat.apache.org/tomcat-9.0-doc/index.html)
- [Java Servlet API](https://github.com/javaee/servlet-spec)

### Tutorials
- [Java Servlet Technology - JavaEE 7 Tutorials](https://docs.oracle.com/javaee/7/tutorial/servlets.htm)
- [How To Install Apache Tomcat 8 on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-install-apache-tomcat-8-on-centos-7)
- [Understanding Web Applications, Servlets, and JSPs](https://docs.oracle.com/cd/E13222_01/wls/docs92/webapp/basics.html)
- [Servlet Programming Tasks](https://docs.oracle.com/cd/E13222_01/wls/docs92/webapp/progservlet.html#wp159442)
- [Servlet Connection Strategies](https://www.oreilly.com/library/view/java-programming-with/059600088X/ch04s02.html)
- [Java SE 8: Creating a Web App with Bootstrap and Tomcat Embedded](https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/basic_app_embedded_tomcat/basic_app-tomcat-embedded.html)
- [Create a Java Web Application Using Embedded Tomcat](https://devcenter.heroku.com/articles/create-a-java-web-application-using-embedded-tomcat)