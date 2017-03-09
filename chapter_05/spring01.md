---
search:
    keywords: ['spring','核心','ioc','aop','di','控制反转','依赖注入','面向切面编程', 'beanfactory', 'applicationcontext', '依赖注入方式']

---


# spring核心思想

# 题目问法

1. 你知道IOC(Inversion of Control)吗? IOC有哪几种类型? 使用IOC有哪些好处? 现在有哪些比较流行的IoC容器?

2. 简述面向切面编程AOP的好处？spring中常见的基础切面有哪些？切面的实现原理是什么？

3. spring中BeanFactory和ApplicationContext的联系和区别

4. spring中循环注入

5. spring中依赖注入的方式

6. spring 的scope


# 参考解答
spring 有两大核心思想：控制反转（IOC）和面向切面编程（AOP）

## IOC
IOC即控制反转，是指将java bean的创建、生命周期、依赖关系管理交给**容器**来控制。

在没有使用IOC思想之前，需要程序员主动去创建bean，维护其是否单例，生命周期等等，这样做的缺点是，对象的创建与对象的使用相耦合，对象与对象之间的关系紧耦合，不利于程序的扩展，经常会牵一发而动全身：某个对象发生了修改，使用这个对象的所有代码都需要跟着修改。

IOC的思想是将刚才提到的创建bean，bean实例个数和声明周期的控制，都交给容器来管理。相当于将bean的控制权移交给了容器，因此被称为控制反转。控制反转的好处是，bean的创建和声明周期均可通过容器配合配置文件的方式来管理，降低了耦合。

## DI
DI即Dependency Injection，是对IOC概念的一个补充。

传统的web开发中也存在容器的概念，例如tomcat 容器控制servlet和jsp的创建以及生命周期。虽然web容器也存在控制反转的思想，但与之前提到的IOC容器不同的是，web容器没有管理对象之间的依赖关系。

为了强调IOC容器的特点，又提出了依赖注入的概念。IOC容器不仅管理bean，还管理bean与bean之间的依赖关系。例如 service使用了 dao，那么称service依赖于 dao，它们之间的依赖关系并不是由代码来建立，而是IOC容器通过配置文件或注解的方式，在程序运行期间关联起来，进一步降低了耦合。

## 小结
正是因为控制反转和依赖注入的存在，使得spring可以和绝大多数开源框架整合。

## Spring IOC 容器的类型
spring中的容器类型有两种：BeanFactory和ApplicationContext

* BeanFactory接口定义了Spring最基本的bean实例化和依赖注入功能，它根据bean定义(bean definition)来创建bean实例。

* ApplicationContext对BeanFactory的功能做了扩展：
 * ApplicationContext继承了MessageSource来承诺实现资源文件管理和国际化
 * ApplicationContext继承了ApplicationEventPublisher来承诺实现事件推送编程
 * ApplicatonContext继承了ResourcePatternResolver来处理Spring中的Resource资源
 
* ApplicationContext和BeanFactory的关系是组合而非继承。

# Spring 依赖注入的方式
* spring中依赖注入主要方式有set注入和构造注入。
* 另外还可以通过@Autowired @Resource @Value 进行注入，它们可以分别用于set方法注入、构造方法注入和field属性注入。
* 最后，spring中的DefaultListableBeanFactory提供了容器外的bean属性的织入

# Spring 循环注入
如果出现如下情况:
类A的构造中引用了类B，而类B的构造中引用了类A，这时候是会出现无限循环的情况，Spring初始化容器会抛异常。

解决方法是将构造注入改造为set方法注入，spring会尽可能晚地处理set依赖关系，换句话说，spring会先构造bean的实例，再进行依赖注入，最后调用生命周期相关方法。

# Sprint 的scope
通过`<bean scope="singleton|prototype">`
来控制bean的单例还是多例，singleton表示bean是单例的，prototype表示bean是多例的

# AOP
aop即面向切面编程，将事务、权限检查、日志等关注点（通知）提取出来，与正常的业务逻辑分离开，这样利于代码的重用和解耦。在运行时，通过代理模式再将这些关注点与正常业务结合在一起，仍然达到分离前相同的功能。


---








