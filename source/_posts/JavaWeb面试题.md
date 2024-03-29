title: "JavaWeb面试题"
date: 2016-05-15 10:18:47
tags:
---

### Java及Web服务器
1. Java中数据类型的长度？可选这以下类型提问：
Int 4、short 2、long 8、byte 1、float 4、double 8、char 2、boolean 1
2. int和Integer的区别？
Java是一个近乎纯洁的面向对象编程语言，但是为了编程的方便还是引入了基本数据类型，但是为了能够将这些基本数据类型当成对象操作，Java为每一个基本数据类型都引入了对应的包装类型（wrapper class），int的包装类就是Integer，从Java 5开始引入了自动装箱/拆箱机制，使得二者可以相互转换。 
Java 为每个原始类型提供了包装类型：    
原始类型——boolean，char，byte，short，int，long，float，double 
包装类型——Boolean，Character，Byte，Short，Integer，Long，Float，Double
3. String s = new String("xyz");创建了几个String Object？二者之间有什么区别？
两个或一个，“xyz”对应一个对象，这个对象放在字符串常量缓冲区，常量”xyz”不管出现多少遍，都是缓冲区中的那一个。New String每写一遍，就创建一个新的对象，它一句那个常量“xyz”对象的内容来创建出一个新String对象。如果以前就用过“xyz”，这句代表就不会创建“xyz”自己了，直接从缓冲区拿。
4. String和StringBuffer的区别
JAVA平台提供了两个类：String和StringBuffer，它们可以储存和操作字符串，即包含多个字符的字符数据。这个String类提供了数值不可改变的字符串。而这个StringBuffer类提供的字符串进行修改。当你知道字符数据要改变的时候你就可以使用StringBuffer。典型地，你可以使用StringBuffers来动态构造字符数据。另外，String实现了equals方法，new String(“abc”).equals(newString(“abc”)的结果为true，而StringBuffer没有实现equals方法，所以，new StringBuffer(“abc”).equals(newStringBuffer(“abc”)的结果为false。
<!--more-->
5. 在Java中如何将日期转换成指定格式的字符串？使用SimpleDateFormat。    
【追问】SimpleDateFormat是否是线程安全的？如果不是线程安全的如何处理？
非线程安全的，最简单的解决方案是每次都new的新的SimpleDateFormat。如果回答使用第三方的工具，如Apache common lang或JodaTime中的api也算正确。
6. `@Autowired`和`@Resource`的区别    
@Autowired是Spring提供的注解，默认按类型注入。    
@Resource是JavaEE提供的注解，可按Name注入。
7. Java中ArrayList和LinkedList区别
    1)	ArrayList是实现了基于动态数组的数据结构，LinkedList基于链表的数据结构。
    2)	对于随机访问get和set，ArrayList觉得优于LinkedList，因为LinkedList要移动指针。
    3)	对于新增和删除操作add和remove，LinedList比较占优势，因为ArrayList要移动数据。
    4)	对ArrayList和LinkedList而言，在列表末尾增加一个元素所花的开销都是固定的。对ArrayList而言，主要是在内部数组中增加一项，指向所添加的元素，偶尔可能会导致对数组重新进行分配；而对LinkedList而言，这个开销是统一的，分配一个内部Entry对象。
    5)	在ArrayList的中间插入或删除一个元素意味着这个列表中剩余的元素都会被移动；而在LinkedList的中间插入或删除一个元素的开销是固定的。
    6)	LinkedList不支持高效的随机元素访问。
    7)	ArrayList的空间浪费主要体现在在list列表的结尾预留一定的容量空间，而LinkedList的空间花费则体现在它的每一个元素都需要消耗相当的空间。
