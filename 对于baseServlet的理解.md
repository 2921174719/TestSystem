baseServlet是一个类，继承了HttpServlet

原理：通过请求带参数“method”，然后通过反射，执行这个方法，将（requset,response）作为参数，baseServlet是重写一个选择器，然后继承它的类通过这个选择器反射执行其中的方法。

HttpServlet这个类里面有两个service()方法。首先要知道的是用户自定义的Servlet都是HttpServlet的子类，也就是要继承HttpServlet，而HttpServlet是从GenericServlet继承而来，GenericServlet类要实现javax.servlet.Servlet接口。而GenericServlet类提供的除service()方法以外所有接口方法都默认实现。所以service()是一个抽象方法，GenericServlet的派生类必须对该方法重置才能实现期望的业务逻辑。

Servlet生命周期分为三个阶段：

　　1，初始化阶段

　　2，响应客户请求阶段

　　3，终止阶段