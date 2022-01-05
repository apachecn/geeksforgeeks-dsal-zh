# 萨斯特里数字

> 原文:[https://www.geeksforgeeks.org/sastry-numbers/](https://www.geeksforgeeks.org/sastry-numbers/)

给定一个整数 **N** ，任务是检查 **N** 是否为萨斯特里数。

> 如果 **N** 与 **N + 1** 连接起来得到一个[完美的正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)，那么数字 **N** 就是萨斯特里数。

**例:**

> **输入:** N = 183
> **输出:**是
> **解释:**
> 183+184 = 183184 = 428<sup>2</sup>
> **输入:** N = 28
> **输出:**否

**方法:**思路是将数字转换为字符串，并串联 N 和(N + 1)，然后再次转换为整数。现在我们只需要检查最后的数字是否是一个完美的正方形。如果是，那么给定的数字是萨斯特里数。
以下是上述办法的实施情况:

**Output**

```
Yes
```

**参考文献:**[OEIS](https://oeis.org/A030465)T4】