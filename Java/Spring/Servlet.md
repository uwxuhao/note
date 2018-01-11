# Servlet #
**Servlet** is an interface.The **Servlet** interface defines a contract between a servlet and the servlet container.

A user request causes the servlet container to call a servlet’s service method, passing an instance of ServletRequest and an instance of ServletResponse.  

For each application the servlet container also creates an instance of ServletContext. This object encapsulates the environment details of the context (application). There is only one ServletContext for each context. For each servlet instance, there is also a ServletConfig that encapsulates the servlet configuration.

## API for **Servlet** interface ##
```java
void init(ServletConfig config) throws ServletException
void service(ServletRequest request, ServletResponse response) 
        throws ServletException, java.io.IOException
void destroy()
java.lang.String getServletInfo()
ServletConfig getServletConfig()
```

**init**. The servlet container invokes this method the first time the servlet is requested. This method is not called at subsequent requests. You use this method to write initialization code. When invoking this method, the servlet container passes a ServletConfig. 

**service**. The servlet container invokes this method each time the servlet is requested.

**destroy**. The servlet container invokes this method when the servlet is about to be destroyed.

Note: A servlet instance is shared by all users in an application.

### ServletConfig ###
The servlet container passes a ServletConfig to the servlet’s init method when the servlet container initializes the servlet. The ServletConfig encapsulates configuration information that you can pass to a servlet through @WebServlet or the deployment descriptor. The deployment descriptor is an XML file that contain configuration values. Every piece of information passed to the ServletConfig is called an initial parameter. An initial parameter has two components: key and value. To retrieve the value of an initial parameter from inside a servlet, call the **getInitParameter** method on the ServletConfig.

```java
java.lang.String getInitParameter(java.lang.String name)
```

InitParameter in ServletConfig using annotation

```java
@WebServlet(name = "ServletConfigDemoServlet", 
    urlPatterns = { "/servletConfigDemo" },
    initParams = {
        @WebInitParam(name="admin", value="Harry Taciak"),
        @WebInitParam(name="email", value="admin@example.com")
    }
)
```

## ServletContext ##
The ServletContext represents the servlet application. There is only one context per web application. You can obtain the ServletContext by calling the getServletContext method on the ServletConfig. In addition, there is also a getServletContext method in ServletRequest, that returns the same ServletContext.
The ServletContext is there so that you can share information that can be accessed from all resources in the application and to enable dynamic registration of web objects. The former is done by storing objects in an internal Map within the ServletContext. Objects stored in ServletContext are called attributes.

### Some API for ServletContext ###
```java
java.lang.Object getAttribute(java.lang.String name)
java.util.Enumeration<java.lang.String> getAttributeNames()
void setAttribute(java.lang.String name, java.lang.Object object)
void removeAttribute(java.lang.String name)
```

# GenericServlet #

```java
public abstract class GenericServlet implements Servlet, ServletConfig
```

Assign the ServletConfig in the init method to a class level variable **servletConfig** so that it can be retrieved by calling getServletConfig. Provide default implementations of all methods in the Servlet interface. Provide methods that wrap the methods in the ServletConfig.

# HTTP Servlet #

The HttpServlet class overrides the javax.servlet.GenericServlet class. When using HttpServlet, you will also work with the HttpServletRequest and HttpServletResponse objects that represent the servlet request and the servlet response, respectively. The HttpServletRequest interface extends javax.servlet.ServletRequest and HttpServletResponse extends javax.servlet.ServletResponse.


