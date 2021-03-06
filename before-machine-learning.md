# 在机器学习之前

## Rule 1 - 别怕推出一个没有使用机器学习的产品

机器学习很nb，但是得先有数据。理论上，你可以从其他问题那借一个现成的机器学习系统过来，然后改造模型用在新产品上，但是这种方法往往比直觉方法还要差。如果你觉得机器学习可以给你带来100%的提升，那么直觉方法往往会贡献50%。
> Eric: 的确50%都说少了，至少能到70%-80%吧。

举例来说，如果你在搞应用市场的app排名，你就可以使用安装率或者安装数来排序；如果你在搞垃圾消息检测，先过滤掉那些历史上发垃圾消息的源；如果你在搞内容排序，把最近使用的排到前面去（甚至按照字母排序）。如果你的系统并不是天生必须使用机器学习，那么在你有数据前就先别用他。

## Rule 2 - 首先，积累数据（Metrics)

 在形式化你的机器学习系统之前，尽量积累现有系统的数据。这么做有以下的原因：
 > Eric: 这里面理解 Metrics 还不仅仅是日志等原始数据，应该是带有 meta 信息的数据，就是原始的特征。

1. 在早期，要获得这些数据的使用许可相对容易.

  > Eric: 不但是使用许可，早期规划了，那么就会约定俗成的积累有价值的数据，比如系统日志。如果前期丢了，后边再补，往往就不全面，切因为系统已经成型而困难重重了

2. 如果你在设计系统之初就有保存数据的意识，那么以后就容易了。 你可不想日后为了搞清楚某个数字的意义在海量日志里各种 grep。

4. 你会发现随着系统演进，有些Metrics 变了，有些没变。 比如你想直接优化每日活跃用户数。你回顾发现，即使产品体验发生了翻天覆地的变化，这项指标也可能一直保持稳定。

  > 按：這段話有點繞口，簡單地說，你對於各種「操作 A 會不會影響 B」的掌握度變高，可以類比成所謂的 domain knowledge
  > Eric：应该就是从数据中人肉发现规律了. 数据积累的越早，那么这种经验就越多。

Google Plus team  衡量了 每个阅读的展开、分享、+1、评论；每个用户的f分享等信息. 这些是他们在线上用来计算一个 post 质量的指标。并且要注意，一个可以给用户分群，并且整合离线统计结果的实验框架也很重要。（参考 Rule 12）
 > Eric：除了线上的那些特征外，离线的基于统计的特征也很重要，记得积累。

 通过更自由广泛的收集指标，你就能够用更宽广的视野来审视你的系统。发现一个问题？增加一个指标来追踪他！对上次发布带来的客观改变很兴奋？加一个指标来追踪他！

## Rule 3 - 选择机器学习而非复杂的直觉

简单的经验方法可以让你产品走出家门。复杂的经验方法则难以维护。一旦你知道了自己的优化目标，并且积累了足够的数据，就转移到机器学习吧。因为在大多数的软件工程任务中，无论是基于经验的，还是基于机器学习的，你都想不断的优化他，而你会发现后者更容易更新和维护。(参考 Rule 16)

> 按：要注意，不管是從 heuristic 轉移到 ML，或是從一個 ML model 轉移到另一個 ML 都需要成本。

> 舉例來說：原本優化 metric A 的模型，其實對 B 也做得不錯（即使並沒有寫在需求裡面）

> 當你轉移到另一個模型，即使它對 A 優化地更好，卻在 B 作得不好，那使用者可能不會接受

> 追根究柢，因為人生就是這麼困難，每個人的工作要優化的目標通常是多個、並且多少有所差異

> 而機器學習（或這個功能）通常只優化其中一兩個目標而已
