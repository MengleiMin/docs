# Welcome to Spring Boot 入门  

## *Spring 架构*


* Spring 整体架构图

 ![Spring整体架构图](/public/img/2020-8-18-Spring.png)

- AOP (Aspect Oriented Programming)  
面向切面编程，通过预编译方式和运行期间动态代理实现程序功能的统一维护的一种技术。 AOP是OOP的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。

- Core Container

<!-- more -->

小知识:
* IoC, Inversion of Control, 控制反转  
IoC的实现方式与DI的关系？  
   - 依赖查找(Dependency Lookup)：容器中的受控对象通过容器的API来查找自己所依赖的资源和协作对象。这种方式虽然降低了对象间的依赖，但是同时也使用到了容器的API，造成了我们无法在容器外使用和测试对象。依赖查找是一种更加传统的IoC实现方式。      
   - 依赖注入(Dependency Injection)：这就是DI，字面上理解，依赖注入就是将服务注入到使用它的地方。对象只提供普通的方法让容器去决定依赖关系，容器全权负责组件的装配，它会把符合依赖关系的对象通过属性（JavaBean中的setter）或者是构造子传递给需要的对象。相对于IoC而言，依赖注入(DI)更加准确地描述了IoC的设计理念。所谓依赖注入，即组件之间的依赖关系由容器在应用系统运行期来决定，也就是由容器动态地将某种依赖关系的目标对象实例注入到应用系统中的各个关联的组件之中。
   - IoC是Spring的核心，贯穿始终。对于Spring框架来说，就是由Spring来负责控制对象的生命周期和对象间的关系。
   Spring中DI有两种实现方式---Setter方式(传值方式)和构造器方式(引用方式)。 


