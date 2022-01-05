# 证明:为什么 A 的补码概率等于 1 减去 A 的概率【P(A’)= 1-P(A)】

> 原文:[https://www . geeksforgeeks . org/proof-why-概率补码等于-1-减-概率-a-pa-1-pa/](https://www.geeksforgeeks.org/proof-why-probability-of-complement-of-a-equals-to-one-minus-probability-of-a-pa-1-pa/)

[**概率**](https://www.geeksforgeeks.org/mathematics-probability/) 是指事件发生的程度。当事件发生时，如扔球、从牌组中选牌等。，那么一定有某种概率与那个事件有关。

**基本术语:**

*   **随机事件-**
    如果一个实验的重复在相似的条件下发生几次，如果它并不是每次都产生相同的结果，而是一个试验中的结果是几种可能的结果之一，那么这样的实验被称为随机事件或概率事件。
*   [**样本空间**](https://www.geeksforgeeks.org/chance-and-probability/)**–**
    样本空间是指随机事件所有可能结果的集合。例如，当抛硬币时，可能的结果是正面和反面。
*   [**事件**](https://www.geeksforgeeks.org/types-of-events-in-probability/)**–**
    事件是指与随机事件相关联的样本空间的子集。
*   [**事件的发生**](https://www.geeksforgeeks.org/dependent-and-independent-events-probability/)**–**
    如果属于某个随机事件的任何一个基本事件是一个结果，则该事件被称为发生。
*   [**补语**](https://www.geeksforgeeks.org/set-operations/#:~:text=Complement,set%20A%20is%20U%20%E2%80%93%20A.)**–**
    在集合中，集合的补语，A 是 A 中不存在的所有元素的集合，用 A’或 A <sup>c</sup> 表示。例如，在一个滚动骰子的实验中，如果 A 是所有偶数结果的集合，那么，A’就是所有奇数结果的集合。
*   [**【互斥事件】**](https://www.geeksforgeeks.org/event-and-its-types/)**–**
    与随机事件相关联的两个或多个事件被称为互斥事件。如果任何一个事件发生，它会阻止所有其他事件的发生。这意味着没有两个或更多的事件可以同时发生。

```
If A and B are mutually exclusive events, then
A ∩ B = ∅
Also, P(A ∩ B) = 0
```

**概率公理:**

> 1.  For any set A, the probability of A is always greater than or equal to zero, that is, P(A) > =0.
> 2.  The probability of sample space (s) is always equal to one, that is, P(S) = 1.
> 3.  If a <sub>1</sub> , a <sub>2</sub> , a <sub>3</sub> , a <sub>4</sub> ... A <sub>N</sub> are mutually exclusive events, then the probability of the combination of these mutually exclusive events will be equal to the sum of the probabilities of these mutually exclusive events. That is, p (a <sub>1</sub> ∪ a <sub>2</sub> ∪ a <sub>a <sub>n</sub> ) = p (a <sub>1</sub> )+p (a <sub>2 + P(A <sub>N</sub> )</sub></sub>

**问题陈述:**
为什么 A 的补码的概率等于 1 减去 A 的概率？

**解决方案:**
我们先从上述问题陈述的证明开始。以下是证明的步骤-

1.考虑一个事件，因为一个实验的样本空间包含了一个实验的所有可能的结果，而 A 和 A’的[并集包含了这个实验的所有可能的结果。所以，样本空间可以写成-](https://www.geeksforgeeks.org/union-and-intersection-of-sets/)

```
S = A ∪ A'
Also, P(S) = P(A ∪ A') --- (1)
```

2.既然 a 和 a’的交集等于∅，可以说 a 和 a’是互斥事件。所以，根据公理 3，

```
Since, A ∩ A' = ∅
P(A ∪ A') = P(A) + P(A') --- (2)
```

3.现在，从等式(1)和(2)，它可以写成-

```
P(S) = P(A) + P(A')
```

4.从公理 2 可知，样本空间的概率总是等于 1，即

```
P(S) = 1
P(A) + P(A') = 1 --- (3)
```

5.在重新排列等式(3)之后，获得以下等式-

```
P(A') = 1 - P(A)
```

即 A 的补码的概率等于 1 减去 A 的概率。因此，证明。

**例子:**
我们来看一些与上述证明相关的已解决的例子——

**1。骰子掷一次。**

> **事件 A-** 出现偶数
> 
> **样本空间，S-** {1，2，3，4，5，6}
> 
> P(S) = 1
> 
> A = {2，4，6}即 P(A) = 3/6 = 1/2
> 
> A' = {1，3，5}即 P(A') =3/6 = 1/2
> 
> 现在，我们可以很容易地观察到，s = a∪a’并且由于 a∪a’=∅，
> A 和 a’是互斥事件，这意味着
> 
> P(S)= P(A∪A’)
> 
> P(S)= P(A)+P(A’)
> 
> P(S) = 1/2 + 1/2
> 
>        = 1
> 
> P(A’)= 1–P(A)
> 
> p(A’)= 1–1/2
> 
> p(A’)= 1/2

**2。** **两枚硬币掷来掷去。**

> **事件 A-** 两头出现
> 
> **样本空间，S- {** HH，HT，TH，TT}
> 
> P(S) = 1
> 
> A = {HH}即 P(A) =1/4
> 
> A' = {HT，TH，TT}即 P(A') =3/4
> 
> 即 s = a∪a ’,由于 a∪a ’=∅，我们可以说 a 和 a’是
> 互斥事件，这意味着–
> 
> P(S)= P(A∪A’)
> 
> P(S)= P(A)+P(A’)
> 
> P(S) = 1/4 + 3/4
> 
> P(S) = 1
> 
> P(A’)= 1–P(A)
> 
> p(A’)= 1–1/4
> 
> p(A’)= 3/4