8. 在一个类中，定义了静态字段，实例字段、静态块。那么在实例化该类时，初始化的顺序是？    
静态变量 -- 静态化初始化块 -- 变量 -- 构造器    
【追问】如果在父类和子类中都定义了静态字段，实例字段、静态块。那么实例化子类时，初始化顺序是？
父类静态变量 -- 父类静态化初始化块 -- 子类静态变量 -- 子类静态初始化块 -- 父类变量 -- 构造器 -- 子类变量 -- 子类构造器
9. Java中finally关键字的作用是什么？    
Finally是对Java异常处理模型的补充，不管有无异常发生，finally中的代码都会执行。    
【追问】假设在try中的return x+y；其中x=1，y=1，如果在finally中修改了x=2，那么return返回得到的值是多少。为什么？
返回值为2，finally是在return后的表达式执行后执行的，先把返回值保存起来，所以无法finally中修改了什么返回值都不变。
10. Java中的方法覆盖(Overriding)和方法重载(Overloading)是什么意思？
Java中的方法重载发生在同一个类里面两个或者是多个方法的方法名相同但是参数不同的情况。与此相对，方法覆盖是说子类重新定义了父类的方法。方法覆盖必须有相同的方法名，参数列表和返回类型。覆盖者可能不会限制它所覆盖的方法的访问。
11. Java8有哪些新特性？    
Lambda表达式、提供接口的默认方法、函数式接口、新的Date API等，只要回答出Lambda表达式可认为本题回答正确。
12. 介绍一下 Hibernate 的二级缓存    
按照以下思路来回答：（1）首先说清楚什么是缓存。（2）再说有了 hibernate 的 Session 就是一级缓存，即有了一级缓存，为什么还要有二级缓存。（3）最后再说如何配置 Hibernate
（1）缓存就是把以前从数据库中查询出来和使用过的对象保存在内存中（一个数据结构中），这个数据结构通常是或类似 Hashmap，当以后要使用某个对象时，先查询缓存中是否有这个对象，如果有则使用缓存中的对象，如果没有则去查询数据库，并将查询出来的对象保存在缓存中，以便下次使用。下面是缓存的伪代码：
引出 hibernate 的第二级缓存，用下面的伪代码分析了 Cache 的实现原理
Dao
```
{
 		hashmap map = new map();
 		User getUser(integer id)
 		{
 			User user =map.get(id)
 			if(user ==null)
 			{
 				user =session.get(id);
 				map.put(id,user);
 			}
 			return user;
 		}
}
```

Dao
```
{
 		Cache cache = null
 		setCache(Cache cache)
 		{
 			this.cache =cache
 		}
 		User getUser(int id)
 		{
 			{
 				Useruser = cache.get(id);
 				if(user==null)
 				{
 					user= session.get(id);
 					cache.put(id,user);
 				}
 				returnuser;
 			}
 			return session.get(id);
 		}
}
```
（2）Hibernate 的 Session 就是一种缓存，我们通常将之称为 Hibernate 的一级缓存，当想使用 session 从数据库中查询出一个对象时，Session 也是先从自己内部查看是否存在这个对象，存在则直接返回，不存在才去访问数据库，并将查询的结果保存在自己内部。由于Session 代表一次会话过程，一个 Session 与一个数据库连接相关连，所以 Session 最好不要长时间保持打开，通常仅用于一个事务当中，在事务结束时就应关闭。并且 Session 是线程不安全的，被多个线程共享时容易出现问题。通常只有那种全局意义上的缓存才是真正的缓存应用，才有较大的缓存价值，因此，Hibernate 的 Session 这一级缓存的缓存作用并不明显，应用价值不大。Hibernate 的二级缓存就是要为 Hibernate 配置一种全局缓存，让多个线程和多个事务都可以共享这个缓存。我们希望的是一个人使用过，其他人也可以使用，session 没有这种效果。
（3）二级缓存是独立于 Hibernate 的软件部件，属于第三方的产品，多个厂商和组织都提供有缓存产品，例如，EHCache和OSCache等等。在 Hibernate 中使用二级缓存，首先就要在hibernate.cfg.xml 配置文件中配置使用哪个厂家的缓存产品，接着需要配置该缓存产品自己的配置文件，最后要配置 Hibernate 中的哪些实体对象要纳入到二级缓存的管理中。明白了二级缓存原理和有了这个思路后，很容易配置起 Hibernate 的二级缓存。扩展知识：一个 SessionFactory 可以关联一个二级缓存，也即一个二级缓存只能负责缓存一个数据库中的数据，当使用 Hibernate 的二级缓存后，注意不要有其他的应用或 SessionFactory来更改当前数据库中的数据，这样缓存的数据就会与数据库中的实际数据不一致。
13. 同步和异步有何异同，在什么情况下分别使用他们？举例说明。
如果数据将在线程间共享，例如正在写的数据以后可能被另一个线程读到，或者正在读的数据可能已经被另一个线程写过了，那么这些数据就是共享数据，必须进行同步存取。
当应用程序在对象上调用了一个需要花费很长时间来执行的方法，并且不希望让程序等待方法的返回时，就应该使用异步编程，在很多情况下采用异步途径往往更有效率。
14. HTTP get和post的区别
    1. GET一般用于获取/查询资源信息，而POST一般用于更新资源信息。
    2. GET请求的数据会附在URL之后（就是把数据放置在HTTP协议头中），以?分割URL和传输数据，参数之间以&相连；POST把提交的数据则放置在是HTTP包的包体中
    3. GET是通过URL提交数据，那么GET可提交的数据量就跟URL的长度有直接关系了。而实际上，URL不存在参数上限的问题，HTTP协议规范没有对URL长度进行限制。这个限制是特定的浏览器及服务器对它的限制。IE对URL长度的限制是2083字节(2K+35)。对于其他浏览器，如Netscape、FireFox等，理论上没有长度限制，其限制取决于操作系统的支持。理论上讲，POST是没有大小限制的，HTTP协议规范也没有进行大小限制，说“POST数据量存在80K/100K的大小限制”是不准确的，POST数据是没有限制的，起限制作用的是服务器的处理程序的处理能力。
