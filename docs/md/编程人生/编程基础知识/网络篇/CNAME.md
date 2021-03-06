# CNAME

### 什么是CNAME？

在网上看了挺多解释，小白表示开始是有点懵的，后来自己总结了下前辈们的解释，如有理解错误，烦请各位指出。

先简单的说下域名解析（懂的不用看啦）： 在以前，人们用IP进行互访，后来发现IP太多不好记忆，便有了域名，比如www.baidu.com，你一看就知道是百度搜索引擎，而不需要管他的服务器IP是多少，但是在最开始通信的时候，电脑路由器不认识域名，只认得IP啊，要怎么去获得对应的IP呢，这时候有了域名解析，就是去请求网络上的DNS服务器，让他们来告诉你这个域名对应的IP是多少，至于请求DNS解析的详细过程，大家就自行搜索啦，这里不赘述。

然后概括地说：

   > + A记录是解析域名到IP，CNAME是解析域名到另外一个域名。

在说CNAME之前，要提到一个东西叫 A记录：

### A记录

A记录，即Address记录，它并不是一个IP或者一个域名，我们可以把它理解为一种指向关系：

   > + 域名 www.xx.com → 111.111.111.111
   > + 主机名 DD → 222.222.222.222

也就是当你访问这些域名或者主机名的时候，DNS服务器上会通过A记录会帮你解析出相应的IP地址，以达到后续访问目的。所以A记录是IP解析，直接将域名或主机名指向某个IP。


### CNAME

CNAME记录，也叫别名记录，相当于给A记录中的域名起个小名儿，比如www.xx.com的小名儿就叫www.yy.com好了，然后CNAME记录也和A记录一样，是一种指向关系，把小名儿www.yy.com指向了www.xx.com，然后通过A记录，www.xx.com又指向了对应的IP：

   > + www.yy.com → www.xx.com → 111.111.111.111

这样一来就能通过它的小名儿直接访问111.111.111.111了。

这时候有人问：这不多了一步嘛，不嫌麻烦？

假如这个时候我又想给原域名取几个小名儿，分别叫www.cc.com和www.kk.com那么存在下列指向关系：

   > + www.yy.com → www.xx.com → 111.111.111.111
   > + www.cc.com → www.xx.com → 111.111.111.111
   > + www.kk.com → www.xx.com → 111.111.111.111

突然服务器的IP地址因为一些不可描述的原因要换了，不再是111.111.111.111了，换成了333.333.333.333，这时候你发现，只要把www.xx.com的指向修改一下即可：

   > + 域名 www.xx.com → 333.333.333.333

这时候你又发现了，原来他的小名儿不需要做更改，直接就能访问服务器，因为他们都只指向了www.xx.com，服务器IP改没改它们不管。

那么假如不用CNAME，直接做A记录会怎样？

   > + www.yy.com → 111.111.111.111
   > + www.cc.com → 111.111.111.111
   > + www.xx.com → 111.111.111.111
   > + www.kk.com → 111.111.111.111

那么当111.111.111.111更改的时候，全部相关A记录指向关系都要做更改，这才叫麻烦…