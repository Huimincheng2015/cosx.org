---
title: 统计学专业应该使用什么样的统计软件（写给在统计学院学习的学弟学妹之四）
date: '2008-11-30T14:25:39+00:00'
author: 谢益辉
categories:
  - 推荐文章
  - 统计软件
tags:
  - R语言
  - SAS
  - SPSS
  - Stata
  - 分析数据
  - 收集数据
  - 整理数据
  - 统计分析
  - 统计软件
  - 表述数据
slug: which-statistical-software-should-we-use
---

过去两三年为院刊写了一些稿件，其中一部分是统计技术层面的，一部分是方法论和原则层面的，姑且作为对低年级统计学子们的一些学习建议，目的在于让大家学会擦亮自己的眼睛，辨明统计学的是与非。文章观点仅为一家之言，而且大多数情况下这些观点相对于流行的、教科书式的观点可能有显著差异，因此请各位小心阅读。

这次要求我写一篇关于统计软件的介绍，我想我也没这个本事去介绍所有的软件，因此私自把主题改成了“统计学专业应该使用什么样的统计软件”，窃以为这样写更有意义，不然这篇文章就变成了死板的统计软件使用手册。

关于统计软件，随着时间的推移，我最终以R语言为中心，基本废弃了其它工具的学习，换句话说，其它统计工具对我来说作用有限，不符合本人的统计分析思想和使用习惯。长话短说，本文的摘要为三个字：**用R吧**！<!--more-->

## 数据分析的需求

毫无疑问，选择都是根据需求而定的。换言之，世上没有万能的好软件。C语言、Fortran语言等低层语言在计算上效率非常高，而且人人都重视计算，但并非所有人都直接选择这些低层语言作为计算工具，原因就是计算速度快不是唯一的需求；SPSS号称统计功能齐全，它最近引进了Python语言，原因是什么？我个人认为模块化的统计分析过程已经不足以满足现代数据分析的需要——没有哪个问题是点鼠标计算一个回归模型就能解决的。我还见过有的公司花了几百万人民币买了SAS软件，其作用只是用来导入导出Excel数据，这就是没有明确需求而盲目选择的典型。

统计专业对软件的需求是什么？这要从我们直接从事的工作说起。统计的工作是什么？仍然是那个定义：收集、整理、分析和表述数据。统计软件在收集数据中一般用处不大（只有试验设计可能需要计算机生成试验表），而后三部分则处处需要软件的帮助。

整理数据要求软件具有良好的处理原始数据的能力。现实生活中的数据与教科书中的行列二维表格区别往往很大，因此我们需要通过整理把那些看似杂乱的数据变成统计中能使用的数据形式。我认为这种能力反映在两方面：（1）字符处理：例如原始数据为简单的文本格式，我们需要从中提取数据，则需要根据特定的规则读写文本数据，这往往涉及到一边计算一边取数据而不是一口气全读进来，更复杂的情况下还需要正则表达式的帮忙，举例来说，有时候数据分散放在多个文件中，我们需要将含有特定文件名的文件找出来，然后将其中符合条件的行读取出来，最终合并为所需的数据，或再距离来说，我们希望了解某个关键词在Google中随着日期推移，搜索结果数目的变化，这样我们需要动态查询Google网页，每次都把特定位置上的那个数字提出来；这些情况下，数据并非理想中的一张表格形式，需要我们预处理才能使用；（2）数据库的整理：随着数据存储技术的进步，数据往往都被存放在数据库中，统计人员在分析之前需要和数据库交互查询得到自己所需要的变量或观测，这些过程中，SQL是必不可少的，因此对SQL的支持是统计数据整理的基本要求。有人可能会产生疑问，为什么不把这样的工作交给计算机专业的人去做？殊不知统计分析乃是精工细活，数据整理并不仅仅是一个技术问题，更多的是对实际问题和统计模型的理解：我们需要解决什么实际问题？我们需要哪些变量？这些变量从哪里来？统计模型是什么？模型的变量是什么性质（离散、连续）？……在正式分析之前，我们对数据应该还有诸多类似的问题，不然仅仅依靠计算机技术，也许会计算出分类变量的均值（如某班级平均性别为1.35）或连续变量的频数等不合理的数据结果。当然，不可否认的是，纯粹的计算机技术对统计数据整理也是很有帮助的，这时，我们可能需要找计算机专业人士合作。