15. Tomcat的默认端口是多少？如何修改？
默认端口是8080，在tomcat目录下的conf/server.xml文件中修改端口。
16. 如何使用tomcat部署一个web工程？
    三种方式
    1. 直接把项目复制到Tomcat安装目录的webapps目录
    2. 更改$CATALINA_HOME\conf\server.xml文件，在<host>标签内添加<Context>标签，内容如下：
    <Context docBase="F:/PetWeb" reloadable="false" path="/Pet"/>
    其中reloadable="false"表示当应用程序中的内容发生更改之后服务器不会自动加载，这个属性在开发阶段通常都设为true，方便开发，在发布阶段应该设置为false，提高应用程序的访问速度。docBase为路径，可以使用绝对路径，也可以使用相对路径，相对路径相对于webapps。path属性的值是访问时的根地址。访问地址如下：http://localhost:8080/Pet/ 
    3. 在$CATALINA_HOME\conf\Catalina\localhost中添加一个xml文件，如Pet.xml，内容如下：
    <Context docBase="F:/PetWeb" reloadable="false" />大家可能发现和第二种方式差不多，但是缺少了path属性，这种方式服务器会使用.xml的名字作为path属性的值。访问地址如下：http://localhost:8080/Pet/ 
17. 请简单描述一下当我们访问淘宝网时，从输入url到浏览器显示页面之间发生的操作。
    1. DNS把该域名解析成对应的IP地址。
    2. 根据该IP地址在互联网上找到对应的服务器，并向这个服务器发起一个get请求，由这个服务器决定返回默认的数据资源给访问的用户。   
    【加分点】
    1. 服务器可能有多台，如何指定哪台服务器来处理请求，需要负载均衡来分配用户请求。
    2. 请求的数据是存储在分布式缓存里面还是一个静态文件中，还是在数据库中，如何处理。
    3. 当数据返回浏览器时，浏览器解析数据发现还有一些静态资源（CSS、JS或者图片）时又会发起另外的HTTP请求，而这些请求有可能会在CDN服务器上，那么CDN服务器会处理这些请求。 
