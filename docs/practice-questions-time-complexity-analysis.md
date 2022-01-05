# 时间复杂度分析练习题

> 原文:[https://www . geesforgeks . org/练习-问题-时间-复杂性-分析/](https://www.geeksforgeeks.org/practice-questions-time-complexity-analysis/)

先决条件:[算法分析](https://www.geeksforgeeks.org/analysis-of-algorithms-set-3asymptotic-notations/)
**1。**的时间、空间复杂度是多少**以下代码:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
int a = 0, b = 0;
for (i = 0; i < N; i++) {
    a = a + rand();
}
for (j = 0; j < M; j++) {
    b = b + rand();
}
```

**选项:**

1.  O(N * M)时间，O(1)空间
2.  时间，空间
3.  O(N + M)时间，O(1)空间
4.  O(N * M)时间，O(N + M)空间

**输出:**

```
3\. O(N + M) time, O(1) space
```

**说明:**第一个循环是 O(N)，第二个循环是 O(M)。既然不知道哪个大，我们就说这个是 O(N + M)。这也可以写成 O(max(N，M))。
由于没有额外的空间被利用，空间复杂度为常数/0(1)
**2。****以下代码的时间复杂度是多少:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
int a = 0;
for (i = 0; i < N; i++) {
    for (j = N; j > i; j--) {
        a = a + i + j;
    }
}
```

**选项:**

1.  O(N)
2.  O(N*log(N))
3.  O(N * Sqrt(N))
4.  O(N*N)

**输出:**

```
4\. O(N*N)
```

**解释:**
上述代码运行总次数
= n+(n–1)+(n–2)+…1+0
= n *(n+1)/2
= 1/2 * n^2+1/2 * n
o(n^2)次。
**3。****以下代码的时间复杂度是多少:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
int i, j, k = 0;
for (i = n / 2; i <= n; i++) {
    for (j = 2; j <= n; j = j * 2) {
        k = k + n / 2;
    }
}
```

**选项:**

1.  O(n)
2.  他(波兰)
3.  O(n^2)
4.  O(n^2Logn)

**输出:**

```
2\. O(nLogn)
```

**说明:**如果你注意到了，j 一直翻倍直到小于等于 n，几次，我们可以把一个数翻倍到小于 n，就是 log(n)。
我们来举个例子。
为 n = 16，j = 2，4，8，16
为 n = 32，j = 2，4，8，16，32
所以，j 会运行 O(log n)步。
我跑 n/2 步。
所以，总步数= O(n/2 * log(n))=**O(n * logn)**
**4。当我们说一个算法 X 在渐近上比 Y 更有效时，这意味着什么？**
**选项:**

1.  对于小输入，x 永远是更好的选择
2.  对于大输入，x 永远是更好的选择
3.  对于小投入，y 永远是更好的选择
4.  对于所有输入，x 总是更好的选择

```
2\. X will always be a better choice for large inputs
```

**说明:**在渐近分析中，我们考虑了算法在输入大小方面的增长。如果对于大于 n0 的值的所有输入大小 n，X 花费的时间小于 Y，则算法 X 被称为渐近优于 Y，其中 n0 > 0。

**5。****以下代码的时间复杂度是多少:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
int a = 0, i = N;
while (i > 0) {
    a += i;
    i /= 2;
}
```

**选项:**

1.  O(N)
2.  O(Sqrt(N))
3.  o(不适用)
4.  o(对数 N)

输出:

```
4\. O(log N)
```

**解释:**我们必须找到最小的 x，使得 N / 2^x N
x = log(N)

**6。以下哪一项最能描述比较算法效率的有用标准？**

1.  时间
2.  记忆
3.  以上两者
4.  以上都不是

```
3\. Both of the above
```

**说明:**比较一个算法的效率显然取决于一个算法占用的时间和内存，

**7。时间复杂度是如何衡量的？**

1.  通过计算算法中算法的数量。
2.  通过计算算法在给定输入大小上执行的原语操作的数量。
3.  通过计算输入到算法中的数据量。
4.  以上都不是

```
2\. By counting the number of primitive operations performed by the algorithm on given input size.
```

**8。以下代码的时间复杂度是多少？**

## java 描述语言

```
for(var i=0;i<n;i++)
    i*=k
```

1.  O(n)
2.  好的
3.  O(log <sub>k</sub> n)
4.  O(log <sub>n</sub> k)

**输出:**

```
3\. O(logkn)
```

**解释:**因为循环 k <sup>n-1</sup> 次，所以取原木后变成原木 <sub>k</sub> n。

**9。以下代码的时间复杂度是多少？**

## java 描述语言

```
var value = 0;
for(var i=0;i<n;i++)
    for(var j=0;j<i;j++)
    value += 1;
```

1.  n
2.  (n+1)
3.  n(n-1)/2
4.  n(n+1)/2

**输出:**

```
3\. n(n-1)/2
```

**说明:**第一个 for 循环将运行(n)次，另一个 for 循环将运行(n-1)次，因此总时间为 n(n-1)/2。

**10。算法 A 和 B 的最坏情况运行时间分别为 O(n)和 O(logn)。因此，算法 B 总是比算法 a 运行得快**

1.  真实的
2.  错误的

```
False
```

**解释:**大 O 符号提供了算法运行时间的渐近比较。例如，对于 n < n <sup>0</sup> ，算法 A 可能比算法 B 运行得更快。