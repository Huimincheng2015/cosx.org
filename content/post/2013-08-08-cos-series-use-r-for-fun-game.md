---
title: COS论坛精华帖系列——use R for fun系列之小游戏开发篇
date: '2013-08-08T18:27:06+00:00'
author: COS编辑部
categories:
  - 推荐文章
  - 软件应用
tags:
  - fun包
  - 交互
  - 游戏
  - 精华帖
  - 论坛
slug: cos-series-use-r-for-fun-game
---

系列以use R for fun为主题，以COS论坛上的精华帖、相关的package以及自己的一些code为素材，结合自身的一些编程体会，从而整合成文。

很多人都片面的认为R仅仅是一个自由免费的统计分析软件，加之其没有其他商业软件诸如SAS、SPSS等商业软件友好的界面而并不被很多人所喜爱，但事实上这非常片面，因此本文旨在通过一系列看似不务正业但实则蕴含一定R语言使用技巧的内容纠结部分user对R 的理解，同时也希望本文能勾起更多人对R的兴趣，推动R推动中国statistics的发展。

这里将其作为一个系列文章将会持续撰写，已经开工的包括小游戏开发篇、小应用开发篇、图像处理篇、搞怪作图篇、操纵office 篇、动画音乐视频制作篇等，各篇之间既有区别又相辅相成，涉及到的技能包括思维的开阔性(idea是核心)、编程艺术、可视化、矩阵运算、好package 的寻找等多个方面，可以说use R for fun 是user 对R综合应用能力的一个good test。

<!--more-->

***本文素材出处均已在正文注明**

小游戏开发篇本该在最后压轴，但考虑到它的吸引力，因此把招牌菜放在了第一道，以诱使各位能继续读下去，让提前倒胃口的p值降到最小，故而作为开篇。言归正传，游戏最主要特点在于它需要人机互动或者人人互动，而实现这一点的一个比较直接的途径就是实现对键盘鼠标信息的读取与响应，而这恰恰可以通过R中最最基础的交互式作图系统轻松实现。

**一、简述交互式作图**

既然是小游戏，能自娱自乐足矣，因此我们的目标是用最少的资源来效果最大化，故没有这必要大费周折去劳驾rgl、rggobi、iplots这些了，就靠最原始最屌丝的graphics和grDevices包丰衣足食。所谓交互式作图，关键在于交互，而交互的关键又在于获取鼠标键盘的信息(还不至于用手柄吧)，那么首先我们就来总结一下鼠标键盘上究竟有些什么有用的信息呢？键盘先来，键盘比较简单，无非就是不同的按键，而对于不同的按键R的前辈早已为我们安排好了对应的参数值，待我后面一一道来；而鼠标则相对复杂些，对于鼠标本身的响应而言，包括左击、右击、双击、移动四种，此外由于鼠标在显示器上还对应着一个小箭头，故鼠标上还承载着关于这个箭头的位置(坐标)甚至附近的信息，好在这一点R也给我们准备好了。了解这些之后，于是搞起！

**1.1 键盘信息的获取**

前面已经提到，对于键盘而言只有动作信息而没有位置信息，故只需考虑动作信息的获取。幸运的是一个function的一部分就可以非常完美的解决这个问题了，就是getGraphicsEvent()，来源于grDevices包，标准包的最大优点就是值得信赖。先来看下它的用法

<pre>getGraphicsEvent(prompt = "Waiting for input",
onMouseDown = NULL, onMouseMove = NULL,
onMouseUp = NULL, onKeybd = NULL,
consolePrompt = prompt)</pre>

在这里最重要的参数非onKeybd莫属，对于它的解释帮助文件中的描述是a function to respond to key presses，也就是它对应的取值是一个函数，是响应键盘操作的函数。需要注意的是，函数的输入参数为key，也就是指定响应的按键，如方向键就分别是&#8221;Left&#8221;, &#8220;Up&#8221;, &#8220;Right&#8221;, &#8220;Down&#8221;，另外如果是大写字母的话，默认指的是shift+小写字母，所以在programming的时候务必要区分大小写。附上一个简单的例子，请看下面这段代码：

<pre>par(bty="n",xaxt="n", yaxt="n",mar=c(0,0,0,0),cex=4,font=4);
plot(c(0,1),c(0,1),type="n",xlab="",ylab="");
num&lt;-1:99;
random1&lt;-function(key){
if(key=="a"){
rect(0.2,0.2,0.8,0.8,col="white",border=NA);
B&lt;-sample(num,1);
text(0.5,0.5,B,col="blue",cex=4);
}
}
getGraphicsEvent("run",onKeybd=random1);</pre>

