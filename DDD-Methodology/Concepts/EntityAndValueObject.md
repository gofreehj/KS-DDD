# 实体(Entity) & 值对象(Value Object)

实体不仅需要知道它是什么？而且还需要知道它是哪个？而值对象只需要知道它是什么？

## 实体

许多对象不是由它们的属性来定义，而是通过一系列的连续性（continuity）和标识（identity）来从根本上定义的。
只要一个对象在生命周期中能够保持连续性，并且独立于它的属性（即使这些属性对系统用户非常重要），那它就是一个实体。

当一个对象由其标识（而不是属性）区分时，这种对象称为实体（Entity）。
例：最简单的，公安系统的身份信息录入，对于人的模拟，即认为是实体，因为每个人是独一无二的，且其具有唯一标识（如公安系统分发的身份证号码）。

在实践上建议将属性的验证放到实体中。

## 值对象

当你只关心某个对象的属性时，该对象便可作为一个值对象。为其添加有意义的属性，并赋予它相应的行为。
我们需要将值对象看成不变对象，不要给它任何身份标识，还应该尽量避免像实体对象一样的复杂性。

实体对象相对容易理解，我们常见的类的都可以看成是实体对象。
值对象在DDD中相对而言是难以理解并且容易误用的。

当一个对象用于对事务进行描述而没有唯一标识时，它被称作值对象（Value Object）。
例：比如颜色信息，我们只需要知道{“name”:“黑色”，”css”:“#000000”}这样的值信息就能够满足要求了，这避免了我们对标识追踪带来的系统复杂性。

值对象很重要，在习惯了使用数据库的数据建模后，很容易将所有对象看作实体。使用值对象，可以更好地做系统优化、精简设计。
它具有不变性、相等性和可替换性。

在实践中，需要保证值对象创建后就不能被修改，即不允许外部再修改其属性。
在不同上下文集成时，会出现模型概念的公用，如商品模型会存在于电商的各个上下文中。
在订单上下文中如果你只关注下单时商品信息快照，那么将商品对象视为值对象是很好的选择。

### 为什么需要使用值对象

书中给了一个解释：使用不变的值对象使得我们做更少的职责假设

使用值对象在不同的BC中进行数据交换，可以避免不同BC对实体对象的状态变更而引发的数据依赖关系，实现最小化的集成。
值类型用于度量和描述事物，DDD中建议应尽量使用值对象来建模而不是实体对象，
因为值对象非常容易地对值对象进行创建、测试、使用、优化和维护。

### 谨慎使用值对象

在实践中，我们发现虽然一些领域对象符合值对象的概念，但是随着业务的变动，很多原有的定义会发生变更，
值对象可能需要在业务意义具有唯一标识，而对这类值对象的重构往往需要较高成本。
因此在特定的情况下，我们也要根据实际情况来权衡领域对象的选型。