18. 浏览器的F5和Ctrl + F5有什么区别？   
F5的作用和直接在URI输入栏中输入然后回车是不一样的，F5会让浏览器无论如何都发一个HTTP Request给Server，即使先前的Response中有Expires Header。所以，当在当前网页中按F5的时候，浏览器会发送一个HTTP Request给Server，但是包含这样的Headers:If-Modified-Since: Fri 30 Nov 2007 00:00:00 GMT。服务器判断还没有过期，就直接返回304not modified，在firebug里看就是这些304的请求都为灰色。因为直接返回304这样的信息，而不是图片等内容。
Ctrl + F5这个就要慢了，应为所有的请求都是重新发送，重新从server读取内容，一点cache都没有读。为了防止在server的cache里读取，在ctrl+f5刷新时，request的header里还加了特殊字段
19. BS 与 CS 的联系与区别
C/S 是 Client/Server 的缩写。服务器通常采用高性能的 PC、工作站或小型机，并采用大型数据库系统，如 Oracle、Sybase、InFORMix 或 SQL Server。客户端需要安装专用的客户端软件。
B/Ｓ是 Brower/Server 的缩写，客户机上只要安装一个浏览器，如 Netscape Navigator 或 Internet Explorer，服务器安装 Oracle、Sybase、InFORMix 或 SQL Server等数据库。在这种结构下，用户界面完全通过 WWW 浏览器实现，一部分事务逻辑在前端实现，但是主要事务逻辑在服务器端实现。浏览器通过Ｗeb Server 同数据库进行数据交互。
C/S 与 B/S 区别：
1)	硬件环境不同
C/S 一般建立在专用的网络上，小范围里的网络环境,局域网之间再通过专门服务器提供连接和数据交换服务。    
B/S 建立在广域网之上的，不必是专门的网络硬件环境，例如电话上网，租用设备，信息自己管理。有比 C/S 更强的适应范围，一般只要有操作系统和浏览器就行。
2)	对安全要求不同
C/S 一般面向相对固定的用户群，对信息安全的控制能力很强。一般高度机密的信息系统采用 C/S 结构适宜。可以通过 B/S 发布部分可公开信息。
B/S 建立在广域网之上。对安全的控制能力相对弱，可能面向不可知的用户。
3)	对程序架构不同
C/S 程序可以更加注重流程，可以对权限多层次校验，对系统运行速度可以较少考虑。
B/S 对安全以及访问速度的多重的考虑，建立在需要更加优化的基础之上。比 C/S 有更高的要求 B/S 结构的程序架构是发展的趋势。
4)	软件重用不同
C/S 程序可以不可避免的整体性考虑，构件的重用性不如在 B/S 要求下的构件的重用性好。
B/S 的多重结构要求构件相对独立，能够较好的重用。就入买来的餐桌可以再利用，而不是做在墙上的石头桌子。
5)	系统维护不同
C/S 程序由于整体性，必须整体考察，处理出现的问题以及系统升级。升级难，可能是再做一个全新的系统
B/S 构件组成，方便构件更换，实现系统的无缝升级。系统维护开销减到最小，用户从网上自己下载安装就可以实现升级。
6)	处理问题不同
C/S 程序可以处理用户面固定，并且在相同区域，安全要求高，与操作系统相关。
B/S 建立在广域网上，面向不同的用户群，分散地域，这是 C/S 无法作到的。与操作系统平台关系最小。
7)	用户接口不同
C/S 多是建立在Window 平台上，表现方法有限，对程序员普遍要求较高。
B/S 建立在浏览器上，有更加丰富和生动的表现方式与用户交流，并且大部分难度减低，降低开发成本。
8)	信息流不同
C/S 程序一般是典型的中央集权的机械式处理，交互性相对低。
B/S 信息流向可变化,，信息、流向的变化，更像交易中心。
 
JavaScript篇
——————————————————基础——————————————————
1．JS主要数据类型？怎么判断类型？
基本数据类型：String，boolean，Number，Undefined，Null
引用数据类型：Object(Array，Date，RegExp，Function)
使用typeof，instanceof判断类型。
2．已知ID的Input输入框，希望获取这个输入框的输入值，怎么做？(不使用第三方框架)
document.getElementById(‘ID’).value

—————————————————基础+高级—————————————————
3．JS中 “==”和“===”的区别是什么？
1)	对于string，number等基础类型，==和===是有区别的
	不同类型间比较：
对于==，比较“转化成同一类型后的值”（隐式类型转换）看“值”是否相等；
对于===，如果类型不同，其结果就是不等。
	同类型比较：
直接进行“值”比较，两者结果一样。
2)	对于Array，Object等高级类型，==和===是没有区别的
进行“指针地址”比较。
3)	基础类型与高级类型，==和===是有区别的
对于==，将高级转化为基础类型，进行“值”比较；
对于===，因为类型不同，===结果为false。

基础：答案能体现==表示等于、===表示严格等于。
高级：能分不同的类型分开阐述。
4．JS的隐式类型转换？哪些会自动转换为false，哪些会自动转化为true？隐式类型转换有哪些好处和弊端？
隐式转换为布尔：当JavaScript 需要一个布尔值时（例如：if 语句），任何值都可以被使用。 最终这些值将被转换为 true 或 false。
下面的值被转换为 false：
undefined, null
Boolean: false
Number: -0, +0, NaN
String: “ ”
所有其他值都认为是 true。

【举例考察】
var x = '5';  // 错误的假设：x 是一个数字 	x + 1是什么？
'51'

