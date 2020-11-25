baseServlet是一个类，继承了HttpServlet

原理：通过请求带参数“method”，然后通过反射，执行这个方法，将（requset,response）作为参数，baseServlet是重写一个选择器，然后继承它的类通过这个选择器反射执行其中的方法。

HttpServlet这个类里面有两个service()方法。首先要知道的是用户自定义的Servlet都是HttpServlet的子类，也就是要继承HttpServlet，而HttpServlet是从GenericServlet继承而来，GenericServlet类要实现javax.servlet.Servlet接口。而GenericServlet类提供的除service()方法以外所有接口方法都默认实现。所以service()是一个抽象方法，GenericServlet的派生类必须对该方法重置才能实现期望的业务逻辑。

BaseServlet继承于HttpServlet，主要使用反射完成servlet后端方法的分发。具体步骤如下：

1.获取请求路径；

2.获取方法名称；

3.获取方法对象（哪个子类继承BaseServlet，那么代码中的this就代表该子类）

4.获取方法，执行方法。

与传统重写service方法相比的不同：

原来是一个功能一个Servlet，现在优化为一个模块一个Servlet，由BaseServlet进行方法的转发，并承担一些公共方法的抽取；

BaseServlet 相当于是项目中所有servlet的父类，让每个模块继承BaseServlet即可；

BaseServlet让一个servlet可以同时处理多个请求，相当于在数据库中一张表对应一个Servlet，在Servlet中提供不同的方法，完成用户的请求。