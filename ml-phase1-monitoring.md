
# 监控

总的来说，建设好告警机制，比如建立 dashboard 并且让告警可以被处理。

## Rule 8 - 对系统的时效性需求了如指掌

如果你的系统1天没更新，效果会退化多少？一周呢？一个季度呢？这些可以用来帮助你理解监控的优先级。如果一天不更新会导致收入少10%，那么让一个工程师整天盯着系统也许就挺值得的。 大多数的在线广告系统每天要处理很多新的广告，每天更新是必须的。比如，如果 Google Play Search 的机器学习系统没有更新，那么一个月后，影响就会体现在收入上。服务于 Google Plus 的What's Hot业务的一些模型，没有 post identifiers(TODO),所以不能很频繁的 export 这些 model。（这句没有太懂）. 其他模型有 post identifier所以就能够比较频繁的更新。同时也要注意到，时效性需求也是会随着时间变化的，特别是模型的一些特征增删的时候。

## Rule 9 - 在发布模型之前就发现问题
> Eric：这里的发布模型，应该指的是用模型到线上去 predicting, 去真正服务。

很多模型最终被拿来服务线上。如果这个时候出问题，那就是用户可感知的问题。如果在此之前出问题，那就是在训练阶段的问题，不会对用户造成可感知的影响。
在发布模型之前做好健壮性检查。特别的，确保模型的性能okay。或者，如果你对数据还有一丝疑虑，就不要发布这个模型。 一些团队会在发布之前不断的检查模型的 [ROC 曲线](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) (or [AUC](http://stats.stackexchange.com/questions/132777/what-does-auc-stand-for-and-what-is-it)) 。**在线下发现的问题，也许一个邮件就能说明清楚，但是如果问题被带到先上去，也许就需要一个正式的网页（这里指bug 说明或者用户致歉信）去说明了。** 所以，在问题触达用户之前解决掉他。

## Rule 10 - 小心沉默的失败

 这种问题在机器学习系统里更容易发生。加入一个被 join 的 table 不再更新了，机器学习系统会自己调整，也许最终系统的行为也还算不错，只是缓慢退化。有时候，有的表几个月也没更新，一个简单的更新操作带来的提升也许比一个 Q 的其他上线都要大！比如，也许特征覆盖率因为实现变化而变了：比如原来覆盖90%样本的特征突然降低到60%。Google Play 原来有个表半年没更新了，更新了后发现安装率涨了2%。如果你跟踪数据的统计值，同时偶尔的手动检查下数据，那么你就能避免这类问题。

## Rule 11 - 给特征指定负责人并健全文档

 如果系统很大，特征很多，那么就得知道每个特征怎么来的，以及谁在维护。如果你发现对某个特这个你很熟悉的人离职了，确保这个信息已经交接给了下一个人。尽管一些特征名本身是可以自解释的，有更详细的说明，比如特征是啥，怎么来的，如何解读，总归是会有些帮助的。