运行之后只要按下“a”，作图界面就会跳出一个从1到99中随机抽取的一个数，每按一次就会随机抽取一个，按住不放就会这么一直下去，窃以为勉强可以算是一个简单的抽奖装置了(后面还会对其做些改进)。值得一提的是，关于参数prompt个人感觉并不是很重要，在上述例子中，其作用就是在命令窗口中显示了run(当然作图装口的标题也会对应改变)。

**1.2 鼠标信息的获取**

虽然键盘有很多按键，但都可以依葫芦画瓢，实属简单，而对于鼠标来说则相对复杂一些。

**1.2.1 位置信息**

关于位置信息则主要依赖于locator函数和identify函数，用起来也是非常好用，先说locator，它的用途是获取点的坐标，先看一下他的usage

<pre>locator(n = 512, type = "n", ...)</pre>

看到这么简洁的usage瞬间觉得神清气爽，意思非常简单，n指的是你取点的上限，缺省为512个点，type指的则是取点过程中描点的方式，取值的范围主要是四种，分别是&#8221;n&#8221;,&#8221;p&#8221;,&#8221;l&#8221;,&#8221;o&#8221;，这里缺省值是&#8221;n&#8221;，也就是只取值不画点，而&#8221;l&#8221;则是把点与点连成线了，&#8221;p&#8221;就是点，&#8221;o&#8221;的话你用了就知道了。既然用法这么简单那就先用为快，再次请看代码：

<pre>par(bty="n",xaxt="n", yaxt="n",mar=c(0,0,0,0),cex=5,font=4);
plot(c(0,1),c(0,1),type="n",xlab="",ylab="");
locator(n=5,type="l",lwd=2,col=sample(1:7,1));</pre>

这让我想起来学arcGIS的时候那坑爹的大作业——描地图，把所谓的栅格数据矢量化，泪崩。

接下来讲讲identify这个函数，也是一个很神奇的函数，它通过鼠标点击一幅散点图(只要本质上有点就行，折线图什么的问题也是不大的)识别鼠标周围的数据点，并且可以给辨识出的数据添加标签，其实也就是捕捉我们需要的点，这在交互中非常有用，用法：

<pre>identify(x, y = NULL, labels = seq_along(x), pos = FALSE,
n = length(x), plot = TRUE, atpen = FALSE, offset = 0.5,
tolerance = 0.25, ...)</pre>

``前提是要已经存在一幅图，解释一下参数，x和y无需多言，散点图的原始数据，labels为数据的标签，也就是显示在屏幕上的，缺省情况用的就是阿拉伯数字的正整数，n指的是最大识别的点的上限，tolerance是一个识别的标准，越小识别的精度也越高，也就是只有离原始数据充分近的点才会被识别，当plot=T的时候label会显示出来，而atpen和offset则是描述了标记label 的位置。 同样附上一个简单的例子：

<pre>par(bty="n",xaxt="n", yaxt="n",mar=c(0,0,0,0),font=4);
plot(c(0,1),c(0,1),type="n",xlab="",ylab="");
xx&lt;-runif(100);
yy&lt;-runif(100);
identify(xx,yy);</pre>

运行一下之后是不是有一种寻宝的感觉呢？别急后面会有更好玩的。

**1.2.2 动作信息**

对于动作信息而言，从某种程度上讲跟前面提到的键盘属于异曲同工，只不过这里所用的参数是onMouseDown, onMouseMove, onMouseUp，参数的意义看名字就能知道了，同样参数对应的是一个函数，这里函数的输入参数变成了三个，分别是button、x、y，button是需要你指定点击鼠标的形式，左击为对应的取值是0，右击为1，x和y指的就是鼠标所在点，也就是那个箭头。关于具体用法的装逼解释请进一步阅读帮助文件，但个人觉得一个example胜过千言万语，因此这里同样通过一个例子来解决所有问题，请看代码：

<pre>par(bty="n",xaxt="n", yaxt="n",mar=c(0,0,0,0),cex=5,font=4);
plot(c(0,1),c(0,1),type="n",xlab="",ylab="");
move&lt;-function(button,x,y){
points(x,y,cex=2,col=sample(1:7));
}
getGraphicsEvent("",onMouseMove=move);</pre>

运行之后就会发现，现在你可以自己涂鸦了。是不是很棒！

**二、游戏界面制作**

