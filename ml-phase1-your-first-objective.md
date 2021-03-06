
# 你的第一个优化目标

你手上有很多关于自己系统的指标，但是你的机器学习系统总是只有一个**优化目标，一个你的系统"努力尝试"去优化的值。** 这里我对指标和优化目标做一个区分：**指标是你系统产出的任何值**，有些重要有些则不重要。参见 Rule #2。

## Rule 12 - 不要过度思考选择哪些指标直接优化

你想赚钱，让用户高兴，想让世界更美好。有大量的指标需要你去考量（见 Rule #2)。但是，在机器学习系统的早期，你会发现他们一起涨了，包括那些你没有直接去优化的指标。比如，你比较在意点击量，停留时长，和 DAU（日活跃用户量）。如果你去优化点击量，很可能你会发现停留时长跟着一起涨。所以，当轻易就能同时优化多指标时候，不用特别费心思去选择指标。当然，也不能太过了：**如果你发现直接指标涨了，但是还没发上线，那么就应该重新 review 一下自己的优化目标了。**

> Eric: 这个有点像我们搞搜索推荐，有的时候点击导流率涨了，但是人工质量评估没有通过。

## Rule 13 - 第一次选一个简单，可视，有归属感的指标作为你的优化目标

有时候你并不知道真正的优化目标是啥。你以为你知道，但是当你盯着数据，并排和老系统进行对比时候，能发现需要调整自己的优化目标。更有甚者，团队的不同成员可能在优化目标选择上不能达成一致。机器学习的优化目标应该简单，并且在某种程度上代表"真实"目标。所以，选一个简单的机器学习优化目标，然后尝试在其上加一个"政策层"（人工规则层），这样可以使得自己可以调整最终的排序。

可以直接度量的用户行为，比较容易哪来建模：

1. 排序链接被点击了吗？
2. 排序实体被下载了吗？
3. 排序实体被 转发/回复/邮件分享了吗？
4. 排序实体被评分了吗？
5. 展示实体被标记为垃圾/色情/冒犯了吗？

避免去建模那些不直接的东西：

1. 用户第二天访问了吗？
2. 用户访问网站多长时间？
3. DAU 的数量是多少？

这些不直接的指标很好，可以在 A/B test 的时候多关注，并且拿来做最终上线的决策参考。（但是不要直接哪来优化）
总之，不要让机器学习试图解决下面的问题：

1. 用户使用这个产品开心吗？
2. 用户体验还满意吗？
3. 产品增加了用户的幸福感吗？
4. 产品对公司的总体健康度有多大的影响？

 这些东西都很重要，但是也很难（去优化）。相反，用一些替代品：如果用户开心，那么他们就会在网站多停留。如果用户满意，他们明天也会来。只要大家还在关心用户福祉和公司健康度，人们就会去把机器学习的优化目标和这些东西一起联合起来进行考量，所以不必局限在[这里](https://www.youtube.com/watch?v=bq2_wSsDwkQ)。

> Eric: 这个 youtube 视频没细看，还不知道这句啥意思.

## Rule 14 - 从一个可交互的模型开始 让查错更简单

[Linear regression 线性回归](https://en.wikipedia.org/wiki/Linear_regression), [logistic regression 逻辑回归](https://en.wikipedia.org/wiki/Logistic_regression), 和[Poisson regression 泊松回归](https://en.wikipedia.org/wiki/Poisson_regression)  直接由统计模型衍生出来。 每个预测都可以被解释成一个概率或者是期望值。 这就使得他们比那些试图直接优化分类准确率或者排序效果的模型（0-1 loss, 各种 hinge losses等等）更具可解释性。比如，如果训练集的概率值与测试集或者线上的概率值偏差太多，那么很可能哪里出问题了。

For example, in linear, logistic, or Poisson regression, **there are subsets of the data where the average predicted expectation equals the average label (1­moment calibrated, or just calibrated)<sup>3</sup>**. If you have a feature which is either 1 or 0 for each example, then the set of examples where that feature is 1 is calibrated. Also, if you have a feature that is 1 for every example, then the set of all examples is calibrated.

> Eric: 上面这段没太看懂，故先留着。

用简单模型，那么使得整个反馈循环 run 起来就比较简单（见 Rule #36）。通常，我们用概率预测来做出决策：比如用户按照用户点击的概率进行帖子的排序。**但是记住在选择模型时候，如何决策比模型的数据拟合效果更重要。(见 Rule #27）**

## Rule 15 - 在政策层 把垃圾过滤和质量排序区分对待

 质量排序是需要细细雕琢的艺术，而垃圾过滤就像打仗。你用来判断帖子质量的因素会对系统用户变得显而易见，他们会调整帖子以迎合你的算法。因此，你的质量排序策略应该专注于排序那些拥有"初心"的帖子。你不应该因为垃圾信息排到了前面而让质量排序系统效果打折。**同样地, "racy"的内容也应该同质量排序区分对待。** 垃圾过滤是另一个故事。为了对抗垃圾，你的特征应该不断变化，通常，会有一些显式的规则公布出来（比如如果一个帖子被3个人举报为垃圾，那么就不会再显示了等等）。反垃圾的机器学习模型至少要每天更新。发帖人的声誉也应该列为重要考量因素。

 在某种程度上，这两个系统的输出应该整合在一起。记住，搜索结果的垃圾过滤应该比垃圾邮件的过滤做得更激进。同时，在训练数据中去除垃圾也是通常的一个做法。

