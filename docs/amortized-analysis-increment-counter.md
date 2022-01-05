# 计数器增量摊销分析

> 原文:[https://www . geesforgeks . org/摊销-分析-增量-计数器/](https://www.geeksforgeeks.org/amortized-analysis-increment-counter/)

[**摊余分析**](https://www.geeksforgeeks.org/analysis-algorithm-set-5-amortized-analysis-introduction/)**是指确定一个序列(不是单个)操作的时间平均运行时间。它不同于平均案例分析，因为在这里，我们不像我们对[快速排序](https://www.geeksforgeeks.org/quick-sort/)的平均案例分析那样，假设数据以平均(不是很差)的方式排列。也就是说，摊销分析是最坏情况分析，但针对的是一系列操作，而不是单个操作。它适用于由操作顺序组成的方法，其中绝大多数操作都很便宜，但有些操作很贵。这可以在下面实现的二进制计数器的帮助下可视化。**

**让我们通过在 c 语言中实现一个增量计数器来看到这一点。首先，让我们看看计数器增量是如何工作的。
让变量 **i** 包含值 0，我们执行 i++多次。因为在硬件上，每个操作都是以二进制形式执行的。让二进制数存储在 8 位。所以，价值是 00000000。让我们增加很多次。所以，我们找到的模式是:
000000000，0000001，0000010，00000011，00000100，00000101，00000110，00000111，00001000 等等…..**

****步骤:**
**1。**从最右边开始迭代，使所有的 1 都为零，直到找到第一个零。
**2。**迭代后，如果索引大于或等于零，则使零位于该位置至 1。**

## **C++**

```
#include <bits / stdc++.h>
using namespace std;

int main()
{
    char str[] = "10010111";
    int length = strlen(str);
    int i = length - 1;
    while (str[i] == '1') {
        str[i] = '0';
        i--;
    }
    if (i >= 0)
        str[i] = '1';
    printf("% s", str);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
import java.util.*;

class GFG{

public static void main(String args[])
{
    String st = "10010111";
    char[] str = st.toCharArray();
    int lengthh = st.length();
    int i = lengthh - 1;

    while (str[i] == '1')
    {
        str[i] = '0';
        i--;
    }

    if (i >= 0)
        str[i] = '1';

     System.out.print( str);
}
}

// This code is contributed by sanjoy_62
```

****输出:****

```
10011000
```

**简单地看程序或算法，它的运行成本看起来与位数成正比，但实际上，它与位数不成正比。让我们看看如何！**

**让我们假设增量操作执行了 k 次。我们看到，在每个增量中，它最右边的位被翻转。因此，LSB 的翻转次数为 k。例如，第二个最右边的在一个间隙后翻转，即以 2 个增量翻转 1 次。第三个最右边–以 4 个增量 1 次。第四个最右边–以 8 为增量 1 次。所以，翻转的次数是第二个最右位的 k/2，第三个最右位的 k/4，第四个最右位的 k/8，以此类推…**

**总成本将是翻转的总次数，即
C(k) = k + k/2 + k/4 + k/8 + k/16 + ……这是几何级数，还有，
C(k)<k+k/2+k/4+k/8+k/16+k/32+……直到无穷大
So，C(k)<k/(1-1/2)
So，C(k) < 2k
我们得出结论，计数器的增量是常数成本运算。**

****参考文献:****

1.  **[http://www . cs . Cornell . edu/courses/cs 3110/2013 sp/补充/背诵/rec21.html](http://www.cs.cornell.edu/courses/cs3110/2013sp/supplemental/recitations/rec21.html)**
2.  **[http://教职工. cs . tamu . edu/kla PPI/csce 411-s17/csce 411-摊销 3.pdf](http://faculty.cs.tamu.edu/klappi/csce411-s17/csce411-amortized3.pdf)**