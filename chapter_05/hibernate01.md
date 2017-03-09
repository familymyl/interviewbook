---
search:
    keywords: ['hibernate','关联关系','@manytoone']

---


# hibernate中怎样实现类之间的关系


# 参考解答

java中类与类之间的关系可以对应数据库中表与表之间的关系。hibernate中通过注解@ManyToOne、@OneToMany、@ManyToMany分别表示数据库中的多对一、一对多、多对多关系。

举例：
商品和类别的关系是多对一

那么实体类可以设计为：


```java
// 类别实体类
@Entity
public class Category {
  
   @Id
   private int id;
   private String name;
   ...
}

```
	

```java
// 商品实体类
@Entity
public class Product {

   @Id
   private int id;
   private String name;
   private Double price;
   // 关系属性
   @ManyToOne  // category_id
   private Category category; // 关系属性 : 多对一	
   ...
}

```
---

