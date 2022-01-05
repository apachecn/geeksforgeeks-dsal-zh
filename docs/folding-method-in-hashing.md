# 散列中的折叠方法

> 原文:[https://www.geeksforgeeks.org/folding-method-in-hashing/](https://www.geeksforgeeks.org/folding-method-in-hashing/)

**折叠法在** [**哈希**](https://www.geeksforgeeks.org/hashing-data-structure/) **:** 它把一个键值分解成精确的段，这些段被相加形成一个[哈希值](https://www.geeksforgeeks.org/foldable-binary-trees/)，再来看看另一种技术，就是在相加之前对每个段单独应用一个乘法哈希函数。有些折叠方法更进一步，在添加之前，每隔一段就反转一次。这种折叠方式**独立于分布**。

**算法:**

*   The folding method used to create the hash function starts with dividing the item into equal-sized blocks, that is, the last block may be of different sizes.
*   The result of adding these [bits](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/) together is the hash value, **h (x) = (a+b+c) mod m** , where a, b and c represent the preprocessed key divided into three parts, **m** is the table size, and
***   In other words, the sum of the three parts of the preprocessing key is divided by the table size. The rest is the hash key.T21】**

****说明:****

****示例 1:** 任务是将密钥 **123456789** 折叠成十个空格的哈希表(0 到 9)。**

***   The key is given, and it is said that **x** is 123,456,789 and the table size (namely **m** = 10).*   Because it can divide **x** into three parts in any order. Let's divide it equally.*   Therefore, a = 123, b = 456 and c = 789.*   【t0 h(x)=(a+b+ c)对着 m(123456789)=(123+456+789)对着 10 = 1368 对着 10 = **对着 T3 .***   Therefore, 123456789 is inserted into the table with address **8** .**

****示例 2:** 任务是将密钥 **452378912** 折叠成十个空格的哈希表(0 到 9)。**

***   The key is given, saying that **x** is **452378912** and table size (namely **m** = 10).*   Because it can divide **x** into three parts in any order. Let's divide it equally.*   Therefore, a = 452, b = 378 and c = 912.*   【t0 h(x)=(a+b+ c)对着 m(457822)=(452+378+912)对着 10 = 1742 对着 10 = **对着 T3 .***   Therefore, 452378912 is inserted in the table with address **2** .**