基础：理解JS隐式类型转换，能答出参考答案内容。
高级：能意识到隐式类型转换的弊端，并在代码中尽量不使用这个特性。
5．0.1+0.2 = ？ 0.58 * 100 = ？为什么？有没有遇到过这类问题，怎么解决的？
0.1+0.2=0.30000000000000004
0.58*100=57.99999999999999
原因：大多数语言在处理浮点数的时候都会遇到精度问题，但是在JS里似乎特别严重，加减乘除操作均会遇到精度问题。我们输入的是两个十进制数，但是JS会转化成二进制进行运算，然后再转化回来，在转化的过程中可能会有损失，但一般的损失往往在乘除运算中比较多，而JS在简单的加减法里也会出现这类问题，这个误差虽然非常小，但是却是不该出现的。

基础：能答出0.1+0.2≠0.3
高级：能答出结果，并解释原因，在项目中亲自解决过这类问题且思路正确。
6．JS怎么创建一个对象？
1)	对象字面量：用“{}”方式声明对象；
2)	Object实例：用new关键字创建一个Object实例，并通过动态添加属性或方法的方式创建一个对象；
3)	构造函数模式：通过function声明一个构造函数，然后通过new 构造函数创建一个对象的实例；
4)	原型模式：类型构造函数模式，将属性和方法定义在prototype上；
5)	工厂模式：定义一个工厂函数，用Object实例方式创建对象，并return该对象。

基础：掌握前三种创建对象的方法。
高级：能答出后两种或者其他方式。
7．HTML5中有哪些本地存储（本地缓存）？他们的生命周期是什么？
1)	localStorage 本地存储，除非代码清除或者用户清除浏览器缓存，否则一直存在；
2)	sessionStorage 针对一个session存储，当用户关闭浏览器或session失效时被清除；
3)	cookie 在H5之前，都是由cookie完成，但是cookie每次请求后台都会全部带上，有大小的限制，且容易遭到XSS攻击。

基础：了解cookie，会使用cookie常见的方法。
高级：能答出localStorage和sessionStorage，理解三者之间的区别，生命周期。

8．什么是Ajax，它有什么优缺点？
Ajax是异步JavaScript和XML，用于在Web页面中实现异步数据交互。
优点：可以使得页面不重载全部内容的情况下加载局部内容，降低数据传输量。
　    避免用户不断刷新或者跳转页面，提高用户体验。
缺点：SEO不友好。
　    要实现ajax下的前后退功能成本较大。
　    可能造成请求数的增加。
　    跨域问题限制。

基础：了解Ajax的概念，至少使用过一种Ajax框架：例如jQuery ajax。
高级：理解Ajax原理以及优缺点，理解原生Ajax的实现以及IE内核和WebKit内核实现的区别。
9．说出几个JS数组的方法？JS怎么删除数组元素？
JS数组常用的方法有：indexOf  join  pop  push  concat  forEach 等等。
JS的数组并没有提供删除元素的方法，如果用delete运算符，通过对象删除属性的方式去删除（误区）会有问题：数组的长度并不会改变，被删除的元素会变成undefined。具体删除方法：只能通过循环将被删除的元素后面的元素前移，并将数组长度减1。

基础：能说出几个数组常用的方法。
高级：理解数组删除原理。
10．原生JS的window.onload与Jquery的$(document).ready(function(){})有什么不同？如何用原生JS实现Jquery的ready方法？
原生JS的window.onload()方法是必须等到页面内包括图片的所有元素加载完毕后才能执行，jQuery的$(document).ready()是DOM结构绘制完毕后就执行，不必等到加载完毕。
考虑通过原生JS的事件监听来实现Jq的ready方法。

基础：知道window.onload与Jquery的ready的区别。
高级：用原生JS实现jQuery的ready方法思路正确。

——————————————————高级——————————————————
11．Object和Function的区别是什么？
Function就是Object，Object就是Function。
	alert(Function instanceof Object); // true 
	alert(Object instanceof Function); // true
JavaScript 中，万物皆对象！但对象也是有区别的。分为普通对象和函数对象，Object ，Function 是JS自带的函数对象；凡是通过 new Function() 创建的对象都是函数对象，其他的都是普通对象。