分析数据应该是统计软件的核心功能，显而易见，这要求统计软件的模型方法比较齐全，表面看来，这只是一个数量的问题，然而，它背后还隐藏着两个问题：（1）程序的可靠性或正确性：大多数商业软件都不是开源软件，我们并不知道其背后统计方法在计算机程序上的可靠性，从这一点上来讲，我们只能根据输出结果去判断程序是否可靠，而这种测试方法是非常低效的，因为这是“测标不测本”的做法，我们检验出来的问题说明软件确实在某方面有错误，但还有很多方面我们无法检验，这就如同统计假设检验的道理一样——零假设（软件没问题）可以被拒绝，但不拒绝不能说明零假设就可以被接受；举例来说，Excel在统计计算上漏洞百出，被诟病已久（参见<a title="为什么不使用Excel" href="http://yihui.name/cn/tag/excel/" target="_blank">此文</a>），然而除了那些被发现的问题，也许还有更多问题，我们（暂时）无法发现；（2）模型方法的变化与更新：我们都知道现在统计方法和模型的更新速度非常快，统计学科的发展日新月异，因此要求统计软件的发展速度能跟上学科的发展，不然统计方法的实施就会大受阻碍。除了这两个问题之外，统计分析还有个特点，那就是它的结果对象往往并不“整齐”，不会是行列二维表格，例如典型的回归分析中得到的结果可能有回归系数及其P值（矩阵形式）、R平方（单个数值）、残差（向量）、AIC（单个数值）等等，这也对统计软件提出了要求：我们需要能够灵活处理统计分析结果的软件，而不是生成无穷无尽的大篇幅报表，报表只是统计分析结果的汇总形式之一，并不一定满足用户的需要，例如有时候我们需要计算多个回归模型，而我们只关心拟合效果如何，因此对于每个回归结果，我们只需要提出R平方或者调整后的R平方之类的统计量并保存起来即可，而不需要输出多篇报表，然后人工去寻找最大的R平方值。

表述数据也是统计工作的重要组成部分，我认为这部分和统计分析部分有密切的关系，因为表述往往也含有分析的意味。表面看来这只是一个美学问题，而统计分析结果的表述却不光是美学这么简单。一方面，我们想将结果安排得美观或直观，这需要我们挑选关键的统计量来完成表达，而去掉那些无关紧要的结果，这也要求统计分析结果中的对象可以被任意提取；另一方面，统计图形也是数据表述的核心组成部分，因此要求统计软件有较强的统计图形展示能力。

## R语言<figure id="attachment_151" style="width: 300px" class="wp-caption aligncenter">

