---
date      : 2016-09-30
---


## 0. 前言 & 序
Hacker: Someone who loves to program and enjoys being clever about it.
    -- 《自由软件杂志》

设想你在参加一个会议。或许你在想，这个会议没完没了，你还不如去写程序。而 Dave 和 Andy 会想，他们为什么在开会，他们想知道是否可以通过另外的方式取代会议。开会并非是某种使他们远离编程的事情。开会就是编程，并且是能够加以改善的编程。
这正是本书美之所在：它体现它的哲学，以如此谦逊的方式。本书的哲学将渗入你的意识，并与你自己的哲学交融在一起。它不鼓吹，它只是讲述什么可行。但在讲述中却又有更多的东西到临，我们有时称之为「无名的品质」（Quality without a name）
    -- Ward Cunningham

作为程序员，你既是倾听者，又是顾问；既是解释者，又是发号施令者。你设法捕捉难以捉摸的需求，并找到表达它们的方式，让一台纯粹的机器能够合理的处理它们。
注重实效的程序员不仅要完成工作，而且要完成得漂亮。
尽管你现在的工作也许只要求你成为某方面的专才，你却总是能够转向新的领域和新的挑战。

提示 1
Care About Your Craft
关心你的技艺

提示 2
Think! About Your Work
思考！你的工作


## 第 1 章：注重实效的哲学  A Pragmatic Philosophy

### 1. 我的源码让猫给吃了
> 承认错误，担负责任

在所有弱点中，最大的弱点就是害怕暴露弱点。
    -- J. B. Bossuet, Politics from Holy Writ, 1709
> 专家也不必害怕暴露自己的无知

提示 3
Provide Options, Don't Make Lame Excuses
提供各种选择，不要找蹩脚的借口


### 2. 软件的熵
> 控制熵增是软件演化的本质

「熵」是一个来自物理学的概念，指的是某个系统中的「无序」的总量

提示 4
Don't Live with Broken Windows
不要容忍破窗户

### 3. 石头汤与煮青蛙
> 在更高的维度让正确的事情发生

提示 5
Be a Catalyst for Change
做变化的催化剂

提示 6
Remember the Big Picture
记住大图景

留心大图景，要持续不断地观察周围发生的事情，而不只是你自己在做的事情。

### 4. 足够好的软件
> 先完成再完美，及时止步

提示 7
Make Quality a Requirements Issue
使质量成为需求问题


## 第 2 章：注重实效的途径  A Pragmatic Approach

### 7. 重复的危害
> DRY，让复用变得容易

系统中的每一项知识都必须具有单一、无歧义、权威的表示。
代码为什么需要注释：糟糕的代码才需要许多注释。
DRY 法则告诉我们，要把低级的知识放在代码中；把注释保留给其他的高级说明。

提示 11
DRY - Don't Repeat Yourself
不要重复你自己

提示 12
Make It Easy to Reuse
让复用变得容易


### 8. 正交性
> 微服务化架构实际强化了正交性

「正交性」是从几何学中借来的术语。如果两条直线相交成直角它们就是正交的，用向量术语说，这两条直线互不依赖。
在计算机书中，该术语用于表示某种不相依赖性或是解耦性。如果两个或更多事物中的一个发生变化，不会影响其他事物。

提示 13
Eliminate Effects Between Unrelated Things
消除无关事物之间的影响

如果你编写正交的系统，你得到两个主要好处：提高生产率与降低风险。
你可以对项目团队的正交性进行非正式衡量，只要看一看，在讨论每个所需改动时需要涉及多少人。人数越多，团队的正交性就越差。
不要依赖你无法控制的事物属性。


### 9. 可撤销性
> 计划没有变化快

管理人员往往与工程师趣味相投：单一、容易的答案正好可以放在电子表格和项目计划中。
要把决策视为是写在沙滩上的，而不要把它们刻在石头上。大浪随时可能到来，把它们抹去。

提示 14
There Are No Final Decisions
不存在最终决策

