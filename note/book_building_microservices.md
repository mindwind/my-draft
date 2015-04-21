

## 微服务建模
I called this onion architecture, as it had lots of layers and made me cry when we had to cut through it.
洋葱架构模式，一层又一层的强耦合，重构像像切洋葱一样让人想哭


## 微服务协作

### 微服务协作模式
Orchestration Versus Choreography
With orchestration, we rely on a central brain to guide and drive the process, much like the conductor in an orchestra. With choreography, we inform each part of the system of its job, and let it work out the details, like dancers all finding their way and reacting to others around them in a ballet.

选择乐队模式（有一个中心指挥），还是舞蹈方式（事件响应模式）
乐队模式存在中心的 God Service，容易形成强耦合，但更有利于监控整个业务流程
舞蹈模式，服务更自治，更松耦合，但无法直观反应业务流。
中心化和去中心化的选择？？
