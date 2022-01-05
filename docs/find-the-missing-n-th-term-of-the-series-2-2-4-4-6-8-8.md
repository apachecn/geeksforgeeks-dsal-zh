# 求数列 2，2，4，4，6，8，8 …的缺失的第 N 项。

> 原文:[https://www . geesforgeks . org/find-the-missing-n-term-of-series-2-2-4-4-6-8-8/](https://www.geeksforgeeks.org/find-the-missing-n-th-term-of-the-series-2-2-4-4-6-8-8/)

给定一个数字 **N，**找到系列 **2，2，4，4，6，8，8……**中的**第 N 项**

**示例:**

> **输入:**N = 1
> T3】输出: 2
> 
> **输入:**N = 2
> T3】输出: 2
> 
> **输入:**N = 5
> T3】输出: 6

**方法:**仔细观察给定的系列，可以看出它是由两个不同的系列在交替的位置梳理在一起组成的。

> 原始系列:2、2、4、4、6、8、8、…
> ————————————————————————
> 仅考虑偶数位置:
> = > 2、2、4、4、6、8、8、…
> = > 2、_、4、_、6、_、8、…(考虑基于 0 的索引)
> = > 2、4、6、8、…(一个 AP 系列)
> —————————————同样，仅考虑奇数位:
> = > 2、2、4、4、6、8、8、……
> =>_、2、_、4、_、8、……(考虑基于 0 的索引)
> = > 2、4、8、……(一个 GP 系列)
> 可以看出，奇数位的数字构成

因此，可以说给定的数列是两个不同数列的混合，其中所有的 A.P 项都位于偶数位置，所有的 G.P 项都位于奇数位置。
因此，在上述观察的基础上，按照以下步骤找到给定序列的第 n 个缺失项:

1.  如果 n 是奇数:
    1.  要求的条款是 A.P [2，4，6，8 …]的第(n+1)/2 <sup>个</sup>条款。
    2.  A.P 的第 n <sup>个</sup>项可计算为**A+(n–1)d .**
2.  如果 n 是偶数:
    1.  所需术语是通用术语[2，4，8 …]的第 n/2 <sup>个</sup>术语。
    2.  通用零件的第 n <sup>个</sup>项可计算为**a * r<sup>n-1</sup>T5】**

下面是上述方法的实现:

## C++

```
// C++ code to find the n-th term
// of series 2, 2, 4, 4, 6, 8, 8...
#include <iostream>
#include <math.h>
using namespace std;

// Driver code
int main()
{
    int n = 15;
    int term;

    // If n is even
    if (n % 2 == 0) {
        term = n / 2;

        // a(first term) = 2
        // r(common ratio) = 2
        cout << 2 * pow(2, term - 1);
    }

    // If n is odd
    else {
        term = (n + 1) / 2;

        // a(first term) = 2
        // d(common ratio) = 2
        cout << 2 + (term - 1) * 2;
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;

class GFG {
  public static void main(String[] args)
  {
    int n = 15;
    int term;

    // If n is even
    if (n % 2 == 0) {
      term = n / 2;

      // a(first term) = 2
      // r(common ratio) = 2
      System.out.println(2 * Math.pow(2, term - 1));
    }

    // If n is odd
    else {
      term = (n + 1) / 2;

      // a(first term) = 2
      // d(common ratio) = 2
      System.out.println(2 + (term - 1) * 2);
    }
  }
}

// This code is contributed by Potta Lokesh
```

## 计算机编程语言

```
# Python code to find the n-th term
# of series 2, 2, 4, 4, 6, 8, 8...

# Driver code
n = 15;
term = 0;

# If n is even
if (n % 2 == 0):
    term = n / 2;

    # a(first term) = 2
    # r(common ratio) = 2
    print(2 * int(pow(2, term - 1)));

# If n is odd
else:
    term = (n + 1) / 2;

    # a(first term) = 2
    # d(common ratio) = 2
    print(2 + int((term - 1) * 2));

# This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# code for the above approach
using System;

class GFG {
    public static void Main(string[] args)
    {
        int n = 15;
        int term;

        // If n is even
        if (n % 2 == 0) {
            term = n / 2;

            // a(first term) = 2
            // r(common ratio) = 2
            Console.WriteLine(2 * Math.Pow(2, term - 1));
        }

        // If n is odd
        else {
            term = (n + 1) / 2;

            // a(first term) = 2
            // d(common ratio) = 2
            Console.WriteLine(2 + (term - 1) * 2);
        }
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript code to find the n-th term
// of series 2, 2, 4, 4, 6, 8, 8...

// Driver code
let n = 15;
let term;

// If n is even
if (n % 2 == 0) {
    term = n / 2;

    // a(first term) = 2
    // r(common ratio) = 2
    document.write(2 * Math.pow(2, term - 1));
}

// If n is odd
else {
    term = (n + 1) / 2;

    // a(first term) = 2
    // d(common ratio) = 2
    document.write(2 + (term - 1) * 2);
}

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
16
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)