### 10. 曳光弹
> 快速集成和迭代的开发方式，更好的可见性

曳光弹与常规弹药交错着装在弹药袋上。发射时，曳光弹中的磷点燃，在枪与它们击中的地方之间留下一条烟火般的踪迹。如果曳光弹击中目标，那么常规子弹也会击中目标。

提示 15
Use Tracer Bullets to Find the Target
用曳光弹找到目标


## 第 3 章：基本工具  The Basic tools
工具放大你的才干。你的工具越好，你越是能更好地掌握它们的用法，你的生产力就越高。
要与工匠一样，想着定期增添工具，要总是寻找更好的做事方式。

### 14. 纯文本的威力
> 性能和空间敏感的应用例外

大多数二进制格式的问题在于，理解数据所必需的语境与数据本身是分离的。你人为地使数据与其含义脱离开来。
通过纯文本你可以获得自描述的、不依赖于创建它的应用的数据流。

提示 20
Keep Knowledge in Plain Text
用纯文本保存知识

### 15. shell 游戏
> 初期学习的高成本需要在高频使用中来摊销

提示 21
Use the Power of Command Shells
利用 shell 命令的力量

### 16. 强力编辑
> 编辑器的选择是一种个人信仰问题。

提示 22
Use a Single Editor Well
用好一种编辑器

### 17. 源码控制
> 这已是一个常识

提示 23
Always Use Source Code Control
总是使用源码控制

### 18. 调试
>

提示 24
Fix the Problem, Not the Blame
要修正问题，而不是发出指责

提示 25
Don't Panic
不要恐慌

在向他人解释问题时，你必须明确的陈述那些你在自己检查代码时想当然的事情。
因为必须详细描述这些假定中的一部分，你可能会突然获得对问题的新洞见。

提示 26
"Select" Isn't Broken
"Select" 没有问题
> Select 是一个系统接口，这里指不要先怀疑库代码而是先怀疑自己

bug 有可能存在于 OS、编译器、或是第三方产品中——但这不应该是你的第一想法。
有大得多的可能性是 bug 存在于正在开发的应用代码中。
与假定库本身除了问题相比，假定应用代码对库的调用不正确通常更有好处。

提示 27
Don't Assume it - Prove It
不要假定，要证明。

## 第 4 章：注重实效的偏执  Pragmatic Paranoia
提示 30
You Can't Write Perfect Software
你不可能写出完美的软件

这刺痛了你？

### 21. 按合约设计
> 如今的微服务难道不是这样一种实践么？十多年前就在本书里写下来了，还是读书少啊。

合约即规定你的权利与责任，也规定对方的权利与责任。此外，还有关于任何一方没有遵守合约的后果的约定。

提示 31
Design with Contracts
通过合约进行设计

Liskov 替换原则：子类必须要能通过基类的接口使用，而使用者无须知道其区别。


### 22. 死程序不说谎
> 最怕要死不活的僵尸程序

提示 32
Crash Early
早崩溃

有许多时候，让你的程序崩溃是你的最佳选择。


### 23. 断言式编程
> 养成自检式编程习惯

提示 33
If It Can't Happen, Use Assertions to Ensure That It Won't
如果它不可能发生，用断言确保它不会发生

现实的情况是，对于任何复杂的程序，你甚至不大可能测试你的代码执行路径的排列数的极小一部分。


## 第 5 章：弯曲，或折断  Bend, or Break

### 26. 解耦与得墨忒耳法则
> 反范式设计需要权衡

提示 36
Minimize Coupling Between Modules
使模块之间的耦合减至最少

与任何技术一样，你必须平衡你的特定应用的各种正面因素和负面因素。
在数据库 schema 设计中，常常会为了改善性能而对 schema 进行「反规范化」：违反规范化规则，以换取速度。


### 27. 元程序设计
> 今天这已经是常识

提示 37
Configure, Don't Integrate
要配置，不要集成

