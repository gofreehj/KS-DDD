# 上下文映射
```md
康威（梅尔·康威）定律：
任何组织在设计一套系统（广义概念上的系统）时，所交付的设计方案在结构上都与该组织的沟通结构保持一致。
界限上下文是分而治之架构原则的体现。
```
```md
领域驱动设计通过上下文映射来表达限界上下文之间的协作关系。
两个限界上下文之间的关系是有方向的。
```
```md
上下文映射模式分为两大类：团队协作模式和通信集成模式。
前者对应的是团队合作的工作边界，后者对应技术实现的应用边界。
```
```md
通过上下文映射关系，我们明确的限制了限界上下文的耦合性，
无论是上下文内部交互（合作关系）还是与外部上下文交互（防腐层），耦合度都限定在数据耦合（Data Coupling）的层级。
```
## Context Map通过下面几种方式表征界限上下文之间的关系：
* 共享内核-Shared Kernel
```md
当不同团队开发一些紧密相关的应用程序时，团队之间需要进行协调，
通常可以将两个团队共享的子集剥离出来形成共享内核（Shared Kernel），双方进行持续集成（Continuous Integration）。
共享内核（Shared Kernel）是业务领域中公共的部分，同时也是团队间容易达成且必须达成共识的领域部分。
```
* 客户/供应商-Customer/Supplier
```md
不同系统之间存在依赖关系时，下游系统依赖上游系统，下游系统是客户，上游系统是供应商，双方协定好需求，
由上游系统完成模型的构建和开发，并交付给下游系统使用，之后进行联调、测试。
这种模式建立在团队之间友好合作和支持的情况下。
```
```md
当两个具有上游/下游关系的团队不归同一个管理者指挥时，Customer/Supplier这样的合作模式就不会奏效。
勉强应用这种模式会给下游团队带来麻烦。
```
* 追随者-Conformist
```md
当两个开发团队具有上/下游关系时，如果上游团队没有动机来满足下游团队的需求，那么下游团队将无能为力。
出于利他主义的考虑，上游开发人员可能会做出承诺，但他们可能不会履行承诺。
下游团队出于良好的意愿会相信这些承诺，从而根据一些永远不会实现的特性来制定计划。
下游项目只能被搁置．直到团队最终学会利用现有条件自力更生为止。下游团队不会得到根据他们的需求而量身定做的接口。
```
```md
这时候“客户/供应商”模式就不凑效了，那么下游系统只能去追随上游系统，下游系统严格遵从上游系统的模型，简化集成。
```
```md
通过严格遵从上游团队的模型，可以消除在 BC之间进行转换的复杂性。
尽管这会限制下游设计人员的风格，而且可能不会得到理想的应用程序模型，但选择 Conformist模式可以极大地简化集成。
此外，这样还可以与供应商团队共享一种 UL。供应商处于驾驶者的位置上，因此最好使他们能够容易沟通。
```
* 防腐层-Anticorruption Layer
```md
前面介绍了在两个BC之间集成时可以进行的各种合作，从高度合作的 Shared Kernel模式或 
Customer/Supplier Team到单方面的Conformist模式。
如果是一种更悲观的关系，假设一个团队既不可能与另一个团队合作也无法利用他们的设计时，该如何应对。
```
```md
这时候我们需要使用防腐层（Anticorruption Layer）模式将上游系统的影响降低。
```
* 公开主机服务-Open Host Service
```md
当一个子系统必须与大量其他系统进行集成时，为每个集成都定制一个转换层可能会减慢团队的工作速度。
如果一个子系统有某种内聚性，那么或许可以把它描述为一组 Service,这组 Service满足了其他子系统的公共需求。
```
```md
公开主机服务（Open Host Service）能够允许系统将一组Service公开出去公其他系统访问。
定义一个协议，把你的子系统作为一组 Service供其他系统访问。
开放这个协议，以便所有需要与你的子系统集成的人都可以使用它。
当有新的集成需求时，就增强并扩展这个协议，但个别团队的特殊需求除外。
```
* 各行其道-Separate Way
```md
当两个系统之间的关系并非必不可少时，两者完全可以彼此独立，各自独立建模，独立发展，互不影响。
```
## 限界上下文之间的映射关系
```md
合作关系（Partnership）：两个上下文紧密合作的关系，一荣俱荣，一损俱损。
共享内核（Shared Kernel）：两个上下文依赖部分共享的模型。
客户方-供应方开发（Customer-Supplier Development）：上下文之间有组织的上下游依赖。
遵奉者（Conformist）：下游上下文只能盲目依赖上游上下文。
防腐层（Anticorruption Layer）：一个上下文通过一些适配和转换与另一个上下文交互。
开放主机服务（Open Host Service）：定义一种协议来让其他上下文来对本上下文进行访问。
发布语言（Published Language）：通常与OHS一起使用，用于定义开放主机的协议。
大泥球（Big Ball of Mud）：混杂在一起的上下文关系，边界不清晰。
另谋他路（SeparateWay）：两个完全没有任何联系的上下文。
```