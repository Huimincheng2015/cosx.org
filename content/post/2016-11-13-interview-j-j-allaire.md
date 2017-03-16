---
title: RStudio的前世今生——RStudio创始人专访
date: '2016-11-13T22:33:57+00:00'
author: COS编辑部
categories:
  - 统计之都
  - 职业事业
  - 软件应用
tags:
  - COS访谈
  - J.J. Allaire
  - RStudio
  - R语言
slug: interview-j-j-allaire
---

本文是一篇Joseph B Rickert（简称JBR）对J.J. Allaire（RStudio的创始人和首席执行官）的采访稿，[原文在此](https://www.rstudio.com/rviews/2016/10/12/interview-with-j-j-allaire/)。统计之都与作者沟通后得到授权将其翻译为中文，希望可以让广大读者能够更多了解在R的世界中这个叫RStudio的地方。在这次采访中讨论了RStudio的历史、使命和J.J.的未来愿景。 短暂的交谈中讨论了各种各样的主题，包括RStudio的业务、R语言的发展、R联盟对R社群的重要性以及J.J.对R新手们的建议。

&nbsp;<figure id="attachment_13297" style="width: 158px" class="wp-caption aligncenter">

<img class="size-full wp-image-13297" src="http://cos.name/wp-content/uploads/2016/11/图片-1.png" alt="J.J. Allaire" width="158" height="158" srcset="http://cos.name/wp-content/uploads/2016/11/图片-1.png 158w, http://cos.name/wp-content/uploads/2016/11/图片-1-150x150.png 150w" sizes="(max-width: 158px) 100vw, 158px" /><figcaption class="wp-caption-text">J.J. Allaire</figcaption></figure> 

<!--more-->

<span style="color: #000080;"><strong>JBR：</strong><strong>问您最早是如何接触到</strong><strong>R</strong><strong>的？</strong><strong>R</strong><strong>最开始引起您的关注时，您在做什么？为什么是</strong><strong>R?</strong></span>

**J.J.：**我本科的时候主修经济学和政治科学，这两门学科让我对量化研究产生了兴趣。当我还是学生的时候，我用过SAS、SPSS和EXCEL。这是我首次接触软件和计算，它们深深吸引了我，而后来我的职业生涯最终更多围绕软件开发而不是量化分析。大概8年前，我在工作的同时在寻找其它值得从事的事。我很清楚自己心里想要的是希望自己开发的软件是开源的，因为我想开发出一种能长期对所有人都是免费且容易获得的软件。

也就是在那个时候我接触到了R，当了解了这个稳健并被广泛应用的开源统计计算环境时，我觉得它棒棒哒。我想它将是我倾其精力的一个伟大领域。我在学校的时候，最早对量化分析很感兴趣，同时，我掌握了重要的编程能力。我正好可以把这些能力应用到R上，做出有意义的贡献。

<span style="color: #000080;"><strong>JBR</strong><strong>：是否有什么特别的事件激励您创立</strong><strong>RStudio</strong><strong>？当您成立它时，您设想它会是一家什么样的公司？</strong></span>

**J.J .：**RStudio一开始并不是作为一家公司而成立的。它最开始仅仅是一个我自己从事的开源项目。最初，我开始研究一个基于R的IDE（集成开发环境）的Web概念。大约过了九个月，我意识到凭我一己之力搭建这个IDE实在是太艰难了，所以我找来了Joe Cheng跟我一起干。Joe和我在过去的几家公司共事过。当时我跟他说：“Joe，我无法保证这将成为一家公司。它可能只是一个开源项目，这对你来说可以吗？”他说“当然可以。”最初这真的只是我们两个人一起从事的一个开源项目，而且也没有打算将它必须做成一家公司。我当时想的是，如果这个项目可以演变成一个公司，那将是极好的，但这并不是必须的。

<span style="color: #000080;"><strong>JBR：</strong><strong>那您对</strong><strong>RStudio</strong><strong>现在这个结果感到惊讶吗？</strong></span>

**J.J .：**我当初其实并不知道会发展成什么样，但可以肯定的一点是开源软件有可能被广泛使用。说实话我并不惊讶R会大放异彩，但我真的没想到自己会创立一个跟R相关的公司。说实话，我惊讶于现在的任何结果。真是万万没想到。

<span style="color: #000080;"><strong>JBR</strong><strong>：请问您在</strong><strong>RStudio</strong><strong>扮演什么样的角色？您主要负责公司运营还是负责产品开发呢？是什么在每天早上唤醒您呢？</strong></span>

**J.J .：**我主要做的是编写软件。这是我最喜欢做的事。虽然我是RStudio的首席执行官，但事实上我并不经营公司，而是与其他从事公司运营的人员合作，特别是Tareef Kawaf——RStudio的总裁，目前Tareef主要负责公司运营。

我将自己的绝大部分时间，超过百分之八十的时间都用于编写软件。一开始我担任RStudio IDE的主要开发人员，之后Joe和我一起工作了几年。现在我一方面继续负责IDE，另一方面也是很多R包的主要开发者，包括R Markdown包。同时我也是其他一些包的维护者，如htmlwidgets和dygraphs包，此外也协助了shiny和Rcpp等。

<span style="color: #000080;"><strong>JBR</strong><strong>：请问您的一个典型的工作日是什么样子的？</strong></span>

**J.J .：**一个典型的工作日，我从查看电子邮件开始，看看有没有什么紧急事件，对一些请求进行反馈或看看一些错误。我可能花大约一个小时来查看我的收件箱，然后花五六个小时为各种产品和包编写代码。之后，当RStudio的西雅图办公室的员工在我的中午时间上网的时候，我可能在网上和他们交流一下（译者注：J.J.在美国东部波士顿办公室上班，与西海岸时差三小时）。然后，也许我继续码些代码直到一天结束。各种各样的事情都会发生，但我常规需要参加的会议很少。我努力保持各项事务条理清晰以便于产品开发工作。

<span style="color: #000080;"><strong>JBR</strong><strong>：从外部看来，</strong><strong>RStudio</strong><strong>用大量的资源来开发开源包和免费产品。许多人都想知道</strong><strong>RStudio</strong><strong>如何能成为一个企业。您能简单谈一谈</strong><strong>RStudio</strong><strong>的商业计划吗？</strong><strong>RStudio</strong><strong>究竟如何营利呢？<br /> </strong></span>

**J.J.：**好的，首先，RStudio公司的使命是开发用于数据分析和统计计算的开源软件。所以，如果你看到我们正在开发大量的开源软件，你不必吃惊，因为这正是我们最主要的使命。与此同时，为了完成我们的使命，我们需要引进尽可能多的人才。显然我们还需要发展和壮大一个围绕R的业务。

我想说，商业业务有两个主要方面，第一个是关心想要大规模部署R的组织，这里的规模是指计算规模或者是在更大的组织内使用R。为了满足这些要求，我们增强了一些服务器产品的商业版本，例如RStudio Server Pro和Shiny Server Pro，它们具有大规模部署R的功能。虽然我们的开源产品是可以免费获取的，可能许多人不会购买我们的专业产品，但当客户对R更加认真时，或者需要在更大的环境中部署R时，他们就会倾向于购买我们的专业产品。所以，这就是我们营利的主要方式——靠那些专业的服务器产品营利。

此外我们还有一个云业务，通过网络提供我们的产品服务。例如，我们有shinyapps.io用来部署Shiny应用程序。目前它并不是我们业务的一大部分，但我们预计它将变得越来越重要，同时我们也期待在未来有其它云服务的出现。

<span style="color: #000080;"><strong>JBR</strong><strong>：请问</strong><strong>RStudio</strong><strong>的长期目标是什么？</strong></span>

**J.J.：**RStudio的核心目标是集中为用户创造一个优雅并高效的使用R的环境。这里我主要指的是RStudio IDE。一个良好的使用R的工作环境，不仅需要为用户提供工具以确保高效工作，还需要将R内的所有丰富的内容展示出来，让人们清楚R可以胜任的工作，之后可以随心所欲地使用R。

其它目标集中在创建R的API（应用程序接口），它们是直观的并且相互关联的。这就是tidyverse包，如果你愿意，你可以使用Hadley和其他人开发的R包大家庭像ggplot2，dplyr，tidyr，lubridate，stringr等。（译者注：因为Hadley Wickham和他的合作者们这些年创建了一系列数据整理和可视化的R包，这些包被坊间称为Hadley次元，即Hadleyverse，为避免个人崇拜嫌疑，后来被Hadley改为tidyverse，极乐净土，意思是让一团浆糊的数据变得干净整洁，方便探索、可视化和统计建模，关于什么是“干净的数据”，可参考他的论文“Tidy Data”）

此外我们还专注于帮助人们交流他们在R中做什么。比如R Markdown主要用来从R中创建文档和网页内容，Shiny则是使用R创建交互式应用程序。

未来我们将继续沿着这三个方向迈进，致力于让我们所有的开源产品和R包精益求精。我们也将继续深入了解大规模部署R的公司的需求，无论是尝试实现高性能，确保稳健安全性，还是与其它企业软件系统无缝集成。随着我们继续深入学习，我们将继续沿着这个方向开发产品。虽然我们已经解决了一些问题，但还有很多问题亟待解决，我们能做的还有很多。构建我们的专业服务器产品线也是一个重点，构建托管产品，让人们在云中访问和使用R。

另外，我们想把我们已有的知识教给更多的人。因此，我们正在努力创建一个全面的课程，人们可以通过不同的媒体，包括书籍、视频、网站和交互式定制进度教程来学习。以后我们会在教育方面投入更多的精力。

<span style="color: #000080;"><strong>JBR</strong><strong>：到目前为止，从您所说的，</strong><strong>RStudio</strong><strong>项目似乎都与生产工具有关，以帮助他人开发</strong><strong>R</strong><strong>软件和进行分析工作，但一个完整的</strong><strong>R</strong><strong>基础工具链是什么样的呢？</strong></span>

**J.J：**我认为我们一直在谈论的，比如帮助大规模部署R这些我们传统上关注的事情是宏观工具。他们是非常非常有用的。但实际上还有另一层我们并没有谈到的工具。在任何给定的应用程序领域中，我们都会希望有一套特定于该领域的微观工具。这虽然是极其重要的，但我们的角色多是这些工具的协助者，而不是创作者，因为我们并不是领域专家。

随着时间的推移，我认为整个R社区正在从事一个非常大的集体项目，以建立所有必要的工具，让人们分析不同领域的数据。我们正在做的一些工作就侧重于实现这一点。例如，Hadley正试图创建工具，并教人们如何为R构建自己的优秀工具，结果已经有很多人开发了一些精彩的软件包，让特定类型的数据分析变得更便捷。我在Rcpp上所做的工作就是让人们能够在自己领域内获得最高的性能，无论是快速读取数据还是快速分析，还是优化某些算法。此外，我们在数据可视化方面开发的许多工具都是提供可扩展平台，让人们为不同的域实现自定义的静态和交互式可视化。那么一个完整的工具链是什么样子的呢？我认为它的一部分是由我们构建的工具组成，其余的是由其他人在我们的基础上构建的工具组成。

<span style="color: #000080;"><strong>JBR</strong><strong>：</strong><strong>sparklyr</strong><strong>是</strong><strong>RStudio</strong><strong>的一个新方向，还是只是您描述的工具链的一部分？</strong></span>

**J.J .：**我认为这并不是一个新的方向。在2014年UCLA的UseR会议的特邀主题演讲中， John Chambers谈到了R的原始概念是创建一个接口语言。其中一个动机是，人们想使用强大并且高性能的FORTRAN库进行已有的统计分析，但他们希望用更灵活和交互的方式来使用它们。所以这个想法是创建一门擅长提供接口到其它计算系统的语言。刚开始时它是对接现有的FORTRAN代码，但随着时间的推移，它已经扩展到运行所有的东西。 R是一个非常好的接口语言。

John在他的演讲中提到了几个例子，一个是我已经谈到的Rcpp，另一个是H2O，它是一个用于进行机器学习的分布式计算系统。 H2O是用Java编写的，而不是R，但是开发人员提供了一个非常好的R接口。我认为几乎所有与统计学家或数据分析师相关的应用程序都可以用这个接口概念去做。如果它还没有在R中，你可以使用R创建一个流畅的和直观的接口。

这就是我们对sparklyr的看法。Spark提供了一系列人们想用的大数据功能，我们在R中创建了一个丰富的接口，所以当你使用Spark时，R中所有的工具和技术、工作环境和交流能力如R Markdown和Shiny都可以为你所用。John提到H2O，而R在很长时间里一直在做分布式处理的事情，所以我认为我们只是以最新和最大的分布式计算平台实现R的愿景和使命。

<span style="color: #000080;"><strong>JBR</strong><strong>：您怎么看待</strong><strong>R</strong><strong>和大数据？您认为</strong><strong>RStudio</strong><strong>做了什么有助于改进已发现的</strong><strong>R</strong><strong>的局限性？</strong></span>

**J.J.：**同样，你应该把R理解成一个用户接口，或者一种提供了很好的用户接口的语言。开发者并不在R中实现核心算法和核心分布式计算原语。他们把R作为与这些东西交互的接口。一旦人们理解了这一点，并且他们看到R有多棒，他们可以如何使用dplyr包和Spark集群交互，我认为他们就会灵光一现然后说：“好啦，我知道R适合哪些方面了。它是世界上用于数据分析的最佳交互式环境，现在我可以直接将R用于Spark。”

<span style="color: #000080;"><strong>JBR</strong><strong>：</strong><strong>RStudio</strong><strong>是语言联盟（</strong><strong>R consortium</strong><strong>）的白金创始会员，外界看来像是一个小公司的大担当？</strong></span>

**J.J.：**是的。

<span style="color: #000080;"><strong>JBR</strong><strong>：为什么</strong><strong>R</strong><strong>语言联盟很重要呢？您对它未来的希望是什么？您认为</strong><strong>R</strong><strong>语言联盟能实现些什么？</strong></span>

**J.J.：**R语言联盟有趣的地方在于它代表了R的所有利益相关者。最初的利益相关者是R Foundation和R的创始团队R core。那里有一整个使用和开发R包的社区，有好多围绕R开展各种业务的供应商。R语言联盟把所有的这些人联合在一起，说：“R变得越来越好与我们有很大关系。我们与这个系统的完善息息相关，所以让我们聚集在一起，可以商讨一些事情，资助对R社区有益的一些项目。”

R语言联盟是一个真正的意义深远且重要的群体。它有潜力成为R社区中每个人的连接点。这就是为什么我们对R语言联盟有如此大的热情，并且让RStudio的开发者花费大量的时间在上面。如果它运作良好，R语言联盟将作为R的中流砥柱，提供一个用于交流R的平台，让R变得更值得信赖。我们希望尽最大的可能来支持它。

<span style="color: #000080;"><strong>JBR</strong><strong>：除了支持</strong><strong>R</strong><strong>社区，似乎</strong><strong>RStudio</strong><strong>包是面向可重复的研究和改进一般的科学研究。请问您对科学本身有具体的目标或愿望吗？</strong></span>

**J.J.：**科学中关于可再现研究我们可以做的还有很多。可重复的研究关乎你所做的工作的真实性。事实上，人们依赖科学软件做一些非常重要的决定，以究天人之际、通古今之变。软件产生结果的过程的真实性和可信度是至关重要的。

我们的目标是确保在R生态系统内可重复工作的工具的可靠性。在过去，人们可能觉得重复性工作需要更多的工作、付出更多的努力，并认为“我没有时间这样做”。我们正在努力使可重现的工作变得比传统工作方式更简单。基于这个想法，我们提供了一个完整的工具链让人们撰写优雅而可靠的数据分析文档，而且无需作者投入额外的精力，这些文档自然而然就是可重复的。

此外，可重复性是我们专注于教人们如何编写和使用代码进行数据分析的原因之一。我们没有投入精力开发数据分析的图形界面工具，因为基于图形界面的操作不可重现，不容易检查，不容易共享，也不容易自动化。我们专注于代码。这是一个核心原则，无论如何，我们宁愿让代码更容易运行，而不是试图消除它。

<span style="color: #000080;"><strong>JBR</strong><strong>：对于初次接触</strong><strong>R</strong><strong>的人，您有什么建议吗？无论是学生、经验丰富的统计学家还是研究人员？</strong></span>

**J.J.：**我会建议他们练习一下Hadley Wickham和Garrett Grolemund在“R for Data Science”这本书中的写的R代码。这本书详细说明了在R中处理数据的tidyverse和基本原则。R中有很多很好的工具，但并不是每个用R的人都能立马找到这些工具。这正是我们试图改变的。我还建议R的新手仔细看看我们在RStudio开发的所有工具和包。

此外，当你有问题或遇到问题千万不要放弃。在StackOverflow和其它地方有很多很有用的关于R的信息，如果你仔细看它们的话，你有机会找到你的问题的答案。

<span style="color: #000080;"><strong>JBR：</strong><strong>您认为统计学家和数据科学家大体上应该知道哪些关于计算机科学的知识呢？</strong></span>

**J.J.：**这是个有趣的问题。许多关于R的最普遍的看法和思考都围绕着Bo Cowgill那著名的言论：“R最好的地方在于它是由统计学家编写的，R最糟的地方也在于它是由统计学家编写的。”然而事实上，R的开发者们对编程和计算机科学相当了解。他们的目标一直都是提供一个让掌握很少的计算机科学知识的人能实现她想法的表达式语言。R努力提供一种接口和语法，使得不懂计算机科学的人也可以使用R做一些复杂的数据分析。

我认为总会存在一些不能用高级的指令解决的问题。所以学习基本的编程原则，做一些简单的计算或者文本分析和语法分析这之类的事是有用的，但是R的重点还是不强迫每个人都成为计算机科学家。

<span style="color: #000080;"><strong>JBR</strong></span>**<span style="color: #000080;">：最后一个问题：您认为</span>**<span style="color: #000080;"><strong>R</strong><strong>和</strong><strong>RStudio</strong><strong>十年后将会应用在哪里呢？</strong></span>

**<span style="color: #000000;">J.J.：</span>**目前，R在大学中已经很受重视。它被教授给学生和研究人员，越来越成为核心课程的一部分，然而在业界仍有很多人在使用不如R性能好、灵活且效率高的专业软件。

我希望在接下里的十年中，我们能看到R现今在大学中占有的优势能真正地占领专业统计学家的世界。我对此充满了希望，而且我希望RStudio能在促进R积极转型中起到重要的作用。我们继续致力于使R构建得更容易学习和使用。这样，当一些机构决定长期使用R代替他们现在的专业统计软件时，他们会进入一个非常完善、非常强大、很容易学习的环境。所以他们可以成功地采取行动大规模应用R。我希望接下来的十年中RStudio可以促进完成所有的这些事情。

**JBR：**谢谢你，J.J.!

<p style="text-align: right;">
  翻译：王佳<br /> 审校：谢益辉、王小宁<br /> 编辑：丁维悦
</p><section class=""> <section class="">版权公告</section> </section> <section class=""> <section class=""> <section class="">原创文章，版权所有。</section> <section class=""></section> <section class=""></section> 

敬告各位友媒，如需转载，请与统计之都小编联系（直接留言或发至邮箱：editor@cos.name ），获准转载的请在显著位置注明作者和出处（转载自：统计之都），并在文章结尾处附上统计之都二维码。</section> </section>