12．JS原型链
在JavaScript 中，每当定义一个对象（函数）时候，对象中都会包含一些预定义的属性。其中函数对象的一个属性就是原型对象 prototype。普通对象没有prototype,但有__proto__属性。原型对象其实就是普通对象（Function.prototype除外,它是函数对象，但它很特殊，他没有prototype属性，前面说到函数对象都有prototype属性）。
JS在创建对象（不论是普通对象还是函数对象）的时候，都有一个叫做__proto__的内置属性，用于指向创建它的函数对象的原型对象prototype，直到Object.prototype对象也有__proto__属性，但它比较特殊，为null，我们把这个由__proto__串起来的直到Object.prototype.__proto__为null的链叫做原型链。
13．JS闭包
闭包是Javascript语言的一个难点，也是它的特色，很多高级应用都要依靠闭包实现。	要理解闭包，首先必须理解Javascript特殊的变量作用域。变量的作用域无非就是两种：全局变量和局部变量。Javascript语言的特殊之处，就在于函数内部可以直接读取全局变量。另一方面，在函数外部自然无法读取函数内的局部变量。出于种种原因，我们有时候需要得到函数内的局部变量，Javascript语言特有的“链式作用域”结构使得子对象会一级一级地向上寻找所有父对象的变量。所以，父对象的所有变量，对子对象都是可见的，反之则不成立。
通俗理解：“闭包就是能够读取其他函数内部变量的函数”，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。
闭包可以用在许多地方。它的最大用处有两个，一个是前面提到的可以读取函数内部的变量；另一个就是让这些变量的值始终保持在内存中（因为在函数外部对函数内部的局部变量进行操作，会导致函数内部变量始终在内存中，不会在调用结束后，被垃圾回收机制回收 ）。
使用闭包应该注意：1）由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。2）闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。
注：闭包的概念比较晦涩难懂，主要通过对答案的深度、术语的表述以及JS内部执行机制的理解来考察JS的整体水平。
14．想实现一个对页面某个节点的拖曳？如何做？（使用原生JS）
回答出概念即可，下面是几个要点（注：需要注意浏览器边界的情况）：
1)	给需要拖拽的节点绑定mousedown, mousemove, mouseup事件；
2)	mousedown事件触发后，开始拖拽；
3)	mousemove时，需要通过event.clientX和clientY获取拖拽位置，并实时更新位置；
4)	mouseup时，拖拽结束。
 
CSS3篇
——————————————————基础——————————————————
1．“.a.b” 和 “.a  .b”的区别
前者选中同时有class a和class b的元素；
后者构成后代选择器。
2．请解释CSS的盒子模型
从内到外：content、padding、border、margin。

—————————————————基础+高级—————————————————
3．请说出几种常用的CSS选择器
基础：能答出id、class、element attribute、父子、祖先后代等基本选择器；
高级：能答出几种伪类、动态伪类选择器，如：:hover :active :enable :last-of-child，并能使用各种组合写出复杂的选择器。
4．position定位
	absolute
生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。
元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
	fixed
生成绝对定位的元素，相对于浏览器窗口进行定位。
元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
	relative
生成相对定位的元素，相对于其正常位置进行定位。
因此，"left:20" 会向元素的 LEFT 位置添加 20 像素。
	Static
默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。
	inherit
规定应该从父元素继承 position 属性的值。

基础：了解绝对定位和相对定位，并能使用他们配合div布局；
高级：理解position定位的原理，熟练使用他们的特性布局。
5．CSS层叠
层叠指的是样式的优先级，当产生冲突时以优先级高的为准。
1)	开发者样式>读者样式>浏览器样式（除非使用!important标记 ）
2)	id选择符>（伪）类选择符>元素选择符
3)	权重相同时取后面定义的样式
CSS样式在针对同一元素配置同一属性时，依据层叠规则（权重）来处理冲突，选择应用权重高的CSS选择器所指定的属性，一般也被描述为权重高的覆盖权重低的，因此也称作层叠。

基础：理解CSS层叠概念；
高级：熟练掌握层叠优先级，当出现冲突时以什么为准。
 
HTML5篇
——————————————————基础——————————————————
1．请说出HTML5相对HTML4的一些新特性
 Canvas， audio， video， input type=“email”，number， datalist， localStorage...
2．HTML5新的Doctype和Charset是什么？
<!DOCTYPE html>
<meta charset="utf-8">

