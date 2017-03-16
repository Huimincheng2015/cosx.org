---
title: Sweave后传：统计报告中的大规模计算与缓存
date: '2011-01-03T11:23:59+00:00'
author: 谢益辉
categories:
  - 优化与模拟
  - 推荐文章
  - 统计软件
tags:
  - cacheSweave
  - Gibbs抽样
  - LyX
  - pgf
  - pgfSweave
  - R语言
  - Sweave
  - tikz
  - tikzDevice
  - UTF-8编码
  - 二维正态分布
  - 可重复研究
  - 密集型计算
  - 等高线图
  - 统计图形
  - 统计计算
  - 缓存
  - 随机模拟
slug: cache-objects-in-sweave-stat-computation-and-graphics
---

学无止境。我曾以为我明白了如何在Sweave中使用缓存加快计算和图形，但后来发现我并没有真的理解，直到读了另外一些手册才明白，因此本文作为前文“<a href="http://cos.name/2010/11/reproducible-research-in-statistics/" target="_blank">Sweave：打造一个可重复的统计研究流程</a>”之续集，向大家介绍一下如何在Sweave的计算和图形中使用缓存，以节省不必要的重复计算和作图，让那些涉及到密集型计算的用户不再对Sweave感到难堪。

如果你还没读前文，建议先从那里开始读，了解Sweave与“可重复的统计研究”的意义。简言之，Sweave是一种从代码（R代码和LaTeX）一步生成报告的工具，我们可以把整个统计分析流程融入这个工具，让我们的报告具有可重复性。然而，就普通的Sweave而言，这样做的一个明显问题就是，所有计算和作图都被融入一个文档之后，每次运行这个文档都要重复所有的计算和作图，这在很多情况下纯粹是浪费时间；比如，我只想对新添加的部分内容运行计算，而文档中的旧内容希望保持不变。这都是很合理的需求，我们需要的实际上就是一种缓存机制，将不想重复计算的对象缓存起来，需要它的时候再从缓存库中直接调出来用。

Sweave本身做不到缓存（或者很难做到），但由于R语言的扩展性以及一些疯子和天才的存在，我们可以通过R的一些附加包来完成缓存。这里的缓存有两种（不关心细节的读者可以略过）：

  * 一种是对R对象的缓存，比如数据、模型（拟合好的模型）和其它计算结果等，这个缓存容易理解，我们可以把它简单想象为把计算过程中的对象存入某些特殊的缓存库（文件），下次计算的时候先查看缓存库中是否存在我们需要的对象，如果存在，那么就直接加载进来，否则就重新计算；如（伪代码）： <pre class="brush: r">## 如果存在，就加载
if (file.exists('x.RData')) {
    load('x.RData')
}
## 如果当前工作环境中不存在x，那么就重新创建它
if (!exists('x')) {
    x = rnorm(100000)
}</pre>
    
    R对象的缓存可以通过<a href="http://cran.r-project.org/package=cacheSweave" target="_blank">cacheSweave包</a>（作者<a href="http://www.biostat.jhsph.edu/~rpeng/" target="_blank">Roger D. Peng</a>）实现，它真正采用的方法比上面的伪代码当然要高级（比如用代码的MD5值作数据库名等），不过用户可以不必关心这其中的细节。这种“当需要时才加载”的方式在术语上叫“延迟加载”，即Lazy Load，这在R里面也很常见，比如很多R包的数据都是采用延迟加载的方式（加载包的时候并不立刻加载数据，而是用`data(name)`在需要的时候加载）。</li> 
    
      * 另一种是图形的缓存，这是一个不可思议的魔法。cacheSweave的帮助文档和vignette中特别提到了它只能缓存R对象，无法缓存图形和其它附属输出，而开源世界的魅力就是你总能找到一些奇妙的解决方案。R包pgfSweave借力于pgf实现了图形的缓存。pgfSweave包的两位作者Cameron Bracken和Charlie Sharpsteen都是水文学相关专业出身，却在R的世界里做了这些奇妙的工作，让我觉得有点意外，这是题外话。pgf是LaTeX世界的又一项重大发明，它提供了一套全新的绘图方式（语言），而且它的图形可以通过LaTeX直接生成PDF输出（这是pgfSweave能实现缓存的关键）。关于pgf，我们可以<a title="pgf手册" href="http://www.ctan.org/tex-archive/graphics/pgf/base/doc/generic/pgf/pgfmanual.pdf" target="_self">翻一翻它726页的手册</a>，如果你能坚持看上10分钟，感叹超过50次，那么你一定是一位超级排版爱好者。它的图形质量之高、输出之漂亮，真的是让人（至少让我）叹为观止。同样，这里我也不详细介绍细节。pgf图形的“缓存”是通过“外置化”（externalization）来实现的，简言之，pgf图形有一种输出形式如下： <pre class="brush: r">\beginpgfgraphicnamed{graph-output-1}