了解了交互式作图，可以说攻克了最大的技术难关，但是再核心也只是一个环节，对于玩游戏的人而言，他们永远不会去关心你的交互是如何实现的，他们只会关注表面的东西，这就涉及到游戏开发过程中的另一个重要环节——游戏界面的制作。R中主要包含了四套作图系统，分别是基础作图系统、grid、lattice、ggplot，同样对于做个小游戏界面而言，用最原始的基础作图系统就足矣，毕竟咱不是暴雪、EA。

**2.1 par函数**

如果足够细心的话那么肯定已经注意到了我之前给的小例子中在最前面总会加上这么一句

<pre>par(bty="n",xaxt="n", yaxt="n",mar=c(0,0,0,0),cex=5,font=4);</pre>

par是一个极其重要的设置图形参数(当然也可以获取)的函数，尤其是对于非常想追求作图效果的user而言(ggplt2脑残粉可暂时忽略这句话)。随便举个例子，总不可能在游戏界面中出现一个坐标系吧，那难免也太丧心病狂了，这也就是bty=&#8221;n&#8221;的意义之所在了。因此做界面的一个首要条件是要学会设置，也就是会运用par函数(很多设置在plot等绘图函数也能实现)，par函数参数众多，覆盖面很全，想详细了解的仔细阅读帮助文件即可。另外谢大在他未完成的在线著作《现代统计图形》中也有对par函数和plot函数详细解读，还包括介绍哪些参数是只能在par 中设置的，可以说是提取了帮助文件中的精华部分翻译后展现出来，很有学习价值。

**2.2 低级绘图函数**

游戏不可避免的需要在现有作图窗口下重复作图，而这件事情像plot之类的是完不成的(再用一个plot就前功尽弃了)，因此只能交给低级绘图函数来做，需要充分利用低级绘图函数的另一个重要原因就是低级绘图函数可以为我们画一些特殊图形提供便利，如多边形，箭头等。这也是为什么我在之前的代码中的第二行都无一例外的加了

<pre>plot(c(0,1),c(0,1),type="n",xlab="",ylab="");</pre>

用plot把作图设备开出来接下来就可以用低级绘图函数为所欲为了。一些常用的低级绘图函数包括了points(点)、lines(曲线)、segments(线段)、rect(矩形)、arrows(箭头)、polygon(多边形)等等，当然也不要忘了用来添加文本的text()等。

**2.3 色彩搭配**

