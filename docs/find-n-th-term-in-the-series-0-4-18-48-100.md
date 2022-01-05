# 求数列 0、4、18、48、100 中的第 N 项……

> 原文:[https://www . geesforgeks . org/find-n-th-系列术语-0-4-18-48-100/](https://www.geeksforgeeks.org/find-n-th-term-in-the-series-0-4-18-48-100/)

**给**一个系列 **0，4，18，48，100。。。**和一个整数 **N** ，任务是找到该系列的**第 N 项**。

**示例:**

> **输入:** N = 4
> **输出:** 48
> **解释:**如顺序所示，我们可以看到第 4 项是 48
> 
> **输入:**N = 6
> T3】输出: 180

**进场:**考虑以下观察:

> 对于 N = 2，第二项为 4，可以表示为 8–4，即 2<sup>3</sup>–2<sup>2</sup>
> 
> 对于 N = 3，第三项为 18，可以表示为 27–9，即 3<sup>3</sup>–3<sup>2</sup>
> 
> 对于 N = 4，第四项为 18，可以表示为 27–9，即 4<sup>3</sup>–4<sup>2</sup>
> 
> 。
> 
> 。
> 
> 。
> 
> 同样，本系列的第 N 项**可以表示为 N<sup>3</sup>–N<sup>2</sup>T5】**

所以对于任何一个 N，找到那个 N 的**平方**，然后**从这个数的**立方**中减去**。

下面是上述方法的实现:

## C++

```
// C++ code to find Nth term of series
// 0, 4, 18, ...

#include <bits/stdc++.h>
using namespace std;

// Function to find N-th term
// of the series
int getNthTerm(int N)
{
    // (pow(N, 3) - pow(N, 2))
    return (N * N * N) - (N * N);
}

// Driver Code
int main()
{
    int N = 4;

    // Get the 8th term of the series
    cout << getNthTerm(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find Nth term of series
// 0, 4, 18, ...
class GFG
{

    // Function to find N-th term
    // of the series
    public static int getNthTerm(int N) 
    {

        // (pow(N, 3) - pow(N, 2))
        return (N * N * N) - (N * N);
    }

    // Driver Code
    public static void main(String args[])
    {
        int N = 4;

        // Get the 8th term of the series
        System.out.println(getNthTerm(N));
    }
}

// This code is contributed by gfgking
```

## 蟒蛇 3

```
# Python code to find Nth term of series
# 0, 4, 18, ...

# Function to find N-th term
# of the series
def getNthTerm(N):

    # (pow(N, 3) - pow(N, 2))
    return (N * N * N) - (N * N);

# Driver Code
N = 4;

# Get the 8th term of the series
print(getNthTerm(N));

# This code is contributed by gfgking
```

## C#

```
// C# code to find Nth term of series
// 0, 4, 18, ...

using System;
class GFG {
    // Function to find N-th term
    // of the series
    public static int getNthTerm(int N) {
        // (pow(N, 3) - pow(N, 2))
        return (N * N * N) - (N * N);
    }

    // Driver Code
    public static void Main() {
        int N = 4;

        // Get the 8th term of the series
        Console.Write(getNthTerm(N));
    }
}

// This code is contributed by gfgking
```

## java 描述语言

```
<script>
// Javascript code to find Nth term of series
// 0, 4, 18, ...

// Function to find N-th term
// of the series
function getNthTerm(N) {
    // (pow(N, 3) - pow(N, 2))
    return (N * N * N) - (N * N);
}

// Driver Code

let N = 4;

// Get the 8th term of the series
document.write(getNthTerm(N));
// This code is contributed by gfgking
</script>
```

**Output**

```
48
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)