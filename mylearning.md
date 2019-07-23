# 学习总结

## 0x00 基础知识

### <1> Linux

#### 1. Linux 参考文档
* [Tutoial - run-cn](https://www.runoob.com/linux/linux-tutorial.html)
* [Tutoial - w3c-cn](https://www.w3cschool.cn/linux/?)
* [Unix Tutoial - eng](https://www.tutorialspoint.com/unix/)
* RHCE [Study Guide](https://www.computernetworkingnotes.com/rhce-study-guide/)

#### 2. 基础概念与常用命令


### <2> Python

[官方文档](https://docs.python.org/zh-cn/3/library/index.html)

#### 1. filter
filter() 函数用于过滤序列，过滤掉不符合条件的元素，返回由符合条件元素组成的新列表。该接收两个参数，第一个为函数，第二个为序列，序列的每个元素作为参数传递给函数进行判，然后返回 True 或 False，最后将返回 True 的元素放到新列表
#### 2. 异常处理
try..except..else没有捕获到异常，执行else语句
try..except..finally不管是否捕获到异常，都执行finally语句
#### 3. zip
​	zip()函数在运算时，会以一个或多个序列（可迭代对象）做为参数，返回一个元组的列表。同时将这些序列中并排的元素配对。

zip()参数可以接受任何类型的序列，同时也可以有两个以上的参数;当传入参数的长度不同时，zip能自动以最短序列长度为准进行截取，获得元组。
用于同时迭代2个列表：
~~~ python3
nfc = ["ABCD","DCBA"]
afc = ["1234","4321"]
for a,b in zip(nfc, afc):
    print(a,b)
~~~

#### 4. copy和deepcopy区别
(1) 复制不可变数据类型，不管copy还是deepcopy,都是同一个地址当浅复制的值是不可变对象（数值，字符串，元组）时和=“赋值”的情况一样，对象的id值与浅复制原来的值相同。

(2) 复制的值是可变对象（列表和字典）

浅拷贝copy有两种情况：
* 第一种情况：复制的 对象中无 复杂 子对象，原来值的改变并不会影响浅复制的值，同时浅复制的值改变也并不会影响原来的值。原来值的id值与浅复制原来的值不同。
* 第二种情况：复制的对象中有 复杂 子对象 （例如列表中的一个子元素是一个列表）， 改变原来的值 中的复杂子对象的值 ，会影响浅复制的值。
深拷贝deepcopy：完全复制独立，包括内层列表和字典

#### 5. 迭代器和生成器的区别
(1)迭代器是一个抽象的概念，任何对象，如果它的类有next方法和iter方法返回自身。对于string、list、dict、tuple等这类容器对象，使用for循环遍历是很方便的。在后台for语句对容器对象调用iter()函数，iter()是Python的内置函数。iter()会返回一个定义了next()方法的迭代器对象，它在容器中逐个访问容器内元素，next()也是python的内置函数。在没有后续元素时，next()会抛出一个StopIterration的异常。

(2)生成器（Generator）是创建迭代器的简单而强大的工具。它们写起来就像是正规的函数，只是在返回数据的时候需要使用yield语句。每次next()被调用时，生成器会返回它脱离的位置（它记忆语句最后一次执行的位置和所有的数据值）

(3)区别：生成器能做到迭代器能做的所有事，而且因为自动创建了__iter__()和next()方法，生成器显得特别简洁，而且生成器也是高效的，使用生成器表达式取代列表解析可以同时节省内存。除了创建和保持程序状态的自动生成，当发生器终结时，还会自动跑出StopIterration异常。举例：python3 range

#### 6. 闭包

(1) 在一个外函数中定义了一个内函数，内函数里运用了外函数的临时变量，并且外函数的返回值是内函数的引用。这样就构成了一个闭包。

(2) 用途：装饰器、面向对象、单利模式

#### 7. 装饰器

(1)装饰器本质其实就是一个函数，可以让其它函数不改动源代码的情况下增加其他新功能

(2)使用场景: 引入日志、函数执行时间统计、执行函数前预备处理、执行函数后的清理功能、权限校验等场景、缓存

#### 8. 推导生成

* 列表生成

```
another_list = [ x + 1 for x in some_list ]
```

 * 集合推导(Set comprehensions)

```
even_set = { x for x in some_list if x % 2 == 0 }
```

 * 字典推导(Dictionary comprehensions)

```
d_dict = { x: x % 2 == 0 for x in range(1, 11) }
```

#### 9. 迭代
* enumerate 带索引的列表迭代
~~~ python
teams = ["A", "B", "C", "D"]
for index, team in enumerate(teams):
    print(index, team)
~~~

* itertools迭代工具
~~~python
from itertools import combinations
# 排列组合
teams = ["A", "B", "C", "D"]
for game in combinations(teams, 2):
    print(game) # tuple
~~~

#### X.提高python运行效率的方法
* 使用生成器，因为可以节约大量内存
* 循环代码优化，避免过多重复代码的执行
* 核心模块用Cython PyPy等，提高效率
* 多进程、多线程、协程
* 多个if elif条件判断，可以把最有可能先发生的条件放到前面写，这样可以减少程序判断的次数，提高效率
* map_reduce

#### X-1. Global Interpreter Lock（全局解释器锁）
Python代码的执行由python虚拟机（也叫解释器主循环，CPython版本）来控制，Python在设计之初就考虑到要在解释器的主循环中，同时只有一个线程在执行，即任意时刻，只有一个线程在解释器中运行。对Python虚拟机的访问由全局解释器锁（GIL）来控制，正是这个锁能保证同一时刻只有一个线程在运行。

** 在多线程环境中，Python虚拟机按以下方式执行：

* 设置GIL
* 切换到一个线程去运行
* 运行：
    * 指定数量的字节码指令
    * 线程主动让出控制（ 可以调用time.sleep(0) 
* 把线程设置为睡眠状态
* 解锁GIL
* 再次重复以上所有步骤

再调用外部代码（如C/C++扩展函数）的时候，GIL讲会被锁定，直到这个函数结束为止（由于在这期间没有Python的字节码被运行，所以不会做线程切换）。

#### X-2. 线程
threading --- 基于线程的并行，当多个线程同时要修改同一份数据时，就会出现一些错误（python2.x出现错误，python3.x无），所以每个线程在要修改公共数据时，为了避免自己在还没改完的时候别人也来修改此数据，可以加上线程锁。来确保每次修改数据时只有一个线程在操作。

#### X-3. 进程
multiprocessing模块，每个进程都拥有自己的内存空间，因此不同进程间内存是不共享的，要想实现两个进程间的数据交换，有几种方法，Queue（队列），Pipe（管道，不常用），Manager（实现了进程间真正的数据共享）。
进程池内部维护一个进程序列，当使用时，则去进程池中获取一个进程，如果进程池序列中没有可供使用的进程，那么程序就会等待，直到进程池中有可用进程为止。
进程池中有两个方法：apply（同步）、apply_async（异步）

#### X-4. 协程
协程，又称微线程，是一种用户态的轻量级线程。协程能保留上一次调用时的状态，每次过程重入时，就相当于进入上一次调用的状态，换种说法：进入上一次离开时所处逻辑流的位置，当程序中存在大量不需要CPU的操作时（IO），适用于协程。
协程有极高的执行效率，因为子程序切换不是线程切换，而是由程序自身控制，因此，没有线程切换的开销。
不需要多线程的锁机制，因为只有一个线程，也不存在同时写变量冲突，在协程中控制共享资源不加锁，只需要判断状态就好了，所以执行效率比多线程高很多。

#### X-5. map reduce

* map()是 Python 内置的高阶函数，它接收一个函数 f 和一个 list，并通过把函数 f 依次作用在 list 的每个元素上，得到一个新的 list 并返回。（python3中返回的是迭代器）
~~~python3
import time
start = time.time()

def work(x):
    time.sleep(0.001)
    return x**6

data = [i for i in range(1000)]
results = map(work, data)
res = list(results)

print(len(res))
print(time.time()-start)
~~~
* reduce()函数接收的参数和 map()类似，一个函数 f，一个list，但行为和 map()不同，reduce()传入的函数 f 必须接收两个参数，reduce()对list的每个元素反复调用函数f，并返回最终结果值。
* 多CPU计算密集型：
~~~python3
from concurrent.futures import ProcessPoolExecutor
import time

start = time.time()

def work(x):
    time.sleep(0.001)
    return x**6

data = [i for i in range(1000)]

with ProcessPoolExecutor() as pool:
    results = pool.map(work, data)  # map

res = list(results) # reduce
print(len(res))
print(time.time()-start)
~~~


### <3> C++ TODO
### <4> 数据结构 TODO
### <5> 数据库 SQL

在线参考 [W3School](http://www.w3school.com.cn/sql/sql_syntax.asp)

要求 | query
-|:--
查询选修了CS3121014课程的学生学号和成绩 | select Sno,Grade from sc where Cno="CS3121014";
查询选修了CS3121014课程的学生学号和姓名 | select Sno,sname from student where Sno in (select Sno from sc where Cno="CS3121014");
查询选修数据库系统课程的学生学号、姓名和成绩，查询结果按分数降序排列 | select student.Sno,student.Sname from sc inner join student on sc.Sno == student.Sno where Cno == "CS3121014"  order by sc.grade DESC; ; 
查询选修了CS3121014或CS3221018课程的学生学号 | select distinct Sno from sc where Cno == "CS3221018" or Cno == "CS3121014";
查询选修了CS3121014和CS3221018课程的学生学号 | select a.Sno from sc as a inner join sc as b on a.Sno == b.Sno where a.Cno =="CS3121014" and b.Cno=="CS3221018";
查询CS3121014的先修课的课程号 | select pno from pcourse where cno=="CS3121014";
查询选修了全部课程的学生学号 | select Sno from student where Sno in (select Sno from sc group by Sno having count(\*)=(select count(\*) from course));
查询选修了学号为“03051066”的学生所选全部课程的学生学号和姓名| select student.Sno ,student.Sname from student where student.Sno not in (select sc.Sno from sc where sc.Cno not in (Select sc.Cno from sc where sc.Sno=="03051066"));

* **MySQL常用查询语法 [简书](https://www.jianshu.com/p/ad48ad439b16)**
* **MySQL常用查询案例 [简书](https://www.jianshu.com/p/adc96e2b4b69)**


## 0x01 专业知识

### <0> 计算机网络

#### 1. 浏览器输入url点击回车后发生的一系列事情

[参考原文](https://segmentfault.com/a/1190000012092552)

* 键盘闭合，产生电流，操作系统产生中断，发往应用程序
* 浏览器解析URL：通过解析了解协议和请求的内容，判断输入是否合法： 判断输入的是url还是域名还是关键字，判断输入是否合法
* DNS查询：DNS查询本地cache或者向DNS服务器发送查询请求，请求目标主机的ip地址
* ARP 过程：首先查询 ARP 缓存，如果缓存命中，我们返回结果：目标 IP = MAC，查看路由表，看看目标 IP 地址是不是在本地路由表中的某个子网内。是的话，使用跟那个子网相连的接口，否则使用与默认网关相连的接口。查询选择的网络接口的 MAC 地址，发送一个二层（OSI模型中的数据链路层）ARP请求
* 使用套接字建立连接，即tcp/udp连接，tcp三次握手
* http协议：发送http包，进行http请求，http回答
* 浏览器解析，渲染：得到请求的资源后。浏览器进行解析和渲染
* 连接拆除，tcp/udp连接结束，tcp四次握手

#### 2. TCP三次握手

客户端选择一个初始序列号(ISN)，将设置了 SYN 位的封包发送给服务器端，表明自己要建立连接并设置了初始序列号

**服务器端接收到 SYN 包，如果它可以建立连接**

* 服务器端选择它自己的初始序列号
* 服务器端设置 SYN 位，表明自己选择了一个初始序列号
* 服务器端把 (客户端ISN + 1) 复制到 ACK 域，并且设置 ACK 位，表明自己接收到了客户端的第一个封包

**客户端通过发送下面一个封包来确认这次连接**

* 自己的序列号+1
* 接收端 ACK+1
* 设置 ACK 位

数据通过下面的方式传输：

* 当一方发送了N个 Bytes 的数据之后，将自己的 SEQ 序列号也增加N
* 另一方确认接收到这个数据包（或者一系列数据包）之后，它发送一个 ACK 包，ACK 的值设置为接收到的数据包的最后一个序列号

**关闭连接时**

* 要关闭连接的一方发送一个 FIN 包
* 另一方确认这个 FIN 包，并且发送自己的 FIN 包
* 要关闭的一方使用 ACK 包来确认接收到了 FIN

#### 3. TLS握手

* 客户端发送一个`ClientHello`消息到服务器端，消息中同时包含了它的 Transport Layer Security (TLS) 版本，可用的加密算法和压缩算法。
* 服务器端向客户端返回一个`ServerHello`消息，消息中包含了服务器端的TLS版本，服务器所选择的加密和压缩算法，以及数字证书认证机构（Certificate Authority，缩写CA）签发的服务器公开证书，证书中包含了公钥。客户端会使用这个公钥加密接下来的握手过程，直到协商生成一个新的对称密钥。
* 客户端根据自己的信任CA列表，验证服务器端的证书是否可信。如果认为可信，客户端会生成一串伪随机数，使用服务器的公钥加密它。这串随机数会被用于生成新的对称密钥
* 服务器端使用自己的私钥解密上面提到的随机数，然后使用这串随机数生成自己的对称主密钥
* 客户端发送一个`Finished`消息给服务器端，使用对称密钥加密这次通讯的一个散列值
* 服务器端生成自己的 hash 值，然后解密客户端发送来的信息，检查这两个值是否对应。如果对应，就向客户端发送一个`Finished`消息，也使用协商好的对称密钥加密
* 从现在开始，接下来整个 TLS 会话都使用对称秘钥进行加密，传输应用层（HTTP）内容。

#### 4. [HTTP](https://juejin.im/post/5a8102e0f265da4e710f5910)

#### 5. ARP

#### 6. OSPF



### <1> 密码学

在线教学视频 [Stanford Crypto](https://www.coursera.org/learn/crypto)

知乎讨论 [Zhihu](https://www.zhihu.com/question/36289177)

#### 1.  流密码与分组密码
* 流密码：线性反馈移位寄存器[LFSR](https://xz.aliyun.com/t/4630)、ZUC祖冲之算法
* 对称加密算法：DES、[AES](https://zhuanlan.zhihu.com/p/26014856)、RC5、RC2，CAST-128，Blowfish等，加密过程和解密过程所用的密钥是相同的。
* 分组密码：
  * DES：Feistel网络，输入，置换，16轮迭代乘机变换，逆置换、输出，安全性：DES靠S盒实现非线性变换。密钥穷举搜索、2DES-中间人攻击 [Eng](https://crypto.stackovernet.com/cn/q/9075) 、[Zh_cn](https://blog.csdn.net/gqqnb/article/details/8171918)
  * [AES](https://zhuanlan.zhihu.com/p/26014856)：前身Rijndael，轮函数：字节代换、行移位 、列混合、密钥加 
  * 分组密码模式：
    * ECB-每个明文组独立地以同一密钥加密（消息过长时不安全）
    * CBC-加密算法的输入是当前明文组与前一密文组的异或（CBC翻转攻击）
    * CFB-每次只处理输入的j比特，将上一次的密文作加密算法的输入以产生伪随机输出，该输出再与当前明文异或以产生当前密文
    * OFB-与CFB类似不同之处是本次加密算法的输入为前一次加密算法的输出
    * CTR-对计数器依次用k加密后与明文异或
 * [SM4]([https://neuqzxy.github.io/2017/06/15/%E6%AC%A3%E4%BB%94%E5%B8%A6%E4%BD%A0%E9%9B%B6%E5%9F%BA%E7%A1%80%E5%85%A5%E9%97%A8SM4%E5%8A%A0%E5%AF%86%E7%AE%97%E6%B3%95/](https://neuqzxy.github.io/2017/06/15/欣仔带你零基础入门SM4加密算法/)) 跟DES很像，使用非对称 Feistel网络
* 密码分析方法：差分攻击-选择明文攻击 [DES差分攻击](https://www.jianshu.com/p/f3bfe82a3a46)，线性分析-已知明文攻击
#### 2. 公钥密码-非对称加密
* 公钥密码-数学困难问题
  * RSA（基于大数分解困难问题）
  * [椭圆曲线ECC](https://blog.csdn.net/forest_open/article/details/81032539)（变形的离散对数问题，椭圆曲线算法已知整数k和点P，计算Q = kP较为容易；而已知Q和P，要反推k则困难得多）
  * [ElGamal](https://blog.csdn.net/weixin_42751456/article/details/90082367)（大数模的离散对数困难问题）

* Diffie Hellman 密钥交换协议
  * 系统参数：$g$
  * Alice的密钥对：$(x_a, y_a=g^x_a)$
  * Bob的密钥对：$(x_b, y_b＝g^x_b)$
  * 会话密钥：$k  =  g^{x_a \times x_b} ＝ y_a^{x_b} ＝y_b^{x_a} $

* RSA
  * 选择两个大素数$p$和$q$，秘密保存
  * 计算 $n=p \times q$；计算 $\phi (n)＝(p-1)(q-1)$
  * 选择整数 $e$，满足$1<e< \phi (n)$ ，且 $gcd(e, \phi (n))=1 $;
  * 计算$d$，满足 $d×e ≡ 1 mod \phi (n) $
  * $\{e，n\}$为公钥； $\{p，q， \phi (n)，d\} $为私钥。
  * 加密：$c ≡ m^e(mod n) $ ， 解密：  $m≡c^d(mod n)$

#### 3. 散列函数
哈希（Hash）函数 、单向性 、抗冲突性
MD5，SHA 
报文签别码（MAC ），本质上，MAC就是加了密的消息摘要。 

#### 4. 数字签名
提供防抵赖的鉴别和认证功能 ，如果说MAC是对称加密与散列函数的结合，那数字签名就是非对称加密与散列函数的结合。 

本质上，一个数字签名就是用私钥加密的消息散列值，比如DS = RSAKR(SHA(M))，即使用私钥KR，将消息M的SHA散列值通过非对称加密算法RSA加密。

**ElGamal数字签名**

 * 密钥生成：
   * 选择一个大的素数p
   * 选择g为域GF(p)的本原元素
   * 选择正整数x，计算$y=gx(modp)$。
   * Alice的公钥是（p，g，y），私钥是x。
 * 签名：
   * Alice用$H$ hash函数 将消息m进行处理，得$h=H(m)$
   * Alice选择秘密随机数k，满足 $0<k<p-1$，且$gcd(k, p-1)=1$，
   * 计算
     * $r=g^k(mod p)$
     * $s=(h-x^r)k-1(mod (p－1))$
     * Alice将$(m，r，s)$发送给Bob。

   * 验证
     * 计算h=H(m)
     * 用 Alice 的公钥，检验是否满足 $y^{r}r^{s}=g^{H(m)} ( mod  p)$。
     * 若是，则$(m，r，s)$ 是 Alice 发送的签名消息。

#### 5. 商用算法介绍

[商密算法SM2、SM3、SM4的用途和原理](https://yq.aliyun.com/articles/705759)

### <2> 机器学习

#### 1. K近邻-[KNN](https://www.jianshu.com/p/3f81f2ae781d)
**算法思想**：它的本质是让输入与给定的数据集进行距离的计算。如果最近的点大部分为某一类（比如说是A），则判定为A类。kNN中的k，就是跟输入比较的点的数量。这个是作为算法的一个参数。当然距离的计算方法有很多种，比如：欧拉距离、明科夫斯基距离

**算法的描述为**：

* 计算测试数据(当前点)与各个训练数据之间的距离(汉明距离)
* 按照距离的递增关系进行排序
* 选取与当前点距离最小的K个点
* 确定前K个点所在类别的出现频率
* 返回前K个点中出现频率最高的类别作为测试数据的预测分类

#### 2. 回归

##### (1).  [线性回归](https://www.jianshu.com/p/47ffb68f4f9f)

假设 特征 和 结果 都满足线性。即不大于一次方。这个是针对收集的数据而言。
收集的数据中，每一个分量，就可以看做一个特征数据。每个特征至少对应一个未知的参数。这样就形成了一个线性模型函数，向量表示形式：
$$h_{(\theta)}(x) = \theta ^{T}X$$

这个就是一个组合问题，已知一些数据，如何求里面的未知参数，给出一个最优解。 一个线性矩阵方程，直接求解，很可能无法直接求解。有唯一解的数据集，微乎其微。

基本上都是解不存在的超定方程组。因此，需要退一步，将参数求解问题，转化为求最小误差问题，求出一个最接近的解，这就是一个松弛求解。

求一个最接近解，直观上，就能想到，误差最小的表达形式。仍然是一个含未知参数的线性模型，一堆观测数据，其模型与数据的误差最小的形式，模型与数据差的平方和最小：

$$ J(\theta) = {{1} \over {2}} \sum_{i=1}^{m}(h_{\theta}(x^{(i)}) - y^{(i)})^2$$

这就是损失函数的来源。接下来，就是求解这个函数的方法，有最小二乘法，梯度下降法。

**最小二乘法**：是一个直接的数学求解公式，不过它要求X是列满秩的。

$$\theta = (X^{T}X)^{-1}X^{T} \vec y$$

**梯度下降法**：分别有梯度下降法，批梯度下降法，增量梯度下降。本质上，都是偏导数，步长/最佳学习率，更新，收敛的问题。这个算法只是最优化原理中的一个普通的方法，可以结合最优化原理来学，就容易理解了。

##### (2).  [逻辑回归](https://blog.csdn.net/viewcode/article/details/8794401)

逻辑回归的模型 是一个非线性模型，sigmoid函数，又称逻辑回归函数。但是它本质上又是一个线性回归模型，因为除去sigmoid映射函数关系，其他的步骤，算法都是线性回归的。可以说，逻辑回归，都是以线性回归为理论支持的。

#### 3. [朴素贝叶斯](https://www.cnblogs.com/ybjourney/p/4779488.html)

**条件概率**

与贝叶斯定理密不可分的条件概率：$P(A|B) ={P(AB) \over P(B)} $

其中$P(A|B)$表示的B发生的情况下A发生的概率，这就是条件概率。

现实生活中的很多问题，是很容易求出$P(A|B)$，但$P(B|A)$却很难求出，而$P(B|A)$却相对更有用，由此贝叶斯定理产生。

$P(B|A) = {  P(A|B)P(B) \over P(A)}$

**朴素贝叶斯分类器**

分类的原理是通过某对象的先验概率，利用贝叶斯公式计算出它的后验概率（对象属于某一类的概率），选取具有最大后验概率的类作为该对象所属的类。把Ａ和Ｂ看作是随机变量，那么P(B|A)就是Ｂ的后验概率，P(B)是B的先验概率。

对于朴素贝叶斯分类器，要做出两个假设：

（1）特征之间相互独立，即一个特征的出现于其它相邻的特征并无关系；

（2）每个特征同等重要。

#### 4. [K-means](https://zhuanlan.zhihu.com/p/54636128)

**算法过程**

* Randomly initialize K cluster centroids。随机初始化K个簇中心点，例如：K=3，
* cluster assignment。通过计算每个数据点与每个簇中心点的距离来把数据点分配到距离最小的簇上，通常使用欧几里得距离或余弦相似度来计算距离，计算距离之前需要先对特征值进行标准化，或者对特征值进行缩放来控制其权重。
$$ min \sum^{K}_{i=1} \sum_{x \in C_{i}} dist (C_i , x)^2$$
* move centroids。根据这些已分配的数据点，重新计算簇中所有向量的均值，来更新簇中心点（cluster centroids）。
* 重复步骤2和3来进行一定数量的迭代，直到簇中心点（cluster centroids）在迭代之间变化不大。


#### 5. [SVM](https://www.jianshu.com/p/7d25e56af510)

#### 6. [决策树与随机森林](https://zhuanlan.zhihu.com/p/30504716)



### <3> 深度学习 TODO
#### 1.



### <4> web安全 TODO

#### 1. SQL注入

**原理**

SQL注入攻击指的是通过构建特殊的输入作为参数传入Web应用程序，而这些输入大都是SQL语法里的一些组合，通过执行SQL语句进而执行攻击者所要的操作，其主要原因是程序没有细致地过滤用户输入的数据，致使非法数据侵入系统。

根据相关技术原理，SQL注入可以分为平台层注入和代码层注入。前者由不安全的数据库配置或数据库平台的漏洞所致；后者主要是由于程序员对输入未进行细致地过滤，从而执行了非法的数据查询。基于此，SQL注入的产生原因通常表现在以下几方面：

 * 不当的类型处理
 * 不安全的数据库配置
 * 不合理的查询集处理
 * 不当的错误处理
 * 转义字符处理不合适
 * 多个提交处理不当

**防御**

使用参数化的过滤性语句、检查用户输入的合法性、错误消息处理、存储过程来执行所有的查询、使用专业的漏洞扫描工具、确保数据库安全、安全审评。



#### 2. XSS

**原理**

HTML是一种超文本标记语言，通过将一些字符特殊地对待来区别文本和标记，例如，小于符号（<）被看作是HTML标签的开始，`<title>`与`</title>`之间的字符是页面的标题等等。当动态页面中插入的内容含有这些特殊字符（如<）时，用户浏览器会将其误认为是插入了HTML标签，当这些HTML标签引入了一段JavaScript脚本时，这些脚本程序就将会在用户浏览器中执行。所以，当这些特殊字符不能被动态页面检查或检查出现失误时，就将会产生XSS漏洞。

从攻击代码的工作方式可以分为三个类型:

* 持久型跨站：最直接的危害类型，跨站代码存储在服务器（数据库）。

* 非持久型跨站：反射型跨站脚本漏洞，最普遍的类型。用户访问服务器-跨站链接-返回跨站代码。

* DOM跨站（DOM XSS）：DOM（document object model文档对象模型），客户端脚本处理逻辑导致的安全问题。基于DOM的XSS漏洞是指受害者端的网页脚本在修改本地页面DOM环境时未进行合理的处置，而使得攻击脚本被执行。在整个攻击过程中，服务器响应的页面并没有发生变化，引起客户端脚本执行结果差异的原因是对本地DOM的恶意篡改利用。

**防御**

基于特征的防御、基于代码修改的防御、客户端分层防御策略

**防范XSS漏洞原则**

* 不信任用户提交的任何内容，对所有用户提交内容进行可靠的输入验证
* 实现Session标记（session tokens）、CAPTCHA（验证码）系统或者HTTP引用头检查，以防功能被第三方网站所执行，对于用户提交信息的中的img等link，检查是否有重定向回本站、不是真的图片等可疑操
* cookie防盗。避免直接在cookie中泄露用户隐私，例如email、密码，等等；通过使cookie和系统IP绑定来降低cookie泄露后的危险。这样攻击者得到的cookie没有实际价值，很难拿来直接进行重放攻击。
* 确认接收的内容被妥善地规范化，仅包含最小的、安全的Tag（没有JavaSeript），去掉任何对远程内容的引用（尤其是样式表和JavaScript），使用HTTPonly的cookie。



#### 3. WAF 



### <5> Linux二进制 TODO

#### 1. 工具集

binwalk、gdb、objdump、nasm、dd、pwntool



## 0x02 平台与架构

### <1> 大数据平台

#### 1. 数据库与文件系统

* [mongodb](https://www.runoob.com/mongodb/mongodb-tutorial.html) 是一个基于分布式文件存储的数据库。由 C++ 语言编写。旨在为 WEB 应用提供可扩展的高性能数据存储解决方案。是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。
  * **Python 操作 [MongoDB](https://www.runoob.com/python3/python-mongodb.html)**
* [redis](https://www.runoob.com/redis/redis-tutorial.html) 是一个开源的使用ANSI C语言编写、遵守BSD协议、支持网络、可基于内存亦可持久化的日志型、Key-Value数据库，并提供多种语言的API。它通常被称为数据结构服务器，因为值（value）可以是 字符串(String), 哈希(Hash), 列表(list), 集合(sets) 和 有序集合(sorted sets)等类型。
  * **python 操作 [redis](https://www.jianshu.com/p/ffc93a407448)**
* [hadoop](https://www.w3cschool.cn/hadoop/) 是一个开源框架，允许使用简单的编程模型在跨计算机集群的分布式环境中存储和处理大数据。它的设计是从单个服务器扩展到数千个机器，每个都提供本地计算和存储。
  * **Python 海量数据处理之_[Hadoop](https://blog.csdn.net/xieyan0811/article/details/78866604)**
  * **用 Python 玩转 Hadoop [简书](https://www.jianshu.com/p/70bd81b2956f)**
* [Hive](https://blog.csdn.net/l1212xiao/article/details/80432759) 是基于Hadoop的一个数据仓库工具，可以将结构化的数据文件映射为一张数据库表，并提供类SQL查询功能。
* [Kafka](https://www.tutorialspoint.com/apache_kafka/)是一个分布式，分区，复制的提交日志服务。它提供了类似于JMS的特性，但是在实现上完全不同，此外它并不是JMS规范的实现。kafka对消息保存时根据Topic进行归类，发送消息者成为Producer,消息接受者成为Consumer,此外kafka集群有多个kafka实例组成，每个实例()成为broker。无论是kafka集群，还是producer和consumer都依赖于zookeeper来保证系统可用性集群保存一些meta信息。[中文参考](http://www.aboutyun.com/thread-9341-1-1.html)

#### 2. 大数据

* 日志分析： [ELK](https://www.elastic.co/what-is/elk-stack) + FileBeats
* 机器学习与深度学习平台：[Spark](https://www.tutorialspoint.com/apache_spark/)

### <2> 数据分析工具

#### 1. numpy 

* [ENG doc](https://docs.scipy.org/doc/numpy/reference/)
* [CN doc](https://www.numpy.org.cn/)

NumPy的主要对象是同类型的多维数组。它是一张表，所有元素（通常是数字）的类型都相同，并通过正整数元组索引。在NumPy中，维度称为轴。轴的数目为rank。

例如，3D空间中的点的坐标 `[1, 2, 1]` 是rank为1的数组，因为它具有一个轴。该轴的长度为3。在下面的示例中，该数组有2个轴。

第一个轴（维度）的长度为2，第二个轴（维度）的长度为3。

```python
[[ 1., 0., 0.],
[ 0., 1., 2.]]
```

NumPy的数组类被称为ndarray。别名为 `array`。 请注意，`numpy.array` 与标准Python库类 `array.array` 不同，后者仅处理一维数组并提供较少的功能。 `ndarray` 对象则提供更关键的属性：

- **ndarray.ndim**：数组的轴（维度）的个数。在Python世界中，维度的数量被称为rank。
- **ndarray.shape**：数组的维度。这是一个整数的元组，表示每个维度中数组的大小。对于有n行和m列的矩阵，shape将是(n,m)。因此，`shape`元组的长度就是rank或维度的个数 `ndim`。
- **ndarray.size**：数组元素的总数。这等于shape的元素的乘积。
- **ndarray.dtype**：一个描述数组中元素类型的对象。可以使用标准的Python类型创建或指定dtype。另外NumPy提供它自己的类型。例如numpy.int32、numpy.int16和numpy.float64。
- **ndarray.itemsize**：数组中每个元素的字节大小。例如，元素为 `float64` 类型的数组的 `itemsize` 为8（=64/8），而 `complex32` 类型的数组的 `itemsize` 为4（=32/8）。它等于 `ndarray.dtype.itemsize` 。
- **ndarray.data**：该缓冲区包含数组的实际元素。通常，我们不需要使用此属性，因为我们将使用索引访问数组中的元素。

#### 2. [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html)

* 时间序列问题 [Doc](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html)
* 数据处理基础 [CSDN](https://blog.csdn.net/qq_16234613/article/details/64217337)

#### 3. [scipy](https://docs.scipy.org/doc/scipy-1.3.0/reference/)

建于NumPy之上，提供了一个用于在Python中进行科学计算的工具集：

- 特殊函数 ([scipy.special](http://docs.scipy.org/doc/scipy/reference/special.html))
- 积分 ([scipy.integrate](http://docs.scipy.org/doc/scipy/reference/integrate.html))
- 最优化 ([scipy.optimize](http://docs.scipy.org/doc/scipy/reference/optimize.html))
- 插值 ([scipy.interpolate](http://docs.scipy.org/doc/scipy/reference/interpolate.html))
- 傅立叶变换 ([scipy.fftpack](http://docs.scipy.org/doc/scipy/reference/fftpack.html))
- 信号处理 ([scipy.signal](http://docs.scipy.org/doc/scipy/reference/signal.html))
- 线性代数 ([scipy.linalg](http://docs.scipy.org/doc/scipy/reference/linalg.html))
- 稀疏特征值 ([scipy.sparse](http://docs.scipy.org/doc/scipy/reference/sparse.html))
- 统计 ([scipy.stats](http://docs.scipy.org/doc/scipy/reference/stats.html))
- 多维图像处理 ([scipy.ndimage](http://docs.scipy.org/doc/scipy/reference/ndimage.html))
- 文件 IO ([scipy.io](http://docs.scipy.org/doc/scipy/reference/io.html))

#### 4. matplotlib





## 0x03 大数据与网络安全 Doing

### <0> 大数据网络安全架构 : Zeek-Kafka+ELK

[基础架构](https://www.freebuf.com/sectool/179757.html)

### <1> 异常检测 : 离群点

**场景**：对先有业务，从业务流量中具体分析数据，从数据的统计特征角度出发，检测数据离群点。

* 异常检测的N种方法 - [阿里](https://mp.weixin.qq.com/s/kv-ZrOF4nnxXoQwFOodzjA)
* 机器学习-异常检测算法（一）- [Isolation Forest](https://zhuanlan.zhihu.com/p/27777266)
* 机器学习-异常检测算法（二）- [Local Outlier Factor](https://zhuanlan.zhihu.com/p/28178476)
* 机器学习-异常检测算法（三）- [Principal Component Analysis](https://zhuanlan.zhihu.com/p/29091645)

### <2> 攻击检测 : 具体问题具体分析

**场景**：对已知网络攻击，具体分析其攻击流程和攻击行为所产生的数据，设计数据规则提取、处理、分类器。

#### 1. 域名安全检测

##### (1). DGA 检测

##### (2). DNS隧道检测

#### 2. Web服务与应用检测

##### (1). SQL注入 检测

##### (2). XSS 攻击 检测

##### (3). webshell 检测

### <3> 对抗检测 : GAN 的思想

**场景**：黑客已知防御端使用了AI的检测方法，同理使用AI的方法绕过检测、对抗检测。

`对AI模型的对抗` 与 `对攻击分析的对抗` 的本质区别是  `对AI模型本身的攻击` 与 `对检测手段的对抗`。

**目的**：黑客寻求绕过检测的方法，检测寻求识别攻击变种的方法。

#### 1. 对AI模型的攻击

#### 2. 对攻击分析的对抗