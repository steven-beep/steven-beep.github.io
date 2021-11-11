# 																Spring Framework 

​                                                                                                                                                   --- Al_tair

----

## 一. 初识Spring  Framework 

​	Spring 春天 迎来了程序员的春天！

- 历史由来：Spring框架即以interface21框架为基础，经过重新设计，并不断丰富其内涵，于2004年3月24日，发布了1.0正式版。
-  开发者：该框架最初由 Rod Johnson 以及 Juergen Hoeller 等人开发

+ 概念：Spring 又称 Spring Framework 是java平台上免费开源的全栈应用程序框架和控制反转的容器实现，换句话来说就是Spring Framework 建立在java平台上，并为其使用者提供了应用程序框架（类似于房屋的整体架构）以及一系列底层容器。

-  目的：解决企业应用开发的复杂性

-  官网：[Spring Framework](https://spring.io/projects/spring-framework)     Github:[网址](https://github.com/spring-projects/spring-framework)

- maven>>[Spring Core](https://mvnrepository.com/artifact/org.springframework/spring-core) » [5.3.10](https://mvnrepository.com/artifact/org.springframework/spring-core/5.3.10): 

    ```xml
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-core -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>5.3.10</version>
    </dependency>
    ```

- 特征： 轻量    面向切面（AOP）  控制反转（IOC）   容器     框架      MVC

- 组成：Spring  Framework  Runtime		                            

    ![SpringFrameworkRuntime](https://use-typora.oss-cn-hangzhou.aliyuncs.com/SpringFrameworkRuntime.png)

     Spring七大模块

    ![image-20211013171033189](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20211013171033189.png)

- 优点： 

    1. 低侵入式设计，代码污染极低

    2. 独立于各种应用服务器，基于Spring框架的应用，可以真正实现Write Once ,Run Auywhere的承诺

    3. Spring的DI机制降低了[业务对象](https://baike.baidu.com/item/业务对象)替换的复杂性，提高了组件之间的解耦

    4. Spring的AOP支持允许将一些通用任务如安全、事务、日志等进行[集中式管理](https://baike.baidu.com/item/集中式管理/4690090)，从而提供了更好的复用

    5. Spring的ORM和DAO提供了与第三方持久层框架的良好整合，并简化了底层的数据库访问

    6. Spring并不强制应用完全依赖于Spring，开发者可自由选用Spring框架的部分或全部

        

## 二. Spring IoC Container 和 Bean 简单介绍

### 2.1	IoC是什么

​	Inversion of Control 即 “ 控制反转 ”  is also known as dependency injection 即 " 依赖注入" ，是一种设计思想，它能够将你设计好的对象交给容器控制，而不是传统的在你的对象内部直接控制

1. **控制反转,控制？反转？**

    获得依赖对象的过程反转了

    -  软件系统在没有引入IOC容器之前，如图1所示，对象A依赖于对象B，那么对象A在初始化或者运行到某一点的时候，自己必须主动去创建对象B或者使用已经创建的对象B。无论是创建还是使用对象B，控制权都在自己手上。

        ![耦合](https://use-typora.oss-cn-hangzhou.aliyuncs.com/%E8%80%A6%E5%90%88.png)

    - 软件系统在引入IOC容器之后，这种情形就完全改变了，如图3所示，由于IOC容器的加入，对象A与对象B之间失去了直接联系，所以，当对象A运行到需要对象B的时候，IOC容器会主动创建一个对象B注入到对象A需要的地方。

        ![解耦](https://use-typora.oss-cn-hangzhou.aliyuncs.com/%E8%A7%A3%E8%80%A6.png)

    - 通过前后的对比，我们不难看出来：对象A获得依赖对象B的过程,由主动行为变为了被动行为，控制权颠倒过来了，这就是“控制反转”这个名称的由来。

        

2. **那么实现依赖注入这种设计思想方式有哪些呢？**

    - constructor arguments（构造函数参数注入）
    - arguments to a factory method （工厂方法参数注入）

    笙式解读工厂方法：主要目的就是创建对象；创建对象原理：构造方法常常被设置为私有方法，工厂方法通常作为静态方法，定义在方法所实例化的类中，易于供外界调用(类名.工厂方法名)，类似于包装了构造函数 

    ```java
    class Complex {
         public static Complex fromCartesianFactory(double real, double imaginary) {
             return new Complex(real, imaginary);
         }
         public static Complex fromPolarFactory(double modulus, double angle) {
             return new Complex(modulus * cos(angle), modulus * sin(angle));
         }
         private Complex(double a, double b) {
             //...
         }
    }
    
    Complex product = Complex.fromPolarFactory(1, pi);
    ```

    -    properties that are set on the object instance after it is constructed or returned from a factory method.（在对象被创建或者来自工厂方法的返回参数之后，对象实例设置属性注入）

###   2.2	Bean 是什么

在 Spring 中，构成应用程序主干并由 Spring IoC 容器管理的对象  ;  bean 是由 Spring IoC 容器实例化、组装和管理的对象

下图显示了 Spring 如何工作的高级视图。您的应用程序类与配置元数据相结合，因此，在`ApplicationContext`创建和初始化之后，您就有了一个完全配置且可执行的系统或应用程序。

![image-20211025094927316](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20211025094927316.png)

基于 XML 的配置元数据的基本结构：  ( Bean 以及它们之间的依赖关系反映在容器使用的配置元数据中 ) 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- 
		bean 对象
		id 对象名   class d所在的地址（索引）	
         ref：引用Spring容器中创建好的对象
         value ：具体的值，基本数据类型
	-->
    <bean id="..." class="...">  
        <!-- collaborators and configuration for this bean go here -->
    </bean>

    <bean id="..." class="...">
        <!-- collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions go here -->

</beans>
```



## 三.IoC创建对象的方式

### 3.1无参构造函数注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- 当该对象无无参构造函数，将报错 -->
    <bean id="user" class="com.Al_tair.user.User">
        <property name="name" value="lns"/>
    </bean>


</beans>
```

```java

public class User {
    String name;

    public User(String name){
        this.name = name;
    }
    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                '}';
    }
}

```

无参构造函数无法找到报错

![image-20211026205041393](Spring.assets/image-20211026205041393.png)

### 3.2有参构造函数

- 下标赋值

```xml
<bean id="user" class="com.Al_tair.user.User">
    <constructor-arg index="0" value="lns"/>
</bean>
```

- 类型赋值

```xml
<bean id="user" class="com.Al_tair.user.User">
    <constructor-arg type="java.lang.String" value="罗念笙"/>
</bean>
```

- 直接通过参数赋值

```xml
<bean id="user" class="com.Al_tair.user.User">
    <constructor-arg name="name" value="lns"/>
</bean>
```

The `ApplicationContext` lets you read bean definitions and access them, as the following example shows:

```java
// create and configure beans 创建和配置bean
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");

// retrieve configured instance 接受配置实例
PetStoreService service = context.getBean("petStore", PetStoreService.class);

// use configured instance 使用配置实例
List<String> userList = service.getUsernameList();
```

总结：在配置文件在创建和配置的时候，容器中的对象已经初始化了！

## 四.	Spring配置说明

- 别名 alias:可以用另外一个name代替原id名

    ```xml
    <bean id="user" class="com.Al_tair.user.User"></bean>
    <alias name="user" alias="user2"/>
    ```

- Bean配置  

    ```xml
    <!--  
          id bean的唯一标识符 可以被认为是对象名
          class bean对象所对应的全限定名:包名+类名
          name 别名 作用比alias还强大 可以取多个别名(中间可以用空格 or , or ;等隔开)
    -->
    <bean id="SpringName2" class="com.Al_tair.helloSpring.HelloSpring" name="SpringName3 SpringName4">
        <property name="name" value="HelloSpring"/>
    </bean>
    ```

- 导入import

    ```xml
    <!-- 创建applicationContext xml文件 
             导入beans.xml && beans2.xml文件
        -->
    <import resource="beans.xml"/>
    <import resource="beans2.xml"/>
    ```

## 五.详细讲解依赖注入

### 5.1构造器注入

回顾第三节我已经实现了无参构造函数和有参构造函数的注入

### 5.2Set方式注入（重点）

测试场景：学生类

```java
// set get toString 方法省略
public class Address {
    public String Address;
}

public class Student {
    private String name;
    private Address address;
    private String[] books;
    private List<String> hobby;
    private Map<String,String> cards;
    private Set<String> games;
    private String son;
    private Properties info;
}
```

  配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- 创建address对象 -->
    <bean name="address" class="com.Al_tair.pojo.Address">
        <property name="address" value="西安"/>
    </bean>


    <bean name="students" class="com.Al_tair.pojo.Student">
        <!-- 直接赋值 -->
        <property name="name" value="罗念笙"/>

        <!-- 对象赋值 -->
        <property name="address" ref="address"/>

        <!-- array -->
        <property name="books">
            <array>
                <value>梦里花落知多少</value>
                <value>懦弱的勇气</value>
                <value>朝花夕拾</value>
                <value>童年</value>
            </array>
        </property>

        <!-- list -->
        <property name="hobby">
            <list>
                <value>运动</value>
                <value>java</value>
                <value>嵌入式</value>
            </list>
        </property>

        <!-- map -->
        <property name="cards">
            <map>
                <entry key="ID" value="1234567"/>
                <entry key="bankId" value="789456123"/>
            </map>
        </property>

        <!-- Set -->
        <property name="games">
            <set>
                <value>LOL</value>
                <value>王者荣耀</value>
                <value>QQ飞车</value>
                <value>哈利波特</value>

            </set>
        </property>

        <!-- null -->
        <property name="son">
            <value>null</value>
        </property>


        <!-- properties -->
        <property name="info">
            <props>
                <prop key="user">root</prop>
                <prop key="password">123456</prop>
            </props>
        </property>
    </bean>
</beans>
```



### 5.3拓展方式注入

**namespace方式**

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    // p命名空间 
    xmlns:p="http://www.springframework.org/schema/p"
    // c命名空间
    xmlns:c="http://www.springframework.org/schema/c"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
</beans>
```

**namespace实现代码**

测试类

```java
public class TestCP {
    private String name;
    private int age;
    public TestCP(){
        System.out.println("无参构造函数");
    }

    public TestCP(String name,int age){
        System.out.println("有参构造函数");
        this.age = age;
        this.name = name;
    }
    
    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

配置文件

```xml
    <!-- c命名空间,有参构造函数注入: construct-args -->
    <bean id="user2" class="com.Al_tair.test.TestCP" c:name="罗念笙" c:age="18"/>

    <!-- p命名空间,无参构造函数注入 :property -->
    <bean id="user" class="com.Al_tair.test.TestCP" p:name="罗念笙" p:age="18"/>
```

### 5.4 Bean作用域

|                            Scope                             |                   Description  information                   |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| [singleton](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-singleton) | （默认）将单个 bean 定义范围限定为每个 Spring IoC 容器的单个对象实例 |
| [prototype](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-prototype) |         将单个 bean 定义范围限定为任意数量的对象实例         |
| [request](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-request) |      将单个 bean 定义范围限定为单个 HTTP 请求的生命周期      |
| [session](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-session) |      将单个 bean 定义范围限定为 HTTP 的生命周期Session       |
| [application](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-application) |           将单个 bean 定义范围限定为ServletContext           |
| [websocket](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#websocket-stomp-websocket-scope) |             将单个 bean 定义范围限定为WebSocket              |



#### 5.41The Singleton Scope（默认作用域）

Only **one shared instance** of a singleton bean is managed, and all requests for beans with an ID or IDs that match that bean definition result in that one specific bean instance being returned by the Spring container

总结来说就是如果您在单个 Spring 容器中为特定类定义一个 bean，则 Spring 容器会创建该 bean 定义定义的类的一个且仅一个实例

![image-20211029104915396](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20211029104915396.png)

以下两种形式效果一样，因为Singleton作为默认作用域

```xml
<bean id="accountService" class="com.something.DefaultAccountService"/>

<!-- the following is equivalent, though redundant (singleton scope is the default) -->
<bean id="accountService" class="com.something.DefaultAccountService" scope="singleton"/>
```

#### 5.42The Prototype Scope

The non-singleton prototype scope of bean deployment results in the **creation of a new bean** **instance** every time a request for that specific bean is made

bean 部署的非单一原型作用域导致每次对特定 bean 发出请求时都会创建一个新的 bean 实例

![image-20211029105623969](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20211029105623969.png)

The following example defines a bean as a prototype in XML:

```xml
<bean id="accountService" class="com.something.DefaultAccountService" scope="prototype"/>
```

#### 5.43其余的request,session,application这些只能在**web开发**中使用到！



## 六.Bean的自动装配

Spring中的三种的装配方式

- 在xml中显示的配置（如上文）
- 在java中显示的配置
- 隐式的自动装配（下文即将讲述）

测试环境: 一个人拥有两个宠物（猫和狗）

```java
package com.Al_tair.Pojo;
/**
 * @author Al_tair
 * @date 2021/10/29-11:52
 */
public class People {
    private Dog dog;
    private Cat cat;
    private String name;

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setDog(Dog dog) {
        this.dog = dog;
    }

    public void setCat(Cat cat) {
        this.cat = cat;
    }

    public Dog getDog() {
        return dog;
    }

    public Cat getCat() {
        return cat;
    }

    @Override
    public String toString() {
        return "People{" +
                "dog=" + dog +
                ", cat=" + cat +
                ", name='" + name + '\'' +
                '}';
    }
}
```

### 6.1byName自动装配

这种模式由**属性名称**指定自动装配。Spring 容器看作 beans，在 XML 配置文件中 beans 的 *autowire* 属性设置为 *byName*。然后，它尝试将它的属性与配置文件中定义为相同名称的 beans 进行匹配和连接。如果找到匹配项，它将注入这些 beans，否则，它将抛出异常。

```xml
<bean id="dog" class="com.Al_tair.Pojo.Dog"/>
<bean id="cat" class="com.Al_tair.Pojo.Cat"/>
<bean id="people2" class="com.Al_tair.Pojo.People" autowire="byName"/>
```

### 6.2byType自动装配

如果容器中存在一个与**指定属性类型**相同的bean，那么将与该属性自动装配；如果存在多个该类型bean，那么抛出异常，并指出不能使用byType方式进行自动装配；如果没有找到相匹配的bean，则什么事都不发生

```xml
<bean id="dog" class="com.Al_tair.Pojo.Dog"/>
<bean id="cat" class="com.Al_tair.Pojo.Cat"/>
<bean id="people" class="com.Al_tair.Pojo.People" autowire="byType">
```

### 6.3使用注解实现自动装配

The introduction of annotation-based configuration raised the question of whether this approach is “better” than XML
通过注解配置比xml配置好

使用注解前须知:

- 导入约束：context 约束
- 配置注解的支持：    <context:annotation-config/>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>
</beans>
```

#### **@Autowired**

```java
// 底层源码:
// 在容器的启动过程中，会初始化很多bean，这也是spring的核心之一（IOC）。但是在注入的过程中，扫描到公共方法中要注入的bean，并未找到，强行注入就会注入失败。我们又不能单独的去除改方法，所以我们采取的思想就是有bean就注入，没有就不注入。解决办法就是@Autowired(required=false)。
public @interface Autowired {
    boolean required() default true;
}
```

xml配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
    <context:annotation-config/>

    <bean id="dog" class="com.Al_tair.Pojo.Dog"/>
    <bean id="cat" class="com.Al_tair.Pojo.Cat"/>
    <bean id="people" class="com.Al_tair.Pojo.People"/>

</beans>
```

1. 应用于构造函数

    ```java
    public class People {
        private Dog dog;
        private Cat cat;
        private String name;
    
        public People(){}
    
        @Autowired
        public People(Dog dog,Cat cat){
            this.cat = cat;
            this.dog = dog;
        }
    }
    ```

2. 传统 setter 方法

    ```java
    @Autowired
    public void setDog(Dog dog) {
        this.dog = dog;
    }
    @Autowired
    public void setCat(Cat cat) {
        this.cat = cat;
    }
    ```

3. 应用于属性参数

    ```java
    public class People {
        @Autowired
        private Dog dog;
        @Autowired
        private Cat cat;
    }
    ```

总结：用带`@Autowired`注释的注入点的类型相同。否则，注入可能会因运行时“未找到类型匹配”错误而失败，如果遇到多个同类型的将无法实现注入，我们就需要用到**@Qualifier**来进行指定名字的注入，例子如下

```java
public class People {
    @Autowired
    @Qualifier(value = "dog3242")
    private Dog dog;
}

// baen2.xml
//    <bean id="dog3242" class="com.Al_tair.Pojo.Dog"/>
//    <bean id="dog" class="com.Al_tair.Pojo.Dog"/>
```

#### **@Resource**

java自带的注解，功能比@Autowired更加强

实现注解注入的查询方式： 先对照id名字，如果没找到对应的，还会进行类型的寻找（只有当名字和类型都不一样的时候才会报错）

```java
// 截取部分底层代码
// 是通过 byName byType进行匹配
public @interface Resource {
    String name() default "";
    Class<?> type() default Object.class;
}
```

代码验证

```java
public class People {
    @Resource
    private Dog dog;
    @Resource
    private Cat cat;
}

// baen2.xml
/*    <bean id="dog3242" class="com.Al_tair.Pojo.Dog"/>
      <bean id="dog" class="com.Al_tair.Pojo.Dog"/>
      <bean id="cat41234" class="com.Al_tair.Pojo.Cat"/>
      <bean id="cat" class="com.Al_tair.Pojo.Cat"/>
 */
```

#### @Component

组件，放在类上进行自动创建bean

约束条件：component-scan  指定要扫描的包，该包下的注解就会生效

```java
@Repository  // 等价于xml配置中的<bean id="name" class="com.Al_tair.dao.UserDao">
public class UserDao {
    @Value("罗念笙")  // 等价于xml配置中的<property name="name" value="罗念笙"></property>
    public String name;
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
    <!-- 指定要扫描的包，该包下的注解就会生效 -->
    <context:component-scan base-package="com.Al_tair"/>
    <context:annotation-config/>

</beans>
```

衍生自动注解

```java
/*
	三个衍生注解分别对应MVC三层架构中的 Dao层 Service层  Controller层
    @Controller
    @Repository      均是 @Component 的衍生注解
    @Service
*/
```

![image-20211102163719677](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20211102163719677.png)

#### 自动注解 Vs Xml配置（总结）

- xml更加强大，适用于任何的范围，维护简单！
- 自动注解适用范围有限，且维护麻烦，分布在各个类

个人觉得最优操作（限于Spring）：

- xml用来创建bean

- 自动注解用来进行属性的注入

    但是要记住需要开启注解的支持

## 七.使用Java的方式配置Spring

### @Configuration    &&     @Bean

实体类

```java
@Component  // 说明这个类被Spring接管，注册到容器中
public class User {
    @Value("罗念笙")
    public String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                '}';
    }
}
```

配置类

```java
/**
 * @Configuration 也会被Spring接管，注册到容器中吗，因为它本身就是一个@Component
 * @Configuration代表这个是配置类 bean.xml能做的，在该配置类中也能做
 */
@Configuration
public class JavaConfig {
    // 代表创建bean对象 id 就是该方法的名字 user   class 就是该方法返回值User对象
    @Bean
    public User user(){
        return new User();
    }
}
```

测试类

```java
public class MyText {
    public static void main(String[] args) {
        // 如果我们完全用java配置类方式去做，我们只能通过AnnotationConfig上下文获取容器，通过配置类对象的.class去加载
        ApplicationContext javaConfig = new AnnotationConfigApplicationContext(JavaConfig.class);

        User user = javaConfig.getBean("user", User.class);

        System.out.println(user.name);

    }
}
```



## 八.代理模式（AOP底层）

> 代理模式为另一个对象提供一个替身或占位符以控制对这个对象的访问，被代理的对象可以是远程对象，创建开销大的对象或需要安全控制的对象
>
> ​																																														--《Head First 设计模式》

### 8.1AOP概述

​		 AOP 英文：Aspect Oriented Programming  即 面向切面编程  和Ioc一样是一种设计思想

​		目的：处理OOP在解决侵入式业务上的不足  （什么是**侵入性业务**？类似日志统计、性能分析等就属于**侵入性业务**）

​		代理模式:   静态代理    动态代理

### 8.2静态代理    

组成分析：

- 抽象行为（Subject）：一般会使用接口或者抽象类来实现 例如：帮助买房的人挑选房型，帮助房东签订合同等买房行为
- 委托方（RealSubject）  ：委托代理方的那个人 例如：房东
- 代理方（ProxySubject）：代理委托方，做一些副属行为）  例如：房产中介
- 客户（client） ： 找代理方办事！ 例如：买房的人

接下来我们通过 装修的人 -- 装修中介商  -- 装修工  身份来实现代码

Subject类  装修

```java
// Java中的静态代理要求代理类(ProxySubject)和委托类(RealSubject)都实现同一个接口(Subject)
// 作为接口实现房屋装修
public interface Subject {
    // 装修
    public void decorate();
}
```

RealSubject类 装修工

```java
// 委托类(RealSubject): 装修工
public class RealSubject implements Subject{
    public void decorate() {
        System.out.println("装修工需要通过装修来糊口!");
    }
}
```

ProxySubject类  装修中介

```java
// 代理类(ProxySubject): 装修中介公司
public class ProxySubject implements Subject{
    private RealSubject  realSubject;
    // 设计房间
    public void decorate() {
        System.out.println("设计房间");
    }

    public ProxySubject() {
    }

    public ProxySubject(RealSubject realSubject) {
        this.realSubject = realSubject;
    }

    // 装修样式
    public void style(){
        System.out.println("看装修房间的款式！");
    }

    // 收中介费
    public void fee(){
        System.out.println("收中介费");
    }
}
```

client类 客户

```java
public class MyText {
    public static void main(String[] args) {
        RealSubject realSubject = new RealSubject();
        realSubject.decorate();
        ProxySubject proxySubject = new ProxySubject(realSubject);
        proxySubject.decorate();
        proxySubject.style();
        proxySubject.fee();
    }
}
```

深入理解静态代理

![image-20211104150354249](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20211104150354249.png)

实现用户的增删改查

接口类

```java
public interface Userdao {
    // 增 删 改 查
    public void add();
    public void delete();
    public void update();
    public void find();
}
```

实现类

```java
public class UserdaoImpl implements Userdao{
    public void add() {
        System.out.println("增加数据");
    }

    public void delete() {
        System.out.println("删除数据");
    }

    public void update() {
        System.out.println("更新数据");
    }

    public void find() {
        System.out.println("查找数据");
    }
}
```

事务类（负责代理）

```java
public class UserServiceimpl implements Userdao{
    private UserdaoImpl userdao;

    public void setUserdao(UserdaoImpl userdao) {
        this.userdao = userdao;
    }

    public void add() {
        addEvent("add");
        userdao.add();
    }

    public void delete() {
        userdao.delete();
    }

    public void update() {
        userdao.update();
    }

    public void find() {
        userdao.find();
    }

    // 增加事务
    public void addEvent(String event){
        System.out.println("[debug]增加"+event);
    }
}
```

客户类

```java
public class Client {
    public static void main(String[] args) {
        UserdaoImpl userdao = new UserdaoImpl();
        UserServiceimpl userServiceimpl = new UserServiceimpl();
        userServiceimpl.setUserdao(userdao);
        userServiceimpl.add();
        userServiceimpl.delete();
        userServiceimpl.find();
        userServiceimpl.update();
    }
}
```

结果

![image-20211104203735021](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20211104203735021.png)

静态代理的好处：

- 可以使委托方做事更加简单，不用关注怎么实现委托事物、
- 各司其职，分工明确，针对性强
- 公共事务去扩展的时候方便集中管理，比如代理方可以优化委托事务的实现

静态事务的坏处：

- 每创建事务就要更改代理方，开放效率降低

### 8.3动态代理



​		