[<img class="size-medium wp-image-151" src="http://cos.name/wp-content/uploads/2008/11/rgui-300x237.png" alt="RGui：Windows下R的图形界面" width="300" height="237" srcset="http://cos.name/wp-content/uploads/2008/11/rgui-300x237.png 300w, http://cos.name/wp-content/uploads/2008/11/rgui.png 666w" sizes="(max-width: 300px) 100vw, 300px" />](http://cos.name/wp-content/uploads/2008/11/rgui.png)<figcaption class="wp-caption-text">RGui：Windows下R的图形界面</figcaption></figure> 

R是一门用于统计计算和作图的语言（<a title="R主页" href="http://www.r-project.org" target="_blank">http://www.r-project.org</a>），受S语言影响发展而来。R语言最初由新西兰奥克兰大学统计系的Robert Gentleman和Ross Ihaka合作编写。自1997年开始，R语言开始由一个核心团队开发，团队成员来自世界各地的大学和研究机构。迄今为止，R源代码已经经历了近70次主要更新，功能也在不断完善、增强中，主要统计功能包括线性模型/广义线性模型、非线性回归模型、时间序列分析、经典的参数/非参数检验、聚类和光滑方法等。R语言具有免费、开源及统计模块齐全的特征，已被国外大量学术和科研机构采用，其应用范围涵盖了数据挖掘、机器学习、计量经济学、实证金融学、统计遗传学、自然语言处理、心理计量学和空间统计学诸多领域。

谈R语言不能不提S语言，因为R语言的发展主要是受S语言和Scheme语言的影响，尤其是在统计分析部分，R和S非常相似。S语言在70年代由贝尔实验室统计部门开发出来，它的设计者们从一开始就做出了三个决定：

  1. 设计S语言的目的是为了提供一个完整的数据分析环境
  2. S语言应该包括交互式图形
  3. S语言应该有详细的在线文档

从这三点我们可以看出，S的直接目的在于数据分析，这是由于此前统计部门的工作者在实际工作中感觉到了当时的软件在数据分析上的不便，因此想开发一套针对数据分析的环境；统计图形的意义在于用户可以随时调用图形来交互式分析数据，这是探索性数据分析的重要部分，我们也都知道探索性数据分析在统计分析中的地位，因此图形作为S语言的开发重点有长远的战略意义；至于文档，则是统计软件与模型方法的重要连接，它意味着使用统计软件必须清楚文档，而读懂文档的前提是对统计方法有一定的了解，这就要求统计软件使用者具备一定的专业素质，从而避免“垃圾进垃圾出”的情况。

深感Fortran语言使用繁琐的S语言设计者们在一个大的Fortran库的基础上设计出了易用的S语言，它省去了每次都编写低层程序的麻烦，而只需要在高层语言中调用低层语言计算。这对那些常规的统计分析过程来说大大减轻了编程的工作，甚至可以说，常规的统计分析从此不需要“编程”了。S语言于1998年获得了ACM（美国计算机学会）的软件系统奖，获奖的原因是：

  * S系统永久性改变了人们分析、图示和处理数据的方式
  * S是一个精致、广为人们接受和不朽的完整软件系统

注意S语言是所有统计软件中唯一获此殊荣的软件系统。

S语言后来逐渐发展成为了商业软件S-Plus，但最初S语言的源代码都是被公布在网络上，因此R的几位作者可以参考S语言的源代码开发R语言，后来R语言也成为了自由软件的成员，获得了越来越多的支持者，大家开始为它找错误和漏洞、编写代码、撰写文档并对用户提供帮助。这所有的工作都是无偿的。

R语言除了在统计计算和统计作图上的方便之外，其面向对象的编程方式为统计分析带来了本质性的革命。在R里面，几乎所有的东西都是对象。每个对象都有自己的属性，我们可以自由操纵这些对象及其属性，包括提取、修改子对象，以及保存对象等。既然统计模型能和对象对应起来，那么只要一个新的对象在数学理论上存在或可计算，那么就可以很快用R写出来，而且用R写程序非常简便，一般来说它的代码几乎可以和数学公式完全对应，例如一个变量的m阶样本中心矩：

数学上为$\sum\_i (x\_i-\bar{x})^m / n$，R里面为`sum((x - mean(x))^m) / length(x)`；

再如回归系数向量（注意实际上R不是直接用下面这种矩阵求逆的方式计算的）：

数学上为$(X&#8217;X)^{-1}X&#8217;Y$，R里面可以写作`solve(t(x) %*% x) %*% t(x) %*% y`；

可以看出，R编程具有数学上的优越性，它内在的隐循环让我们节省了大量写繁琐代码的时间和精力，以上的例子若用低层代码编写必不可少涉及到大段的显式循环，而R将这些过程打包交给低层代码去计算，从而简化了编程的工作。实际上即便是这种“编程”在R里面也不多见，诸如回归等模型都有特定的函数lm()去计算，用不着我们自己写程序。从这种意义上来说，R没有图形界面完全不重要，因为在其它带图形界面的软件中点菜单本质上就是在设定函数的参数，对R来说只是敲键盘的事情。而R里面有大量能做的工作通过菜单操作是不可能做到的。这样的例子数不胜数。

（插播小广告：写这篇文章听着歌，刚好听到五月天的一首歌，让我想类比一句话：R只因统计而生！广告完毕。）

R与统计结合之紧密，是需要时间去体会的，这种味道，我在其它软件中没有感觉到过。这里不再多举例，仅留几个问题供大家思考、玩味：

  1. 为什么R很多函数对缺失值的处理方式是不要删掉缺失值（na.rm = FALSE），从而使得计算结果为NA？
  2. 为什么连简单的计算均值的函数mean()还有trim参数？均值不就是把所有数字加起来除以样本量么？
  3. 为什么R、Excel、SPSS、SAS等软件计算出来的分位数可能不一样？样本分位数的计算有多少种方法？参见quantile()函数。
  4. 为什么简单的箱线图还有notch参数？
  5. 为什么直方图hist()不能像SPSS那样自带选项让用户添加一条正态分布的密度曲线？

## Stata软件

Stata统计软件由美国计算机资源中心（Computer Resource Center）1985年研制。特点是采用命令操作，也可以菜单操作，程序容量较小，统计分析方法较齐全，计算结果的输出形式简洁，绘出的图形精美。不足之处是数据的兼容性差，占内存空间较大，数据管理功能需要加强。网址：http://www.stata.com。

Stata是各种商业统计软件中我最喜欢的一款（先声明我没有收取广告费），当然不管什么统计软件在我眼中都离R差远了，但是Stata确实做得还不错，虽然它的名声远不如SAS和SPSS，但其统计模块非常齐全，打开看看菜单就知道了。尤其是计量经济学和医学统计的人，如果惧怕写代码，不妨试试Stata。它分析小型数据应该是非常顺手，但能读取的数据种类有限，据我所知基本上仅仅是纯文本数据和Stata本身的数据（*.dta），而且计算受内存大小和程序版本种类限制，所以无法处理特大型的数据。

在用Stata菜单操作的时候它同时会在屏幕上输出与菜单对应的程序代码，因此若不熟悉Stata编程，可以通过这样的过程逐步学习，而且有些操作用菜单不方便实现，此时就可以结合不同的程序命令来完成。（例如指定模型中的分类变量要用xi:命令，但它在模型的菜单中无法直接指定，所以可以直接把xi:加到模型命令的前面）

另外需要提及的是，Stata自身有一本刊物Stata Journal，里面的内容比较学术，都是结合Stata命令讲一些统计方法如何实现，不过这本刊物要收费，这点对于学生来说是个比较大的障碍。所以话说回来，要看这类文章还是看R News吧，它不但不收费，而且文章质量也都比较高，明年就要更名为The R Journal了。

## SAS软件

SAS是英文Statistical Analysis System的缩写，即统计分析系统，最初由美国北卡罗来纳州立大学两名研究生开始研制，1976年创立SAS公司，2003年全球员工总数近万人，统计软件采用按年租用制。SAS系统具有十分完备的数据访问、数据管理、数据分析功能。SAS系统是一个模块组合式结构的软件系统，共有三十多个功能模块。网址：http://www.sas.com。

我在COS论坛（http://cos.name/bbs）上对SAS的介绍是“庞大的统计分析系统”，并没有强调它在统计分析方面的所谓优势。论坛上有几位朋友认为SAS编写代码的方式已经非常“恐龙级”了，对此我基本认同，不过鉴于我对SAS了解并不深入，所以不敢大放厥词。总之，“大”未必好，甚至以小人之心去揣测一下，也许“大”意味着代码臃肿。总之我们也看不到源代码，不知道它的统计分析代码怎么能写到七张光盘那么大。R的Windows安装文件30M，源文件16M左右。

别的不多说了，据我了解，我周围上下的同学在SAS上面花时间最多的是学习怎么把这个大家伙装进自己的电脑，然后道听途说一个proc名称，就开始把数据导进来写上几个变量名，然后提交run，直到有一天终于有了长达30页的报表了，就高兴了。大家不妨对照看看自己是不是这么做的。

## SPSS软件

SPSS是Statistical Package for Social Science的缩写（后来改成什么服务Service了），即社会科学统计程序包，20世纪60年代末由美国斯坦福大学的三位研究生研制，1975年在芝加哥组建SPSS总部。SPSS系统特点是操作比较方便，统计方法比较齐全，绘制图形、表格较有方便，输出结果比较直观。网址：http://www.spss.com。

算了，SPSS没什么好写的，自己打开看就是了。懂统计的不用学，不懂统计的学了也白学。反正要是不懂统计你总懂点右上角那个OK按钮吧。SPSS是傻瓜软件，所以有时候开玩笑戏称之为Stupid Package for Social Science。

匆匆行文，思想杂乱，请读者小心阅读。最后，以自编的一段大腕儿结束吧（关键的文字都在本文的第一部分）：

> “一定要找最庞大的软件，聘哈佛的统计教授，什么SAS啊SPSS啊，能买的全都给我买了，买就买最烧钱的软件，用最复杂的统计模型，比Breiman的随机森林还难，生成报表比红楼梦还长，什么互熵呀，BIC呀，随机效应呀，能挂的全TM给他挂上。计算时间最少也得一个星期，你要三天就算出来，你都不好意思跟人打招呼。软件就要买实用功能少的，1%截尾均值没法算，带凹槽的箱线图没法画，特冠冕堂皇的那种，到了分析的时候，甭管有用没用，它都得输出这么几句：‘All requested variables entered. Testing Global Null Hypothesis: BETA = 0’，一口地道的统计术语，倍儿有面子，你说买这样的软件得花多少钱啊？我觉得怎么也得一万吧。一万？那是软件小于600M的，其它至少十万，你还别嫌贵，弄不好人家还回收你的使用权，就一个字：黑！你得揣摩软件生产商的心理，能用这种软件写报告糊弄领导和期刊编辑的，根本就不在乎再多花几万块钱，什么叫统计分析你知道吗？真正的统计分析就是不怕得不出有用的结论，得不出倒显得报告深奥！所以我们选软件的口号就是‘不求最好，但求最贵！’”

<span style="color: #808080;"><strong>作者注</strong>：下面3号评论提到的文档可以作为大家选择软件的参考，感兴趣的读者不妨一读。谢谢江堂。</span>