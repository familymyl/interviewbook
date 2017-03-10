---
search:
    keywords: ['struts2']

---


# Struts2的应用，它有哪些功能？

# 参考解答：

Struts2 可以用来开发 web应用程序。 Struts2有如下的主要功能：

 1) 基于MVC(Model-View-Controller)设计模式，基于aop拦截器来处理用户请求，可以开发Action控制器来联系模型和视图的数据交互
  
 2) 提供了一套标签库，用来创建动态页面
 
 3) 简化了请求参数接收和类型转换、作用域变量传输、支持多种视图技术、解耦了servlet API，让开发和测试更为容易
 
 4) 提供web应用程序开发时所需要的通用功能，例如：表单重复提交、国际化支持等
 
 
 详细解释：
 
 1、struts.xml中的配置：

```xml
 <struts>
     <package name="test" namespace="/hello" extends="struts-default">
     <action name="helloworld"  class="com.xx.action.HelloAction" method="abc">
         <result name="success">/WEB-INF/list.jsp</result>
     </action>
     </package>
 </struts>
```
1、标签介绍：

package标签中的属性：

name：用来指定包名，必须是唯一的
namespace：用来定义包的命名空间，命名空间会作为访问该包下action路径的一部分
extends：用来定义该包的继承包，一般都继承struts-default包（该包定义了struts的核心功能，比如拦截器）

action标签中的属性：

name：用来指定action的名称，它与package的namespace共同组成访问某个action的路径。比如本例访问helloworld这个action的完整路径为：http://localhost:9090/helloworld/hello/helloworld.action
(其中.action可以省略)
class：用来指定action所对应的处理类，需要写类的全路径名
method：用来指定处理器类中的哪个方法执行该action操作。
 备注：action标签中的class属性和method属性可以缺省，缺省后默认状态下执行struts2中的ActionSupport类中的execute()方法。如果只缺省method就执行指定类的execute()方法。
 
result 标签用来指定action执行完需要跳转的视图。


struts 2 中的处理类可以是普通的java类和继承了ActionSupport的java类。范例：



```
// 例1
public class HelloAction{
	public String abc(){
		System.out.println("进入了HelloAction的abc()方法");
		return "success";
	}
}
```





```
// 例2
public class HelloAction extends ActionSupport{
	public String abc(){
		System.out.println("进入了HelloAction的abc()方法");
		return "success";
	}
}
```

2、struts标签库：
![](/assets/10.jpg)



3、

在struts.xml中配置国际化拦截器：i18n
```
<interceptor-ref name="i18n"/>
```
i18n拦截器在执行Action方法前，会自动查找请求中一个名为request_locale的参数，并转换成Locale对象，并将其设为用户默认的Locale（代表语言/国家环境）






 
 
 ---
 

