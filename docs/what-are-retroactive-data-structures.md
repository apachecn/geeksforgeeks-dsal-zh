# 什么是追溯性数据结构？

> 原文:[https://www . geesforgeks . org/什么是追溯性数据结构/](https://www.geeksforgeeks.org/what-are-retroactive-data-structures/)

追溯数据结构是一种支持对[数据结构](https://www.geeksforgeeks.org/data-structures/)进行有效修改的数据结构类型，在这种新的数据结构范式中，对数据结构进行的操作不仅存在于现在，也存在于过去，这意味着即使在消遣时间间隔内，这些操作也可以改变和修改。

在处理需要定期更新的复杂应用程序时，这些数据结构在灵活性方面给了我们很大的安慰，因为调整结构可以根据程序的工作模型进行调整，在现实世界中，有各种情况需要从一系列操作中修改过去的操作。

### 追溯数据结构的需求:

*   **实现动态化:**一般来说，一些静态的[算法](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)需要一个动态的数据结构来处理它们的输入，追溯数据结构可以是使这些算法动态化的最佳解决方案。
*   **用于执行近似范围搜索:**追溯数据结构有助于实现需要在任何时间点进行插入和删除等更新的操作，并在近似时间范围 t 内返回输入
*   **避免额外的 O(log n)开销:**追溯数据结构帮助我们避免额外的 O(log n)开销，并使应用程序能够执行操作，例如在段上构建高度的段树，用传统数据结构扩充根，用 CDFC 结构扩充节点。
*   **改变事务的历史顺序:**追溯性数据结构使应用程序能够有效地适应各种条件，例如撤销以前发生的错误，而无需重新进行此后的所有工作。

**与持久数据结构的比较:**

即使[持久数据结构](https://www.geeksforgeeks.org/persistent-data-structures/)和追溯数据结构的概念在考虑时间维度时看起来相似，但它们处理时间元素的方式仍然使它们彼此不同。

*   持久数据结构维护多个版本的数据结构，并且可以在一个版本的数据上实现操作来创建另一个版本。
*   在追溯数据结构的情况下，直接对以前的版本进行更改，并且不创建在过去经历数据更改的其他修改过的以前版本。

### 追溯的类型:

**1。部分追溯:**任何数据结构都可以通过一般转换进行部分追溯。例如，下面插入一个初始状态为[1，2，3，4，5]的部分追溯列表。然后，我们可以添加或删除当前的操作。

以下是上述概念的 Python 伪代码:

```
# Python program to implement  
# the above approach  
x = PartiallyRetroactive([1, 2, 3, 4, 5])  
def appendOne(lst):
 return lst + [1]

# Three appendOnes by applying  
# insertAgo()
x.insertAgo(appendOne, tminus = 0)
x.insertAgo(appendOne, tminus = 0)
x.insertAgo(appendOne, tminus = 0)
x.query()

# Three appendOnes by applying insertAgo()
[1, 2, 3, 4, 5, 1, 1, 1]   
```

**输出:**

```
>>x.query() :
[1, 2, 3, 4, 5, 1, 1, 1]
```

我们还可以添加或删除过去的操作:

```
def MethodForAppendNum(lst):
       return lst + [6]

 ## For Inserting into  *two* operations ago
 a.insertAgo(appendSix, tminus=2)   
 a.query()
 [1, 2, 3, 4, 5, 1, 6, 1, 1]

 ## For Deleting the first appendOne
 a.deleteAgo(tminus=3)   
 a.query()
 [1, 2, 3, 4, 5, 6, 1, 1]
```

**输出:**

```
>>a.query() :
[1, 2, 3, 4, 5, 1, 6, 1, 1]
```

**2。一般完全追溯:**完全追溯数据结构类似于它们的兄弟部分追溯数据结构，因为它们允许操作的追溯插入和删除。然而，完全追溯的数据结构也允许查询过去，而不仅仅是现在。

下面是上述方法的 Python 伪代码:

```
b = MethodForFullyRetroactive([1,2,3])
b.insertAgo(appendOne, tminus = 0)

## This one should come last
b.insertAgo(appendSix, tminus = 0) 

## This one should come first
b.insertAgo(appendTen, tminus =2)

b.query()

## The current state of the data structure
[1, 2, 3, 10, 1, 6]   
b.query(1)
[1, 2, 3, 10, 1]
b.query(2)
[1, 2, 3, 10]
b.query(3)

## The state of the data structure way back
## in the past
[1, 2, 3]   
```

**输出:**

```
>>b.query(1) :
[1, 2, 3, 10, 1, 6]
>>b.query(2) :
[1, 2, 3, 10]
>>b.query(3) :
[1, 2, 3]
```

**应用:**追溯数据结构的一些应用如下

*   **Recovery:** If one of our hardware chips is damaged and the data on it is lost, but it has been repaired now, we can read the data from the sensor, and we want the data to be inserted back into the system as if the hardware has never been damaged.
*   **Error correction:** The data input is incorrect, so it is necessary to correct the data to eliminate the secondary influence of incorrect input.
*   **Data manipulation in recreation area:** Modifying data in recreation area is helpful to prevent damage control in case of injecting false data due to system error or manual error.
*   **Bad data:** When processing data input in large-scale systems, especially in systems such as sensors in the weather network, failure will lead to a large number of automatic data transmission, and garbage and incorrect data may cause great damage to applications. The ideal solution is to delete bad data in past operations by using traceability data structure, thus creating a scene, such as if bad data never happened.

**追溯性数据结构的优势:**

*   When the data crashes, it is unnecessary to use cost-effective rollback operation, which provides us with the flexibility to correct the time-based update.
*   These data structures can be most effectively applied to search problems, such as maintaining a set K of unknown objects, which are subjected to operations such as insertion, deletion and query (x, s), because here we can have the privilege to modify the data structures by returning and retrieving the queries we want again in chronological order.
*   These data structures help us to solve the decomposed search problem, such as the query of form query(x, AuB) = f(query(x, a), query (x, b)) running in O(1) time.
*   They are helpful to dynamic static algorithms effectively.

**追溯性数据结构的缺点:**

*   These data structures run in higher polynomial time and require higher storage and computing resources.
*   These data structures are suitable for complex applications, which only rely on time-based updates without proper sequence-based goals, but are not recommended for simple and extensible applications, which generate timely updates based on strict rules, such as **employee attendance management system and one-time password generator** , because the implementation of this data structure will produce errors for changing and modifying information.
*   Due to the high polynomial transformation, high maintenance cost is involved.
*   If the application implemented by tracing data structure does not cover the effective encryption algorithm standard, it is very likely that there will be intentional data operation or even no tracking, because there is no available time record.

**自动追溯:**对于通过使用通用技术将数据结构自动转换为追溯形式的可能性，我们的头脑中自然会产生疑问，例如将指针机器模型转换为有效的部分追溯数据结构？这种通用技术将很好地补充现有的持久性数据结构，但是在追溯数据结构的情况下，追溯与持久性有着根本的不同，并且一般已知的技术并不适用。

解决这一普遍问题的一种简单方法是回滚方法，其中存储辅助信息，因为数据结构的所有更改都是由每个操作以这样一种方式进行的，即每个更改都可以动态反转。例如，为了启用内存写操作的回滚，我们存储先前在地址中的值，因此它们的性能根据追溯更改而有所不同。

**追溯运行时间:**取数据结构执行的若干操作，用于确定追溯数据结构的运行时间。例如，假设 m 是在结构上执行的操作数，r 是在追溯操作之前执行的操作数，n 是在任何时候结构中存在的最大元素数。