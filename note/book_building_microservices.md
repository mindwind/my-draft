---
title     : Building Microservices 读书笔记
date      : 2015-04-21
---


## 1. Microservices
### 脉络
Microservices 定义
Microservices are small, autonomous services
  1. Small, and Focused on Doing One Thing Well
  2. Autonomous


Microservices 的优势
  1. Technology Heterogeneity  [技术多样性，对不同的业务场景选择最合适的技术]
  2. Resilience  [快速可恢复性]
  3. Scaling   [扩展性，不均匀的扩展]
  4. Ease of Deployment  [易部署性，仅仅部署受影响的服务]
  5. Organizational Alignment [人员组织架构的适应性，康威定律]
  6. Composability [可组合性]
  7. Optimizing for Replaceability [替换性]


SOA 和 Microservices 对比
Service-oriented architecture (SOA) is a design approach where multiple services collaborate to provide some end set of capabilities.
[SOA 是一种服务化架构方法论，而 Microservices 是一种具体实践该方法，类似 Unicode 和 UTF-8 的关系]


其他解耦合技术
1. Shared Libraries
   drawbacks [共享库的缺点]
     - lose true technology heterogeneity.
     - scale parts of system independently from each other is curtailed.
     - ability to deploy changes in isolation is reduced.
   Creating code for common tasks that aren’t specific to your business domain that you want to reuse across the organization
    [适合共享库的地方是业务领域无关的公共任务]

2. Modules
   They allow some lifecycle management of the modules, such that they can be deployed into a running process, allowing you to make changes without taking the whole process down, Like java OSGI, Erlang.
   [目前的动态模块化技术在实践中并未大规模采用，不够成熟。]


### 亮点
This is reinforced by Robert C. Martin’s definition of the Single Responsibility Principle, which states “Gather together those things that change for the same reason, and separate those things that change for different reasons.”

So you should instead think of microservices as a specific approach for SOA in the same way that XP or Scrum are specific approaches for Agile software development.

Having a process boundary separation does enforce clean hygiene in this respect (or at least makes it harder to do the wrong thing!).



## 2. 微服务架构进化
### An Evolutionary Vision for the Architect
To borrow a term from Frank Buschmann, architects have a duty to ensure that the system is habitable for developers too.

So our architects as town planners need to set direction in broad strokes, and only get involved in being highly specific about implementation detail in limited cases.


## Zoning
That means we need to spend time thinking about how our services talk to each other, or ensuring that we can properly monitor the overall health of our system.


### Strategic Goals & Principled Approach & Practice
If you’re the person defining the company’s technical vision, this may mean you’ll need to spend more time with the nontechnical parts of your organization

Rules are for the obedience of fools and the guidance of wise men.  -- Generally attributed to Douglas Bader
Making decisions in system design is all about trade-offs, and microservice architectures give us lots of trade-offs to make!


### Building a Team
With larger, monolithic systems, there are fewer opportunities for people to step up and own something. With microservices, on the other hand, we have multiple autonomous codebases that will have their own independent lifecycles. Helping people step up by having them take ownership of individual services before accepting more responsibility can be a great way to help them achieve their own career goals, and at the same time lightens the load on whoever is in charge!
微服务架构让服务帮助开发人员（服务拥有者）增强责任感，我的地盘我做主，有利于个人职业生涯发展。


## 3. 微服务建模
I called this onion architecture, as it had lots of layers and made me cry when we had to cut through it.
洋葱架构模式，一层又一层的强耦合，重构像像切洋葱一样让人想哭


## 4. 微服务协作

### Orchestration Versus Choreography
With orchestration, we rely on a central brain to guide and drive the process, much like the conductor in an orchestra. With choreography, we inform each part of the system of its job, and let it work out the details, like dancers all finding their way and reacting to others around them in a ballet.

选择乐队模式（有一个中心指挥），还是舞蹈方式（事件响应模式）
乐队模式存在中心的 God Service，容易形成强耦合，但更有利于监控整个业务流程
舞蹈模式，服务更自治，更松耦合，但无法直观反应业务流。
中心化和去中心化的选择？？