\input{graph-output-1.tikz}
\endpgfgraphicnamed
</pre>
        
        如果LaTeX在运行过程中遇到这样的代码段，那么它会把tikz图形（tikz是高层实现，pgf是基础设施）先编译为PDF图形，等下次重复运行LaTeX的时候，这段代码就不必重新运行了，LaTeX会跳过它直接引入PDF图形。这样就省去了编译tikz图形的时间，同时也能得到高质量的图形输出。
        
        pgfSweave从R的层面上可以输出这样的代码段，并生成一个shell脚本来编译图形为PDF；而pgfSweave也会尝试根据R代码的MD5来判断一段画图的代码是否需要重复运行——如果R代码没有变化，那么图形就不必重制。这是自然而然的“缓存”。对了，pgfSweave对Sweave的图形输出作了扩展，新增了tikz输出，这是通过另一个R包tikzDevice实现的（同样两个作者），这个包可以将R图形录制为tikz绘图代码。pgfSweave依赖于cacheSweave包，把它缓存R对象的机制也引入进来，所以我们可以不必管cacheSweave，把精力放在pgfSweave上就可以了。</li> </ul> 
        
        介绍完血腥的细节之后，我们就可以坐享高科技的便利了。下面我以一个统计计算中的经典算法“Gibbs抽样”为例来展示pgfSweave在密集型计算中的缓存功能。
        
        Gibbs抽样的最终目的是从一个多维分布$f(X\_1,X\_2,\ldots,X\_n)$中生成随机数，而已知的是所有的条件分布$f(X\_1|X\_2,\ldots,X\_n)$、$f(X\_2|X\_1,\ldots,X\_n)$、……、$f(X\_n|X\_1,\ldots,X\_{n-1})$，并且假设我们可以很方便从这些条件分布中抽样。剩下的事情就很简单了：任意给定初始值$x\_1^{(0)},x\_2^{(0)},\ldots,x\_n^{(0)}$，括号中的数字表示迭代次数，接下来依次迭代，随机生成$x\_1^{(k)} \sim f(X\_1|x\_2^{(k-1)},\ldots,X\_n^{(k-1)})$、$x\_2^{(k)} \sim f(X\_2|x\_1^{(k)},\ldots,x\_n^{(k-1)})$、……、$x\_n^{(k)} \sim f(X\_n|x\_1^{(k)},\ldots,x_{n-1}^{(k)})$（迭代次数$k=1,\cdots,N$），也就是，根据上一次的迭代结果并已知条件分布的情况下，从条件分布中生成下一次的随机数（这个算法很简单，你什么时候看明白上标下标了就明白了）。这是个串行的过程，所以无法避免循环。
        
        接下来的计算没有那么复杂，我们仅仅用一个二维正态分布为例。当我们知道一个二维正态分布的分布函数时，我们也知道它的两个边际分布都是一维正态分布，而且分布的表达式也很明确，后文我会详细提到，读者也可以参考维基百科页面。生成一维正态分布的随机数对我们来说当然是小菜一碟——直接用`rnorm()`就可以了。这样，我们只需要交替从$f(X|Y)$和$f(Y|X)$生成随机数，最终我们就能得到服从二维联合分布的随机数（对）。假设我们要从下面的二维正态分布生成随机数：
        
        <p style="text-align: center;">
          $<br /> \left[\begin{array}{c}X\\ Y\end{array}\right]\sim\mathcal{N}\left(\left[\begin{array}{c}0\\ 1\end{array}\right],\left[\begin{array}{cc} 4 & 4.2\\ 4.2 & 9\end{array}\right]\right)<br /> $
        </p>
        
        详细过程和结果参见下面这份PDF文档（点击下载）：
        
        <p style="text-align: center;">
          <a href="http://cos.name/wp-content/uploads/2011/01/cache-pgfSweave-demo-Yihui-Xie.pdf">A Simple Demo on Caching R Objects and Graphics with pgfSweave (PDF)</a>
        </p>
        
        <p style="text-align: center;">
          <figure id="attachment_2810" style="width: 480px" class="wp-caption aligncenter"><a href="http://cos.name/wp-content/uploads/2011/01/cache-pgfSweave-demo-Yihui-Xie.pdf"><img class="size-full wp-image-2810 " title="二维正态分布随机数及其等高线图" src="http://cos.name/wp-content/uploads/2011/01/cache-pgfSweave-demo-Yihui-Xie-cache-graph.png" alt="二维正态分布随机数及其等高线图" width="480" height="480" srcset="http://cos.name/wp-content/uploads/2011/01/cache-pgfSweave-demo-Yihui-Xie-cache-graph.png 480w, http://cos.name/wp-content/uploads/2011/01/cache-pgfSweave-demo-Yihui-Xie-cache-graph-150x150.png 150w, http://cos.name/wp-content/uploads/2011/01/cache-pgfSweave-demo-Yihui-Xie-cache-graph-300x300.png 300w, http://cos.name/wp-content/uploads/2011/01/cache-pgfSweave-demo-Yihui-Xie-cache-graph-218x218.png 218w, http://cos.name/wp-content/uploads/2011/01/cache-pgfSweave-demo-Yihui-Xie-cache-graph-73x73.png 73w, http://cos.name/wp-content/uploads/2011/01/cache-pgfSweave-demo-Yihui-Xie-cache-graph-40x40.png 40w" sizes="(max-width: 480px) 100vw, 480px" /></a><figcaption class="wp-caption-text">二维正态分布随机数及其等高线图</figcaption></figure> 
          
          <p>
            我们生成了50万行随机数，并画了X与Y的散点图。由于我们设定了相关系数为0.7，所以图中自然而然显现出正相关；而等高线也体现出多维正态分布的“椭球形”特征。均值在(0, 1)附近，都和理论分布吻合。所以这个Gibbs抽样还不太糟糕。
          </p>
          
          <p>
            生成上面的PDF文档和图形的LyX/Sweave源文档在这里：
          </p>
          
          <p style="text-align: center;">
            <a href="http://cos.name/wp-content/uploads/2011/01/cache-pgfSweave-demo-Yihui-Xie.zip">A Simple Demo on Caching R Objects and Graphics with pgfSweave (LyX)</a>
          </p>
          
          <p>
            如果你已经按照我<a href="http://cos.name/2010/11/reproducible-research-in-statistics/" target="_blank">前面的文章</a>配置好你的工具（<strong>即使当时配置过，现在也需要重新配置</strong>，因为我最近作了重大修改），这个文档应该可以让你重新生成我的结果。文档中有两处关键选项：
          </p>
          
          <ul>
            <li>
              <code>cache=TRUE</code> 使得文档中的R对象可以被缓存；
            </li>
            <li>
              <code>external=TRUE</code> 使得图形可以被缓存；
            </li>
          </ul>
          
          <p>
            第一次运行文档时，也许需要等待一分钟左右的时间，因为R需要长时间的Gibbs抽样计算，并编译生成的图形为PDF，但如果下一次再运行这个文档，则速度会快很多，因为不需要再计算任何东西，只需从缓存加载就可以了。我们前一次的抽样结果已经在缓存库中了。
          </p>
          
          <p>
            本文至此可以结束，但真正想享用这个结果的读者可能还要继续看几个问题：
          </p>
          
          <ol>
            <li>
              pgfSweave对图形的缓存经常有点过度，即使你改动了代码，缓存仍然不会被替换，这种情况下你可以把生成的tikz和pdf图形删掉；
            </li>
            <li>
              中文问题：tikzDevice包好像还没有完全解决中文问题，作者正在尝试我提供的中文图形，也许在未来不久的新版本中会有完全的中文支持，但目前实际上我已经在我的自动配置脚本中解决了这个问题。我们只需要保证我们的中文LyX文档用UTF-8编码就可以了——在文档选项中使用CTeX类（以及UTF8选项），并设置语言为中文、编码为Unicode (XeLaTeX) (utf8)。这种设置至少我在Windows和MikTeX下可以成功编译中文Sweave文档。目前高亮代码功能在中文文档中还不能用，但我已经向相关作者发了补丁，等CRAN管理员回来发布新版parser包之后这个问题也会解决。所以，中文用户也不必担心，一切都（将）可以使用。
            </li>
            <li>
              依旧是样式问题：细心的读者也许能发现上面的PDF文档中的图形和这里网页中的图形略有区别，PDF文档中图形的字体和正文字体是一致的，这也是pgf的优势，前文第5节曾提到过。
            </li>
            <li>
              如果使用缓存，那么代码段中的对象都无法打印出来，即使用<code>print(dat)</code>也无法打印<code>dat</code>，这是因为缓存的代码段只管是否加载对象，而无法执行进一步的操作（包括打印），对于这种情况，我们应该设计好我们的Sweave文档结构，让某些代码段作计算（并缓存），某些代码段作输出（不要缓存）。
            </li>
          </ol>
          
          <p>
            这两篇文章都有点长，但最终的操作都极其简单。如果能理解这套工具，我想无论是写作业还是写报告，都将事半功倍（比如我就一直用它写作业）。
          </p>
          
          <p>
            祝大家在新的一年能写出漂亮、利索的统计文档，告别复制粘贴的体力劳动。
          </p>