提示 38
Put Abstractions in Code, Details in Metadata
将抽象放进代码，细节放进元数据


## 第 6 章：当你编码时  While You Are Coding

### 31. 靠巧合编程
> 新手爱犯的错误，对于老手，有时大脑会欺骗你，你认为的事实有可能是假定

提示 44
Don't Program by Coincidence
不要靠巧合编程

不要只是测试你的代码，还要测试你的假定。不要猜测，要实际尝试它。


### 32. 算法速率
> 运行时测算去验证开发时的估算

提示 45
Estimate the Order of Your Algorithms
估算你的算法的阶

提示 46
Test Your Estimates
测试你的估算


## 第 7 章：在项目开始之前  Before The Project

### 36. 需求之坑
> 考虑原因而非方式

完美，不是在没有什么需要增加，而是在没有什么需要去掉时达到的。
    -- Antoine de St. Exupery, _Wind, Sand, and Stars_, 1939

需求很少存在于表面上，通常，它们深深地埋藏在层层假定、误解和政治手段的下面。

提示 51
Don't Gather Requirements - Dig for Them
不要搜集需求——挖掘它们

找出用户为何要做特定事情的原因，而不只是他们目前做这件事情的方式。
> 用户通常提需求都是告诉你他想要的形式，而非原因。例如：给我一张这样报表、这里需要加个列表，我需要像这个 APP 功能一样的东西。

提示 52
Work with a User to Think Like a User
与用户一同工作，以像用户一样思考

提示 53
Abstractions Live Longer than Details
抽象比细节活得更长久

制作需求文档的一大危险是太过具体，好的需求文档会保持抽象。

提示 54
User a Project Glossary
使用项目词汇表


### 37. 解开不可能解开的谜题
> 发散性思维

提示 55
Don't Think Outside the Box - Find the Box
不要在盒子外面思考——要找到盒子


### 38. 等你准备好
> 心有疑虑，切勿躁动

提示 56
Listen to Nagging Doubts - Start When You're Ready
倾听反复出现的疑虑——等你准备好再开始


## 第 8 章：注重实效的项目  Pragmatic Projects

### 41. 注重实效的团队
> 建立团队文化

提示 60
Organize Around Functionality, Not Job Functions
围绕功能、而不是工作职务进行组织

项目至少需要两个「头」—— 一个主管技术，另一个主管行政。
技术主管设定开发哲学和风格，给各团队指派责任，并仲裁成员之间不可避免的「讨论」。
技术主管还要不断关注大图景，设法找出团队之间任何不必要的，可能降低总体正交性的交叉。
行政主管或项目经理调度各团队所需要的各种资源，监视并报告进展情况，并根据商业需要帮助确定各种优先级。
与外界交流时，行政主管还要充当团队的大使。

### 42. 无处不在的自动化
> 自动化习惯是优秀程序员的属性体现

文明通过增加我们不假思索就能完成的重要操作的数目而取得进步。
    -- 阿尔弗雷德·诺斯·怀特海

提示 61
Don't Use Manual Procedures
不要使用手工流程

### 43. 无情的测试
> 拥有完整的测试思维框架才能写出更好的程序

提示 62
Test Early. Test Often. Test Automatically.
早测试，常测试，自动测试

提示 63
Coding Ain't Done 'Til All the Tests Run
要通过全部测试，编码才算完成

提示 64
Use Saboteurs to Test Your Testing
通过“蓄意破坏者”测试你的测试

提示 65
Test State Coverage, Not Code Coverage
测试状态覆盖，而不是代码覆盖

提示 66
Find Bugs Once
一个 bug 只抓一次

一旦测试人员找到了某个 bug，这应该是测试人员最后一次发现这个 bug。
应该对自动化测试进行修改，从此每次都检查那个特定的 bug，没有例外。

dead-line: 在监狱里或监狱周围划出的一条线，犯人一旦越过，就有遭到枪击的危险。
    -- 韦伯斯特大学词典
