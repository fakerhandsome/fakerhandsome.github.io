---
id: SSM三层架构
title: SSM三层架构的关系
---



#### SSM框架下，spring中service和dao层的作用与三者之间的关系

**1、java web 中dao 层和service层都使用接口，是否是为使用接口而使用接口？**

一个dao或者一个service都是一个接口，然后再一个类去实现，为什么不直接使用一个类呢？在入门级（单表）的SSM+maven代码里面，我们甚至可以看到dao和service的接口类中代码内容都是一样的，这个作何理解？

**java web中的三层架构：**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190414150344909.?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NvY29fX19fXw==,size_16,color_FFFFFF,t_70)

其中，表示层一般是采用 MVC 架构模式，业务层有事务脚本模式、领域模型模式等，持久层有数据映射器模式（Hibernate即是典型的）、入口模式（MyBatis、JDBC）。企业应用中最关键的显然是业务层。而对于初学者来说，事务脚本模式是最为简单，最容易掌握的。如果开发团队面向对象设计能力一般，而且业务逻辑相对简单，业务层一般都会采用事务脚本模式。

所谓事务脚本模式，就是将业务层的对象分为三类，按照下图的方式组织起来（下图是用EA画的UML类图，一个简单的学生管理的业务层设计）。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019041415044654.?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NvY29fX19fXw==,size_16,color_FFFFFF,t_70)

如上图所示，在事务脚本模式中，有三类对象。其中，Service类封装业务流程（或者说是界面上的业务流程），DAO类封装对持久层的访问，DTO类封装业务实体对象。各个对象之间的关系如上图所示，这就是所谓业务逻辑的组织方式。

为什么要用Service接口和DAO接口？
其实就是为了解耦，解耦说的意思是你更改某一层代码，不会影响我其他层代码，如果你会像spring这样的框架，你会了解面向接口编程，表示层调用控制层，控制层调用业务层，业务层调用数据访问层。举个例子，用DAO接口，那么持久层用Hibernate，还是用myBatis，还是 JDBC，随时可以替换，不用修改业务层Service类的代码。

具体来讲：标准主流现在的表现层都是采用MVC综合设计模式，最终目的达到解耦， 初期也许都是new对象去调用下一层，比如你在业务层new一个DAO类的对象，调用DAO类方法访问数据库，这样写是不对的，因为在业务层中是不应该含有具体对象，最多只能有引用，如果有具体对象存在，就耦合了。 当那个对象不存在，我还要修改业务的代码，这不符合逻辑。好比主板上内存坏了，我换内存，没必要连主板一起换。我不用知道内存是哪家生产，不用知道多大容量，只要是内存都可以插上这个接口使用。这就是MVC的意义。
其实因为入门级程序做东西分层次不是那么严格，涉及到的业务很少，举个最简单的例子，你做一个分页的功能，数据1000条，你20条在一个页，你可以把这个功能写成工具类封装起来，然后在业务层里调用这个封装的方法，这才是业务里真正干得事，只要没访问数据库的，都要在业务里写。
DAO一定是和数据库的每张表一一对应，而service则不是。项目中一个service和一个DAO其实也一样可以操作数据库，只不过那要是表非常多，出问题了，那找起来多麻烦，而且太乱了。

一个DAO单独对1个表进行操作。一个Service可以操作几个DAO。

构建业务层的模式：Service + DAO,即DAO中只做CRUD及类似的简单操作(称之为功能点,不包含业务逻辑),Service中通过调用一个或多个DAO中的功能点来组合成为业务逻辑.Service的数量应该由功能模块来决定。在这种模型中业务逻辑是放在Service中的,事务的边界也应该在Service中控制. 当然,直接在Service中控制事务会引入非业务逻辑的代码,幸好spring的AOP可以解决这个问题,这也是引入Spring的原因之一。如果说到缺点,就在于对某些对象的操作就是简单的CRUD，Service层显得累赘。

**2、java web中的service，dao，po分别是什么意思和什么作用**

Service:service层是在mcv三层模式中新添加一层，能够更加清晰的定义应用程序的边界，需要操作数据的时候，通过service层访问DAO层来实现。service层做的事情，不仅仅是调用DAO操作数据，还会包含了一定的业务逻辑。整个程序设计就变成了针对服务的设计。

DAO：Data Access Object是一个数据访问接口，数据访问：顾名思义就是与数据库打交道。夹在业务逻辑与数据库资源中间。是MVC模式中Model层

PO：Persistent Object即持久对象，它们是由一组属性和属性的get和set方法组成。可以看成是与数据库中的表相映射的java对象
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190414150556382.?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NvY29fX19fXw==,size_16,color_FFFFFF,t_70)
Dao主要做数据库的交互工作
Modle 是模型 存放你的实体类
Service 做相应的业务逻辑处理
Action是一个控制器
Action像是服务员，顾客点什么菜，菜上给几号桌，都是ta的职责；Service是厨师，action送来的菜单上的菜全是ta做的；Dao是厨房的小工，和原材料(通过mybatis操作数据库)打交道的事情全是ta管。对象的调用流程：JSP—Action—Service—DAO—mybatis—数据库。

**3、service层事物控制的理解**

一般情况下，我们会把事务控制在service层。

例如我们的一个业务：删除A记录，插入B记录（需要在一个事务里进行），如果我们把这个业务逻辑写在了action层，我们再action层调用删除A的service，然后再调用插入B的service，如果说插入B失败了，那我们删除A这个操作将不能回滚，因为事务控制在了service层，这样写已不是一个事务。删除A操作的service已经完成，事务已经提交了，插入B的操作在另外的事务里运行。根据需要，业务逻辑尽量放在service层。通过配置spring事务控制的传播行为，在service层可以达到大部分的业务事务要求，而不需另加一层。spring的事务有两种一种是声明式事务，一种是编程式事务。

action和dao层，会使用一些框架技术。比如action层可能选择有springmvc、struts等，dao层有hibernate、mybatis等选择，所以action的dao有可能根据情况变化，而service层关注业务逻辑，业务代码都是自己完成的，代码对自己是透明的。

我们更应该把与业务相关的代码移至service层控制事务。这主要发生在我们把整个业务逻辑放在了service的一个方法，而这个方法以及调用的方法的事务配置为required（或其他），但业务的部分操作需要在不同的事务中进行，我们不想写另外的方法，也不想去更改事务配置，所以引入support层（或许你说可以把这种逻辑向action层移动，在action层处理，但记住我们的前提，action的框架是会变的，我们想尽量做到更改action层时，更简单。而且从分工来说，action层应该只关注视图逻辑，个人自扫门前雪，休管他人瓦上霜）。support层当然不是只为处理这种事务问题的，我把它定义为业务处理时需要的一些辅助层，可以协助处理业务，比如刚才说的事务问题，还有可以提供工具类支持等。

对于dao层，应该只关注数据库连接执行结果封装这些事。