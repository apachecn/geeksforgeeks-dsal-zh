# 循环关系练习集

> 原文:[https://www . geesforgeks . org/practice-set-recurrence-relations/](https://www.geeksforgeeks.org/practice-set-recurrence-relations/)

先决条件–[算法分析|第 1 集](https://www.geeksforgeeks.org/analysis-of-algorithms-set-1-asymptotic-analysis/)、[第 2 集](https://www.geeksforgeeks.org/analysis-of-algorithms-set-2-asymptotic-analysis/)、[第 3 集](https://www.geeksforgeeks.org/analysis-of-algorithms-set-3asymptotic-notations/)、[第 4 集](https://www.geeksforgeeks.org/analysis-of-algorithms-set-4-analysis-of-loops/)、[第 5 集](https://www.geeksforgeeks.org/analysis-algorithm-set-5-amortized-analysis-introduction/)

**Que-1。**求解以下递推关系？
t(n)= 7t(n/2)+3n^2+2
(a)o(n^2.8)
(b)o(n^3)
(c)？(n^2.8)
(d)？(n^3)

**解释–**
t(n)= 7t(n/2)+3n^2+2
从上式可以看出:
a = 7，b = 2，f(n) = 3n^2 + 2
所以，f(n) = O(n^c)，其中 c = 2。
属于[主定理](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)情况 1:
logb(a)= log2(7)= 2.81>2
由主定理第一种情况得出 T(n) =？(n^2.8)意味着 O(n^2.8)以及 O(n^3).
因此，选项(a)、(b)和(c)是正确的选项。

**Que-2。**按照渐近(大 o)复杂度的递减顺序对以下函数进行排序:
f1(n) = n^？n，f2(n) = 2^n，f3(n) = (1.000001)^n，F4(n)= n^(10)*2^(n/2)
(a)F2>F4>f1>F3
(b)F2>F4>F3>f1
(c)f1>F2>F3>F4
(d)F2>f1>F4>F3

**解释–**
F2>F4 因为我们可以写 f2(n) = 2^(n/2)*2^(n/2，f4(n) = n^(10)*2^(n/2)这清楚地表明 f2 > f4
f4 > f3 因为我们可以写 f4(n) = n^10.？？2?^n = n10。(1.414)n，清楚显示 F4>F3
F3>f1:
f1(n)= n^？n 取两边对数 f1 =？n log n
f3 (n) = (1.000001)^n 取 log 两边 log f3 = n log(1.000001)，我们可以写成 log f3 =？n*？n log(1.000001)和？n >对数(1.000001)。
所以，正确的顺序是 f2 > f4 > f3 > f1。选项(b)是正确的。

**Que-3。** f(n) = 2^(2n)
下列哪一项正确表示上述功能？
(a) O(2^n)
(b)？(2^n)
(c)？(2^n)
(d)这些都不是

**解释–**f(n)= 2^(2n)= 2^n*2^n
选项(a)表示 f(n) < = c*2n，不成立。
选项(c)表示 c1*2n < = f(n) < = c2*2n，满足下界但不满足上界。
选项(b)表示 c*2n < = f(n)这个条件满足，因此选项(b)是正确的。

**Que-4。**硕士定理可以应用于下列哪个递推关系？
(a)t(n)= 2t(n/2)+2^n
(b)t(n)= 2t(n/3)+sin(n)
(c)t(n)= t(n-2)+2n^2+1
(d)这些都不是

**解释–**主定理可以应用于以下类型的递推关系
T (n) = aT(n/b) + f (n)(除函数)& T(n)=aT(n-b)+f (n)(减函数)
选项(a)是错误的，因为要应用[主定理，](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)函数 f(n)应该是多项式。
选项(b)是错误的，因为为了应用主定理 f(n)应该是单调递增的函数。
选项(d)不是上面提到的类型，因此正确答案是(c)因为 T (n) = T (n-2) + 2n^2 + 1 会被认为是 T (n) = T (n-2) + 2n^2 那是递减函数的形式。

**那-5。**t(n)= 3t(n/2+47)+2n ^ 2+10 * n–1/2。T(n)会是

(a)o(n^2)
(b)o(n^(3/2)
(c)o(n log n)
(d)这些都不是

**解释–**对于更高值的 n，n/2 > > 47，所以我们可以忽略 47，现在 T(n)将是
t(n)= 3t(n/2)+2*n^2+10 * n–1/2 = 3t(n/2)+o(n^2)
应用主定理，它是主定理 T(n) = O(n^2).的情况 3
选项(a)正确。