—————————————————基础+高级—————————————————
3．如何显示/隐藏一个DOM元素？ 
1)	更改元素的css style，设为display: none；
2)	将visibility设为hidden；
3)	透明度设为0；
4)	长、宽设为0；
5)	$.hide()...
注意：display:none的方式会使该DOM元素所占的位置被后面的元素覆盖；visibility:hidden会将位置占住，只是该区域不可见。

基础：能说出几种方法；
高级：能区分display:none和visibility:hidden的区别。
4． 块级元素和内联元素的区别是什么？块级元素有哪些，内联元素有哪些？内联元素设margin-left，margin-top有没有效果？内联元素怎么转化为块级元素？（附加：表单元素和表格元素）
块级元素：h1-6、p、div、ol、ul、table...
内联元素：a、select、strong、img、input、span...

行内元素与块级函数的三个区别：
1)	行内元素与块级元素直观上的区别：行内元素会在一条直线上排列，都是同一行的，水平方向排列；块级元素各占据一行，垂直方向排列。块级元素从新行开始结束接着一个断行。
2)	块级元素可以包含行内元素和块级元素。行内元素不能包含块级元素。
3)	行内元素与块级元素属性的不同，主要是盒模型属性上：行内元素设置width无效，height无效(可以设置line-height)，margin上下无效，padding上下无效。

行内元素转换为块级元素：display:block (字面意思表现形式设为块级)

基础：能区分行内元素和块级元素、并分别说出几种；
高级：能理解二者之间的三个区别，特别是第三个和盒模型有关的特性。

——————————————————高级——————————————————
5．让IE浏览器使用Chrome内核渲染怎么实现？
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
 
前端综合篇
1．HTTP协议？Header、body有哪些参数？
HTTP（超文本传输协议）是一个基于请求与响应模式的、无状态的、应用层的协议，常基于TCP的连接方式，HTTP1.1版本中给出一种持续连接的机制，绝大多数的Web开发，都是构建在HTTP协议之上的Web应用。
HTTP协议的主要特点可概括如下：
1)	支持客户/服务器模式。
2)	简单快速：客户向服务器请求服务时，只需传送请求方法和路径。请求方法常用的有GET、HEAD、POST。每种方法规定了客户与服务器联系的类型不同。由于HTTP协议简单，使得HTTP服务器的程序规模小，因而通信速度很快。
3)	灵活：HTTP允许传输任意类型的数据对象。正在传输的类型由Content-Type加以标记。
4)	无连接：无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间。
5)	无状态：HTTP协议是无状态协议。无状态是指协议对于事务处理没有记忆能力。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快。

