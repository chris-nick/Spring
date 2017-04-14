### Spring框架学习（一）
 - 1.what Spring framework?
  ~~ Spring是J2EE应用框架，轻量级AOP和IOC容器框架，主要针对JavaBean的生命周期进行管理，可单独使用，也可和Struts，ibatis等组合使用。 ~~
 - 2.概述
  1).IOC控制反转
    BeanFactory是Ioc的核心接口，负责实例化，定位，配置应用程序中的对象及建立这些对象间的依赖。XmlBeanFactory实现BeanFactory接口，通过获取xml数据，组合对象和对象间的依赖。
    BeanFactory factory = new XMLBeanFactory(new FileInputSteam("mybean.xml"));
    MyBean myBean = (MyBean)factory.getBean("mybean");
    Spring三种注入方式：setter方法,构造函数,接口注入。
  2).AOP面向切面编程
    两只实现：动态代理和CGLIB。动态代理必须提供接口，而CGLIB要有继承。
  3).7个模块:AOP,DAO,ORM,Context,Web，MVC,Core。Spring Core主要组件BeanFactory。
  - 核心容器：核心容器提供 Spring 框架的基本功能。核心容器的主要组件是 BeanFactory，它是工厂模式的实现。BeanFactory 使用控制反转 （IOC） 模式将应用程序的配置和依赖性规范与实际的应用程序代码分开。
  - Spring 上下文：Spring 上下文是一个配置文件，向 Spring 框架提供上下文信息。Spring 上下文包括企业服务，例如 JNDI、EJB、电子邮件、国际化、校验和调度功能。
  - Spring AOP：通过配置管理特性，Spring AOP 模块直接将面向方面的编程功能集成到了 Spring 框架中。所以，可以很容易地使 Spring 框架管理的任何对象支持 AOP。Spring AOP 模块为基于 Spring 的应用程序中的对象提供了事务管理服务。通过使用 Spring AOP，不用依赖 EJB 组件，就可以将声明性事务管理集成到应用程序中。
  - Spring DAO：JDBC DAO 抽象层提供了有意义的异常层次结构，可用该结构来管理异常处理和不同数据库供应商抛出的错误消息。异常层次结构简化了错误处理，并且极大地降低了需要编写的异常代码数量（例如打开和关闭连接）。Spring DAO 的面向 JDBC 的异常遵从通用的 DAO 异常层次结构。
  - Spring ORM：Spring 框架插入了若干个 ORM 框架，从而提供了 ORM 的对象关系工具，其中包括 JDO、Hibernate 和 iBatis SQL Map。所有这些都遵从 Spring 的通用事务和 DAO 异常层次结构。
  - Spring Web 模块：Web 上下文模块建立在应用程序上下文模块之上，为基于 Web 的应用程序提供了上下文。所以，Spring 框架支持与 Jakarta Struts 的集成。Web 模块还简化了处理多部分请求以及将请求参数绑定到域对象的工作。
  - Spring MVC 框架：MVC 框架是一个全功能的构建 Web 应用程序的 MVC 实现。通过策略接口，MVC 框架变成为高度可配置的，MVC 容纳了大量视图技术，其中包括 JSP、Velocity、Tiles、iText 和 POI。
 - 3.why use spring?
  在不使用spring框架之前，Service层调dao，必须要new 一个dao对象，如下：
      //dao层对象  
    public class UserDao{  
       publicvoid insert(User user){}  
    }  
       
    //service层对象  
    public classUserService{  
       publicvoid insert(User user){  
           UserDaouserdao = new UserDao();  
           userdao.insert(user);  
       }  
    }  
   使用Spring之后：
    //dao层对象  
    public class UserDao{  
        publicvoid insert(User user){}  
    }  
       
    //service层对象  
    public classUserService{  
       privateUserDao userdao;  
       
       publicUserDao getUserdao() {  
          returnuserdao;  
       }  
       publicvoid setUserdao(UserDao userdao) {  
          this.userdao= userdao;  
       }  
       
       publicvoid insert(User user){  
          userdao.insert(user);  
       }  
       
    }  
    service层要用dao层对象需要配置到xml配置文件中，至于对象是怎么创建的，关系是怎么组合的都交给了spring框架去实现。
 - 4.框架优点
   - 轻量级的容器框架没有侵入性
   - 使用IoC容器更加容易组合对象直接间关系，面向接口编程，降低耦合
   - Aop可以更加容易的进行功能扩展，遵循ocp开发原则
   - 创建对象默认是单例的，不需要再使用单例模式进行处理

 - 5.缺点：业务功能依赖spring特有的功能，依赖与spring环境。
