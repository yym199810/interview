**1.Diff**
> diff算法早就存在，计算将一棵树转换为另一棵树的最少操作，需要循环递归对节点进行对比。

> 算法复杂度 O(n^3)，非常消耗性能

**2.react Diff**
> virtual DOM + diff  

> 复杂度变为 O(n)

2.1 diff 策略
- webUI 中DOM节点跨层级的移动特别少 可以忽略不计
- 相同类的组件将会生成相似的树型结构、不同类的组件将会生成不同的树型结构
- 对于同一层级的一组子节点，可以通过唯一id进行区分

2.2 根据策略进行优化
- tree diff
- component diff
- element diff

> tree diff
  >> 基于策略一（webUI中DOM节点的跨层级移动较少可以忽略不计），对树进行分层比较，只比较同一层的节点。
  当发现节点不在了，会将其和其子节点会被完全删除，不用再比较了，这样只进行了一次比较，就完成了整个
  DOM的比较。
  >> ![tu](https://pic1.zhimg.com/80/0c08dbb6b1e0745780de4d208ad51d34_1440w.png)

  >> 那么问题来了，如果出现了跨层级移动怎么办？
  如下：A节点从根节点R下移动到了D节点下，此时在React中是新创建了A节点，然后删除之前的A节点。
  过程：createA->createB->createC->deleteA
  由此可见，当跨层级移动时并不是移动，而是创建操作。这会影响react性能，因此不建议进行DOM节点跨层级的移动。

> component diff
- 如果是同一类型的组件，按照原策略继续比较virtua DOM tree
- 如果不是，则该组件被判定为dirty component，从而替换整个组件下的子节点
- 对于同一类型的组件，有可能其virtualDOM 没有发生任何改变，如果知道这一点可以节省大量的diff运算时间
  因此react通过shouldComponentUpdate()判断该组件是否需要进行diff。

  如下：D被替换成了G，即使组件D和G结构相似，但是也会创建组件G和子节点，然后删除组件D和其子节点
  ![tu](https://pic1.zhimg.com/80/52654992aba15fc90e2dac8b2387d0c4_1440w.png)

> element diff
  当节点处于同一层级时，react diff提供了三种节点操作：插入、移动、删除
  - 插入：新的component不在老的集合里，即所有节点全是新的，需要对节点进行插入操作
  - 移动：在老的集合里有新component类型，且element是可更新的类型，就需要进行移动操作可以复用之前的DOM节点
  - 删除：老的component在新的集合里也有，但对应的element不同则不能更新复用需要进行删除操作。 或老的component在新的集合中不存在
>> 提出问题
   ![tu](https://pic2.zhimg.com/80/7541670c089b84c59b84e9438e92a8e9_1440w.png)
    如上图，新集合和老集合进行diff比较时：B!=A 则会创建一个B 然后删除老集合的A，以此类推创建并插入A、D、C，然后删除B、C、D
   
   这些都是相同的节点，只是因为移动，需要进行繁杂低效率的创建和删除，其实只要对节点进行移动即可
>> 解决问题
  react允许 对同一层级的同组子节点，添加唯一key进行区分。
  ![tu](https://pic4.zhimg.com/80/c0aa97d996de5e7f1069e97ca3accfeb_1440w.png)   
  通过key发现新老集合中的节点都是相同的节点，只需将老集合中的节点移动位置，更新为新集合中节点的位置。
  此时react的diff：只移动A和D节点，B和C保持不动

