#[第七章 PHP设计模式](https://github.com/liujingyu/The-road-of-my-PHP/blob/master/Book-7.md)

##1. 设计模式介绍及原则

###1.1 什么是设计模式
    设计模式（Design pattern）是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结。使用设计模式是为了可重用代码、让代码更容易被他人理解、保证代码可靠性。

###1.2 设计原则

* 单一职责原则(Single Responsibility Principle, SRP)
    定义:一个对象应该只包含单一的职责，并且该职责被完整地封装在一个类中。（Every object should have a single responsibility, and that responsibility should be entirely encapsulated by the class.），即又定义有且仅有一个原因使类变更。
    类的职责要单一，不能将太多的职责放在一个类中。（高内聚、低耦合）

* 开闭原则(Open - Closed Principle, OCP)
    定义:一个软件实体(如类、模块和函数)应该对扩展开放，对修改关闭.  意思是,在一个系统或者模块中,对于扩展是开放的,对于修改是关闭的,一个 好的系统是在不修改源代码的情况下,可以扩展你的功能. 而实现开闭原则的关键就是抽象化.
    对扩展开放，对修改关闭（设计模式的核心原则是）

* 里氏代换原则(Liskov Substitution Principle, LSP)
    定义：第一种定义方式相对严格：如果对每一个类型为S的对象o1，都有类型为T的对象o2，使得以T定义的所有程序P在所有的对象o1都代换成o2时，程序P的行为没有变化，那么类型S是类型T的子类型。
    任何基类可以出现的地方,子类也可以出现

* 依赖倒转原则

    定义：高层模块不应该依赖低层模块，它们都应该依赖抽象。抽象不应该依赖于细节，细节应该依赖于抽象。简单的说，依赖倒置原则要求客户端依赖于抽象耦合。原则表述：
        1）抽象不应当依赖于细节；细节应当依赖于抽象；
        2）要针对接口编程，不针对实现编程。
    要依赖抽象,而不要依赖具体的实现.

    依赖注入的三种写法：
    •构造注入(Constructor Injection)：通过构造函数注入实例变量。
    •设值注入(Setter Injection)：通过Setter方法注入实例变量。
    •接口注入(Interface Injection)：通过接口方法注入实例变量。

* 合成/聚合复用原则(Composite/Aggregate ReusePrinciple ，CARP)

    定义：经常又叫做合成复用原则（Composite ReusePrinciple或CRP），尽量使用对象组合，而不是继承来达到复用的目的。

    要尽量使用对象组合,而不是继承关系达到软件复用的目的
* 接口隔离原则

    定制服务的例子，每一个接口应该是一种角色，不多不少，不干不该干的事，该干的事都要干。

* 迪米特法则(Law of Demeter，LoD：系统中的类,尽量不要与其他类互相作用,减少类之间的耦合度)

    定义：又叫最少知识原则（Least Knowledge Principle或简写为LKP）几种形式定义：
    (1) 不要和“陌生人”说话。英文定义为：Don't talk to strangers.
    (2) 只与你的直接朋友通信。英文定义为：Talk only to your immediatefriends.
    (3) 每一个软件单位对其他的单位都只有最少的知识，而且局限于那些与本单位密切相关的软件单位。


##2. Creational (创建型)

###2.1 Simple Factory
###2.2 Factory Method
###2.3 Abstract Factory
###2.4 Builder
###2.5 Prototype

##3. Structural (结构型)
###3.1 Adapter
###3.2 Bridge
###3.3 Composite
###3.4 Decorator
###3.5 Facade
###3.6 Flyweight
###3.7 Proxy

##4. Behavioral (行为型)
###4.1 Interpreter
###4.2 Template method
###4.3 Chain of Responsibility
###4.4 Command
###4.5 Iterator
###4.6 Mediator
###4.7 Memento
###4.8 Observer
###4.9 State
###4.10 Strategy
###4.11 Visitor