关于基础作图系统的中色彩，主要由grDevices包负责，事实上它所提供的调色功能非常强大，而我们只是利用到其中的极小一部分，关于该包，可以参考[这里](http://stat.ethz.ch/R-manual/R-devel/library/grDevices/html/00Index.html)，所有内容尽收眼底，当然图省事图方便同样可以参考谢大的《现代统计图形》，着实是本好书，里面专门有一节讲色彩。由于本人审美观非常拙计，因此点到为止，再说下去就是误导了。

**2.4 写function能事半功倍**

通过写function可以简化编程过程中的很多麻烦事。举个例子，如果游戏需要多处用绘制旗子，每次重复操作岂不是很麻烦，就算可以复制粘贴，但是一方面影响运行效率，另一方面影响代码可读性，因此在这种情况下，我们通过如下代码编写一个绘制旗子的function，就可以一劳永逸了。

<pre>plot.flag&lt;-function(x,y,...){
polygon(c(x-0.1,x-0.1,x+0.25,x+0.25),
c(y+0.1,y+0.3,y+0.3,y+0.1),
col="red",border="red");
polygon(c(x-0.3,x-0.3,x+0.3,x+0.3),
c(y-0.3,y-0.2,y-0.2,y-0.3),
col="black",border="black");
segments(x-0.1,y+0.3,x-0.1,y-0.2);
}</pre>

比较合适的做法，把有用的函数事先在代码最前面先定义好，function写完后不妨先测试一下，这样会显得有条理而不容易出错，事实上在各个情况都是如此。

**三、示例-瞻仰COS前辈**

示例永远都是王道，接下来所介绍的几个示例都出自COS论坛，由统计之都的前辈大牛们所做，现在都已经被收录在fun包中，可以说属于成功的典范。在[该包的github上](https://github.com/yihui/fun/tree/master/R)都可以找到源代码，当然直接在package中也可以找到。

**3.1 (围棋)五子棋**

其在fun包中的函数为gomoku，意为五子棋，唯一的一个tag是用于设置棋盘的大小，默认为19，即棋盘大小为19*19，也是标准围棋棋盘，关于该idea的原帖来自于[COS论坛](http://cos.name/cn/topic/104750#post-221212)。其实原理也非常简单，利用locator 函数的交互获取坐标信息，然后根据坐标信息寻找到离其最近的一个交叉点，再利用points函数在改点落子，从而实现了在R中下围棋或者五子棋。唯一欠缺的是里面似乎欠缺对胜负的评判，无论是对五子连珠的判断还是围棋中点目，并没有在其中添加相关的命令。有兴趣的读者也可自行去研究源代码(代码并不长)。看起来可有模有样啊！

[<img class="aligncenter size-medium wp-image-8135" alt="weiqi" src="http://cos.name/wp-content/uploads/2013/08/weiqi-300x280.jpeg" width="300" height="280" srcset="http://cos.name/wp-content/uploads/2013/08/weiqi-300x280.jpeg 300w, http://cos.name/wp-content/uploads/2013/08/weiqi-500x468.jpeg 500w, http://cos.name/wp-content/uploads/2013/08/weiqi-320x300.jpeg 320w, http://cos.name/wp-content/uploads/2013/08/weiqi.jpeg 551w" sizes="(max-width: 300px) 100vw, 300px" />](http://cos.name/wp-content/uploads/2013/08/weiqi.jpeg)

**3.2 扫雷**

还记得之前提到的画旗子么，这里就用上了，当然远远不止画旗子这么简单，如果说棋类的胜负可以由双方自行判断的话，那么扫雷这种人际交互的游戏就肯定做不到了，因此代码也比之前的要长很多。在这段代码中采用了getGraphicsEvent函数进行交互，分别针对左击和右击设置不同的相应。效果也非常棒，也是笔者熬夜必备游戏之一。忘了说了，对应的函数是mine_sweeper()，对应的参数分别可以设置大小，雷的个数等，相当调整游戏的难度，论坛原帖在[这里](http://cos.name/cn/topic/14477#post-14477)。

[<img class="aligncenter size-medium wp-image-8144" alt="mine_sweeper" src="http://cos.name/wp-content/uploads/2013/08/mine_sweeper-300x300.png" width="300" height="300" srcset="http://cos.name/wp-content/uploads/2013/08/mine_sweeper-300x300.png 300w, http://cos.name/wp-content/uploads/2013/08/mine_sweeper-150x150.png 150w, http://cos.name/wp-content/uploads/2013/08/mine_sweeper-500x500.png 500w, http://cos.name/wp-content/uploads/2013/08/mine_sweeper.png 672w" sizes="(max-width: 300px) 100vw, 300px" />](http://cos.name/wp-content/uploads/2013/08/mine_sweeper.png)**3.3 关灯游戏**

****关灯游戏貌似在手机上挺流行的，规则也无需多说，非常好玩的一个游戏，同样是我刷夜必备。同样是用到了getGraphicsEvent函数进行交互操作，代码非常简洁，可读性很强，不过可玩性更强。这里也就不再多说了。对应的函数是lights_out()，关于函数的参数width和height用于设置灯的个数，col.off和col.on分别用于表示等熄灭和点亮的颜色。比较有意思的参数是seed, 用来设置随机数种子，也就是能让你每次都处于同一个起点，比较方便作弊。

[<img class="aligncenter size-medium wp-image-8138" alt="light" src="http://cos.name/wp-content/uploads/2013/08/light-296x300.jpg" width="296" height="300" srcset="http://cos.name/wp-content/uploads/2013/08/light-296x300.jpg 296w, http://cos.name/wp-content/uploads/2013/08/light-494x500.jpg 494w, http://cos.name/wp-content/uploads/2013/08/light.jpg 549w" sizes="(max-width: 296px) 100vw, 296px" />](http://cos.name/wp-content/uploads/2013/08/light.jpg)

此外fun包中的游戏还有拼图游戏(sliding\_puzzle)和汉诺塔(tower\_of_hanoi)，论坛原帖的地址：[拼图](http://cos.name/cn/topic/14516)、[汉诺塔](http://cos.name/cn/topic/101199#post-201430)。

**四、示例——如何DIY？**

****下面的示例并没有任何可取之处，效果更是无法上面的这些个示例相比，之所以厚着脸皮放在这里的目的在于说明programming的过程，一个由简到繁不断改进的过程，好文章是改出来的同样好程序也是改出来的，事实证明，通过改进至少可以把很挫编程略微有点挫。

**4.1 抽奖装置**

这个示例是对之前解释getGraphicsEvent函数时所给example的改进。当面临选择时，纠结是难免的，比方说谁去拿外卖，选谁做代表，谁能中奖等等。这里我们不妨以那段示例为基础，给界面做一些修缮，这样一个简陋的抽奖装置就完成了。

<pre>par(bty="n",xaxt="n", yaxt="n",mar=c(0,0,0,0),cex=4,font=4);
plot(c(0,1),c(0,1),type="n",xlab="",ylab="");
text(0.4,0.9,"Who's turn?",
col=rainbow(1000)[sample(1:1000,1)],cex=1);
text(0.8,0.1,"made by Chen-ang Liu",
col=rainbow(1000)[sample(1:1000,1)],font=2,cex=0.2);
num&lt;-1:99;
A&lt;-100;
run&lt;-function(key){
if(key=="s"){
rect(0.2,0.2,0.8,0.8,col="white",border=NA);
B&lt;-sample(num,1);
A&lt;-c(A,B)
text(0.5,0.5,B,col=rainbow(1000)[sample(1:1000,1)],cex=4);
}
}
getGraphicsEvent("run",onKeybd=run);</pre>

当然这只是对界面做了更改，还可以在功能上进行改进，简单一点的，可以增加一些文字素材，表明其用途，再进一步，将其与鼠标结合，从而扩大功能(如增加一些按钮等)，考虑到前面已经有这么多成功的案例，这里也就不再多加赘述了。

[<img class="aligncenter size-medium wp-image-8139" alt="choujiang" src="http://cos.name/wp-content/uploads/2013/08/choujiang-300x300.jpeg" width="300" height="300" srcset="http://cos.name/wp-content/uploads/2013/08/choujiang-300x300.jpeg 300w, http://cos.name/wp-content/uploads/2013/08/choujiang-150x150.jpeg 150w, http://cos.name/wp-content/uploads/2013/08/choujiang-500x500.jpeg 500w, http://cos.name/wp-content/uploads/2013/08/choujiang.jpeg 558w" sizes="(max-width: 300px) 100vw, 300px" />](http://cos.name/wp-content/uploads/2013/08/choujiang.jpeg)

&nbsp;

**4.2 其他？**

事实上顺着上面的思路很多小游戏都可以应运而生，读者不妨自己尝试下？

**五、一条龙之作——sudoku包**

****本想不提这个包的，因为这个包实在是统计之都没啥关系，但本着求是的校训还是在最后简单提一下，因为该包对数独游戏的构建上已经做到了非常完整了，某种程度上讲也是把**无聊**推向了极致(我觉得我已经够无聊了)，该包可以在CRAN上下载，包中共有八个函数，功能涵盖了获取数独题(从<http://www.sudoku.org.uk>中)、生成数独题、解数独题(这是最不无聊的部分)、写数独题当然还有玩数独。玩数独用到的函数是playSudoku()，如果不是在windows下的话，还需要安装tkrplot包。直接用默认设置即可，输入命令(加载这种话就不用我多说了吧)

<pre>&gt; playSudoku()
Solving...done!
? -- this help
1-9 -- insert digit
0,' ' -- clear cell
r -- replot the puzzle
q -- quit
h -- hint/help
c -- correct wrong entries (show in red)
u -- undo last entry
s -- show number in cell
a -- show all (solve the puzzle)</pre>

<pre>Ready!</pre>

玩法是把鼠标拖至空格处，然后输入数字即可，如果受不了了那么可以按照上面的提示寻求相应的帮助。
  
[<img class="aligncenter size-medium wp-image-8140" alt="shudu" src="http://cos.name/wp-content/uploads/2013/08/shudu-300x296.jpg" width="300" height="296" srcset="http://cos.name/wp-content/uploads/2013/08/shudu-300x296.jpg 300w, http://cos.name/wp-content/uploads/2013/08/shudu-500x494.jpg 500w, http://cos.name/wp-content/uploads/2013/08/shudu-303x300.jpg 303w, http://cos.name/wp-content/uploads/2013/08/shudu.jpg 560w" sizes="(max-width: 300px) 100vw, 300px" />](http://cos.name/wp-content/uploads/2013/08/shudu.jpg)
  
关于小游戏就暂时写到这了(可能的话会再来一篇进阶篇)，如果有更好的示例或者idea欢迎和我或者COS的几位前辈联系，并及时更新，当然如果很棒的话目测就果断收录fun包了，下一篇将是小应用开发篇，里面将会给出更多的示例和demo，内容更精彩！

**关于作者**

  * 刘辰昂，浙大准大四本科，统计之都主站编辑
  * weibo：[求证1加1](http://weibo.com/2011764505/profile?topnav=1&wvr=5)
  * blog: <http://chenangliu.info/cn/>
  * email: liuchenang@gmail.com