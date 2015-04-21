
## 1. 微服务概念
### Small, and Focused on Doing One Thing Well
microservices. This is reinforced by Robert C. Martin’s definition of the Single Responsibility Principle, which states “Gather together those things that change for the same reason, and separate those things that change for different reasons.”


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