POST http://10.170.3.50:8080/ntraffic/user/login.do HTTP/1.1
Host: 10.170.3.50:8080
Connection: keep-alive
Content-Length: 36
Accept: application/json, text/plain, */*
 Origin: http://10.170.3.50:8080
 User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/40.0.2214.115 Safari/537.36
 Content-Type: application/json;charset=UTF-8
 Referer: http://10.170.3.50:8080/ntraffic/ntraffic/app/index.html
 Accept-Encoding: gzip, deflate
 Accept-Language: zh-CN,zh;q=0.8
 Cookie: JSESSIONID=5AF249CC9E2DCD6F685980FF2E361A94
2．平时上哪些技术网站？知道哪些前端大牛博客？
csdn oschina 慕课网 W3CSchool 菜鸟 慕课 iteye 各大框架官网...
大漠、阮一峰、老赵、大猫 ...
3．用过的前端或JS框架有哪些？NodeJS、RequireJS、AngularJS、Backbone、BootStrap、Grunt、yeoman有没有了解过？
使用过Require Angular Backbone Bootstrap 一种或几种为佳。

4．有没有关注过GitHub上面的开源项目？有没有在git上共享过项目？你的git账号是什么？

5．浏览器兼容问题？
问题一：不同浏览器的标签默认的padding和margin不同
解决方案：CSS里    *{margin:0;padding:0;}

问题二：块属性标签float后，又有横行的margin情况下，在IE6显示margin比设置的大，常见症状是IE6中后面的一块被顶到下一行。
解决方案：在float的标签样式控制中加入 display:inline;将其转化为行内属性

问题三：图片默认有间距
问题症状：几个img标签放在一起的时候，有些浏览器会有默认的间距，加了问题一中提到的通配符也不起作用。
解决方案：使用float属性为img布局。
......
6．都使用和了解过哪些编辑器或IDE？
Notepad++  editplus  sublime  Aptana  Webstorm  Intellij idea  eclipse brackets ...
7．说说你平时注意的前端代码规范？
1)	在属性上，使用双引号，不要使用单引号；
2)	嵌套的节点应该缩进；
3)	不要忽略可选的关闭标签；
4)	HTML 属性应该按照特定的顺序出现以保证易读性；
5)	页面中尽量避免使用style属性；
6)	禁止在html中使用<style>标签定义样式；
7)	禁止使用 @import；
8)	完全避免 == != 的使用， 用严格比较条件 === !==。
8．html5的现状和发展前景？Html5的优点和缺点？
HTML5是什么？狭义的HTML5：HTML5草案的前身名为 Web Applications 1.0，于2004年被WHATWG提出，于2007年被W3C接纳，并成立了新的 HTML 工作团队。2013年5月6日， HTML 5.1正式草案公布。该规范定义了第五次重大版本，第一次要修订万维网的核心语言：超文本标记语言（HTML）。在这个版本中，新功能不断推出，以帮助Web应用程序的作者，努力提高新元素互操作性。广义的HTML5包括HTML, CSS和JavaScript在内的一套技术组合，其目标是减少浏览器对于插件的依赖，提供丰富的RIA（富客户端）应用。所以CSS3， SVG， WebGL， Touch事件，动画支持等都属于HTML5技术范围。

互联网趋势：
随着网络架构的完善，宽带提升，网速满足实时交互需求时，计算机结构也将发生变化，光驱消失，硬盘消失，内存增大，GPU愈加重要，现在B/S结构的应用越来越多，而HTML5旨在富互联网应用，能够改善B/S结构应用的用户体验，是互联网应用的趋势之一

HTML5的缺点：
- 功能简单且分散
HTML5是一种技术集合，包括各种标签及其相关API，HTML，CSS，SVG，JavaScript等，没有统一的开发工具，一个完整的HTML5应用涉及到多种技术，导致开发难度大，对于企业应用，HTML5的功能有限，需要借助第三方类库
- 浏览器支持不一
一直以来HTML5都以跨平台著称，但实际上要实现这一目标工作量巨大，HTML5缺少一个浏览器的标杆（Webkit有希望成为），尤其目前在IE6/7/8占有率居高不下的情况下，希望用HTML5跨全平台基本是不可能的。
9．有没有做过前端优化？
参考原则：
尽量减少HTTP请求；使用内容发布网络（CDN的使用）；添加Expires头(缓存)；压缩组件（使用Gzip方式）；将CSS样式表放在顶部；将javascript脚本放在底部；避免使用CSS表达式；使用外部javascript和CSS；减少DNS查询；精简javascript；避免重定向；删除重复脚本
参考思路：产品发布时，js的压缩，即函数名替换、整个文件压缩成一行。css开发的时候，注释写清楚，先有个base.css，然后根据不同页面需要再加css，发布的时候将css中的一个定义写成一行，目的是压缩文件大小，最终发布的时候甚至可以将css，js分别压缩成一个文件，甚至css、js通过技巧压缩到一个里边（亮点）以减少用户访问web产品的http连接数；字体图标，使用css截取图片...
10．AMD和CMD思想？
JavaSript模块化
模块化是指在解决某一个复杂问题或者一系列的杂糅问题时，依照一种分类的思维把问题进行系统性的分解以之处理。模块化是一种处理复杂系统分解为代码结构更合理，可维护性更高的可管理的模块的方式。可以想象一个巨大的系统代码，被整合优化分割成逻辑性很强的模块时，对于软件是一种何等意义的存在。对于软件行业来说：解耦软件系统的复杂性，使得不管多么大的系统，也可以将管理，开发，维护变得“有理可循”。
AMD( Asynchronous Module Definition)，用白话文讲就是 异步模块定义，对于 JSer 来说，异步是再也熟悉不过的词了，所有的模块将被异步加载，模块加载不影响后面语句运行。所有依赖某些模块的语句均放置在回调函数中。
AMD 与 CMD 区别：
AMD 是 RequireJS 在推广过程中对模块定义的规范化产出；CMD 是 SeaJS 在推广过程中对模块定义的规范化产出。
对于依赖的模块，AMD 是提前执行，CMD 是延迟执行。CMD 推崇 as lazy as possible.CMD 推崇依赖就近，AMD 推崇依赖前置。
