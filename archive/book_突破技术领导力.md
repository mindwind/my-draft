# 突破技术领导力
2018-01-16

--------------------------------------------------------------------------------


## 何时选择切分你的服务
__修改频率__  
如果某个服务需要在大型代码库上进行频繁修改，通常这会引起代 码资源的竞争，并且会浪费一部分时间去解决不同团队之间的产品合并的冲突。这样 高频变化的服务应该被切分成细粒度的服务，并且被安置在自己独立的泳道，这样的话即便频繁更新也不会影响彼此的服务。而低频变化的服务应该被合并起来，因 为即便分离这种服务也没有任何价值，而且在更新这些服务也几乎没有什么风险。

__复用程度__  
如果库或者服务在整个产品中有很高程度的复用，应该考虑去将它们剥离开，将其中专门针对某个功能或服务的代码分离。这样服务就可以在编译时链接，部署时作为一个共享的动态可加载库或者直接作为一个独立的运行时服务。

__团队规模__  
小而精的团队可以胜任处理功能独立且高频变化的微服务，或者是非常多功能但低频变化的服务。这会给他们更好的归属感，增加专业化程度，让他们自主工作。另外团队的规模也决定了是否应该切分服务。越大的团队的协调成本也会更高，也就越需要切分团队来减少代码库的冲突。在这种情况下，我们会基于缩小团队规模这个因素来进行切分产品，以减少冲突。而理想的切分是基于增加可用性、可扩展性、减少需求的开发时间来拆分。


__专业化的技能__  
一些服务可能需要一些和其他团队不一样的特殊的开发技能。


## 制造还是购买
  1. 这个“事物”(产品/架构组件/功能)是否在我们的业务中创造战略上的差异
     这个问题的答案是“不 - 它不会产生竞争优势”，那么99%的时间你应该停下来，试图 找到一个打包的产品，开源的解决方案，或外包供应商来构建你所需要的。

  2. 我们是否是创造这个“事物”最合适的公司（团队）?
     这个问题有助于通知您是否可以有效地构建它并实现所需的价值。

  3. 你想要制造的“事物”，是不是只有很少的，甚至没有竞品?

  4. 我们能够有效的控制成本了制造这个“事物”?
