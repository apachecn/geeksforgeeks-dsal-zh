# 求数列 5、13、37、109、325、.。。

> 原文:[https://www . geesforgeks . org/find-the-n-term-of-series-5-13-37-109-325/](https://www.geeksforgeeks.org/find-the-nth-term-of-the-series-5-13-37-109-325/)

给定正整数 **N** 。任务是找到系列 **5、13、37、109、325、** **的**第 n 个**术语…..**

**示例**:

> **输入** : N = 5
> **输出** : 325
> **说明:**从顺序可以看出第五项是 325
> 
> **输入** : N = 1
> **输出** : 5
> **说明:**给定序列的第一项为 5

**接近**:使用以下模式形成的序列。对于任何 N 值

> t<sub>N</sub>= 4 * 3<sup>N–1</sup>+N

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return Nth term
// of the series
int calcNum(int N) 
{ 
  return 4 * pow(3, N - 1) + 1; 
}

// Driver Code
int main()
{
    int N = 5;

    cout << calcNum(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
public class GFG
{

  // Function to return Nth term
  // of the series
  static int calcNum(int N) 
  { 
    return 4 * (int)Math.pow(3, N - 1) + 1; 
  }

  // Driver Code
  public static void main(String args[])
  {
    int N = 5;
    System.out.println(calcNum(N));
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to return Nth term
       // of the series
       function calcNum(N) {
           return 4 * Math.pow(3, N - 1) + 1;
       }

       // Driver Code
       let N = 5;
       document.write(calcNum(N));

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
325
```

***时间复杂度*** : O(1)
***辅助空间*** : O(1)