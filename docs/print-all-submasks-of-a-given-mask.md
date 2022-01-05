# 打印给定掩膜的所有子掩膜

> 原文:[https://www . geesforgeks . org/print-all-submasks-of-a-给定掩码/](https://www.geeksforgeeks.org/print-all-submasks-of-a-given-mask/)

给定一个整数 **N** ，任务是打印由存在于 **N** 的二进制表示中的[集合位构成的集合的所有子集。](https://www.geeksforgeeks.org/prime-number-of-set-bits-in-binary-representation-set-1/)

**示例:**

> **输入:** N = 5
> **输出:** 5 4 1
> **说明:**
> N 的二进制表示为“101”，因此所有需要的子集为{“101”、“100”、“001”、“000”}。
> 
> **输入:** N = 25
> **输出:** 25 24 17 16 9 8 1
> **说明:**
> N 的二进制表示为“1101”。因此，所有必需的子集都是{“11001”、“11000”、“10001”、“10000”、“01001”、“01000”、“0001”、“0000”}。

**简单方法:**最简单的方法是遍历范围内的每个掩码【T20，1】<<(N)**中的设置位计数，并检查除了 **N** 中的位之外，是否没有其他位设置在其中。然后，打印出来。
***时间复杂度:**O(2<sup>(N 中设置位计数)</sup> )*
***辅助空间:** O(1)***

****高效方法:**上述方法可以通过仅遍历作为掩码 **N** 的子集的**子库**来优化。**

> ***   Let **s** be the current sub-mask, which is a subset of the mask **n** . Then, it can be observed that by assigning **s = (s–1) & n** , the next subtask of **n** less than **s** can be obtained.*   In [T0】 S-1 【T1 , it flips all the bits to the right of the rightmost setting bit, including the rightmost setting bit of **s** .*   Therefore, after performing **bit by bit &** with **n** , the subtasks of **n** are obtained.*   Therefore, **s = (s–1) & n** gives the next subtask of **n** , which is less than **s** .**

**按照以下步骤解决问题:**

*   **初始化一个变量，比如 **S = N.****
*   **在 **S > 0** 时迭代，在每次迭代中，打印 **S** 的值。**
*   **分配**S =(S–1)&n .****

**下面是上述方法的实现:**

## **C++**

```
// C++ Program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the submasks of N
void SubMasks(int N)
{
    for (int S = N; S; S = (S - 1) & N) {
        cout << S << " ";
    }
}

// Driver Code
int main()
{
    int N = 25;
    SubMasks(N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program for above approach
import java.util.*;
class GFG
{

// Function to print the submasks of N
static void SubMasks(int N)
{
    for (int S = N; S > 0; S = (S - 1) & N)
    {
        System.out.print(S + " ");
    }
}

// Driver Code
public static void main(String args[])
{
    int N = 25;
    SubMasks(N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to print the submasks of N
def SubMasks(N) :
    S = N
    while S > 0:
        print(S,end=' ')
        S = (S - 1) & N

# Driven Code
if __name__ == '__main__':
    N = 25
    SubMasks(N)

    # This code is contributed by bgangwar59.
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to print the submasks of N
static void SubMasks(int N)
{
    for (int S = N; S > 0; S = (S - 1) & N)
    {
        Console.Write(S + " ");
    }
}

// Driver Code
static public void Main()
{
    int N = 25;
    SubMasks(N);
}
}

// This code is contributed by Code_hunt.
```

## **java 描述语言**

```
<script>

// JavaScript program of the above approach

// Function to print the submasks of N
function SubMasks(N)
{
    for (let S = N; S > 0; S = (S - 1) & N)
    {
        document.write(S + " ");
    }
}

    // Driver Code

    let N = 25;
    SubMasks(N);

</script>
```

****Output:** 

```
25 24 17 16 9 8 1
```** 

*****时间复杂度:**O(2<sup>(N 中设置位计数)</sup>)*
*T8】辅助空间: O(1)***