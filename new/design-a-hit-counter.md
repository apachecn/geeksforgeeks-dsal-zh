# 设计点击计数器

设计一个点击计数器，计算过去 5 分钟内收到的点击次数。

**来源：** [Microsoft 面试体验](https://www.geeksforgeeks.org/microsoft-interview-experience-set-109-2-years-experienced/)

最近，包括 Dropbox 在内的许多公司都提出了“设计命中计数器”问题，这个问题比看起来要困难的多。 它包括几个主题，例如基本数据结构设计，各种优化，并发和分布式计数器。

它应该支持以下两个操作：**命中**和 **getHits** 。

**hit（timestamp）** –显示给定时间戳的匹配。

**getHits（timestamp）**-返回过去 5 分钟（300 秒）（从 currentTimestamp）收到的命中数。

每个函数都接受一个 timestamp 参数（以秒为单位），并且您可以假定按时间顺序对系统进行了调用（即时间戳是单调递增的）。 您可以假定最早的时间戳记从 1 开始。

例子：

```

HitCounter counter = new HitCounter();

// hit at timestamp 1.
counter.hit(1);

// hit at timestamp 2.
counter.hit(2);

// hit at timestamp 3.
counter.hit(3);

// get hits at timestamp 4, should return 3.
counter.getHits(4);

// hit at timestamp 300.
counter.hit(300);

// get hits at timestamp 300, should return 4.
counter.getHits(300);

// get hits at timestamp 301, should return 3.
counter.getHits(301);

```

**询问：**微软，亚马逊，Dropbox 等。

**1.简单解决方案（暴力法）：**

我们可以使用向量来存储所有匹配。 这两个功能是自我解释。

```
vector< int > v;
/* Record a hit.
@param timestamp - The current timestamp (in
seconds granularity).  */
void hit( int timestamp)
{
v.push_back(timestamp);
}
// Time Complexity : O(1)
@param timestamp - The current timestamp (in
seconds granularity). */
int getHits( int timestamp)
{
int i, j;
for (i = 0; i < v.size(); ++i) {
if (v[i] > timestamp - 300) {
break ;
}
}
return v.size() - i;
}
// Time Complexity : O(n)
```

**2.空间优化解决方案：**

我们可以使用队列存储命中并删除队列中没有用的条目。 它将节省我们的空间。
我们正在从队列中删除多余的元素。

```
queue< int > q;
/** Record a hit.
@param timestamp - The current timestamp
(in seconds granularity). */
void hit( int timestamp)
{
q.push(timestamp);
}
// Time Complexity : O(1)
/** Return the number of hits in the past 5 minutes.
@param timestamp - The current timestamp (in seconds
granularity). */
int getHits( int timestamp)
{
while (!q.empty() && timestamp - q.front() >= 300) {
q.pop();
}
return q.size();
[
}
// Time Complexity : O(n)
```

**3.最优化的解决方案：**

如果数据无序排列并且多个匹配项带有相同的时间戳怎么办？

由于没有排序数据就无法使用队列方法，因此这次需要使用数组来存储每个时间单位的点击计数。

如果我们以过去的 5 分钟（即 300 秒）为单位跟踪点击，则创建 2 个大小为 300 的数组。
int [] hits = new int [300];

TimeStamp [] times = new TimeStamp [300]; //最后计数的匹配
的时间戳给定传入的时间戳，将其时间戳修改 300，以查看其在 hits 数组中的位置。

int idx =时间戳％300; => hits [idx]保持点击计数在这一秒内发生

但是，在我们将 idx 的点击次数增加 1 之前，时间戳确实属于 hits [idx]正在跟踪的秒数。
timestamp [i]存储最后一次计数的命中的时间戳。
如果使用时间戳记[i] >时间戳记，则此匹配应该被丢弃，因为它在过去 5 分钟内没有发生。
如果 timestamp [i] ==时间戳，则 hits [i]增加 1。
如果 timestamp [i] currentTime – 300。

```
vector< int > times, hits;
times.resize(300);
hits.resize(300);
[
/** Record a hit.
@param timestamp - The current timestamp
(in seconds granularity). */
void hit( int timestamp)
{
int idx = timestamp % 300;
if (times[idx] != timestamp) {
times[idx] = timestamp;
hits[idx] = 1;
}
else {
++hits[idx];
}
}
// Time Complexity : O(1)
[
/** Return the number of hits in the past 5 minutes.
@param timestamp - The current timestamp (in
seconds granularity). */
int getHits( int timestamp)
{
int res = 0;
for ( int i = 0; i < 300; ++i) {
if (timestamp - times[i] < 300) {
res += hits[i];
}
}
return res;
}
// Time Complexity : O(300) == O(1)
```

**如何处理并发请求？**

当两个请求同时更新列表时，可能会出现争用情况。 有可能最终未包含首先更新列表的请求。

最常见的解决方案是使用锁来保护列表。 每当有人想要更新列表（通过添加新元素或删除尾部）时，将在容器上放置一个锁。 操作完成后，列表将被解锁。

当您的请求量不大或性能不重要时，此方法效果很好。 放置锁有时可能会很昂贵，并且当并发请求过多时，锁可能会阻塞系统并成为性能瓶颈。

**分配计数器**

当一台计算机的流量过多而性能成为问题时，现在正是考虑分布式解决方案的最佳时机。 分布式系统通过将系统扩展到多个节点，显着减少了单台机器的负担，但同时又增加了复杂性。

假设我们将访问请求平均分配给多台计算机。 我想首先强调平均分配的重要性。 如果特定的计算机比其他计算机获得更多的流量，则该系统无法充分使用，因此在设计系统时必须考虑到这一点，这一点非常重要。 在我们的情况下，我们可以获取用户电子邮件的哈希值并按哈希值进行分发（直接使用电子邮件不是一个好主意，因为某些字母的出现频率可能比其他字母高得多）。

为了计算数量，每台机器都独立工作以计算过去一分钟内自己的用户。 当我们请求全局编号时，我们只需要将所有计数器加在一起即可。

**参考：**我最初是在此处发布它的。
https://aonecode.com/getArticle/211

[![design-pattern-img](img/14db468c0f00e6c64bfe591457d1b437.png)](https://practice.geeksforgeeks.org/courses/design-patterns-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_ooddpl)

* * *

* * *



