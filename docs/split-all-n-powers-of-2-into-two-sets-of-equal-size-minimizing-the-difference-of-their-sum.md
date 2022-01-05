# 将 2 的 N 次方分成两个子集，使得它们的和之差最小

> 原文:[https://www . geeksforgeeks . org/将所有 n 的 2 次方拆分为两组大小相等的最小和差/](https://www.geeksforgeeks.org/split-all-n-powers-of-2-into-two-sets-of-equal-size-minimizing-the-difference-of-their-sum/)

给定一个偶数 **N** ，任务是将 2 的所有 **N** [次幂分成两组，使得它们之和的差值最小。
**举例:**](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) 

> **输入:** n = 4
> **输出:** 6
> **解释:**
> 这里 n = 4 表示我们有 2 <sup>1</sup> ，2 <sup>2</sup> ，2 <sup>3</sup> ，2 <sup>4</sup> 。将它分成两个元素相等的组的最佳方式是一组中的 2 <sup>4</sup> + 2 <sup>1</sup> 和另一组中的 2 <sup>2</sup> + 2 <sup>3</sup> ，给出最小可能差 6。
> **输入:** n = 8
> **输出:** 30
> **解释:**
> 这里 n = 8 表示我们有 2 <sup>1</sup> ，2 <sup>2</sup> ，2 <sup>3</sup> ，2 <sup>4</sup> ，2 <sup>5</sup> ，2 <sup>6</sup> ，2 <sup>7 将它分成两个元素相等的组的最佳方式是一组中的 2<sup>8</sup>+2<sup>1</sup>+2<sup>2</sup>+2<sup>3</sup>和另一组中的 2<sup>4</sup>+2<sup>5</sup>+2<sup>6</sup>+2<sup>7</sup>，给出 30 的最小可能差值。</sup>

**方法:**要解决上述问题，我们必须遵循以下步骤:

*   在第一组中添加最大的元素，即**2<sup>N</sup>T3。**
*   在一组中添加第一个数字后，在该组中再添加**N/2–1**个元素，其中元素必须从 2 的最小幂开始或从序列的开始开始。
    **例如**:如果 N = 4，则在第一组中增加 2 <sup>4</sup> ，并增加**N/2–1**，即在该组中增加 1 个元素，这是最少的，这意味着是 2 <sup>1</sup> 。
*   序列的剩余元素形成第二组的元素。
*   计算两个组的总和，然后找出组之间的绝对差，最终将是最小值。

以下是上述方法的实现:

## C++

```
// C++ program to find the minimum
// difference possible by splitting
// all powers of 2 up to N into two
// sets of equal size
#include<bits/stdc++.h>
using namespace std;

void MinDiff(int n)
{

    // Store the largest
    int val = pow(2, n);

    // Form two separate groups
    int sep = n / 2;

    // Initialize the sum
    // for two groups as 0
    int grp1 = 0;
    int grp2 = 0;

    // Insert 2 ^ n in the
    // first group
    grp1 = grp1 + val;

    // Calculate the sum of
    // least n / 2 -1 elements
    // added to the first set
    for(int i = 1; i < sep; i++)
       grp1 = grp1 + pow(2, i);

    // Sum of remaining
    // n / 2 - 1 elements
    for(int i = sep; i < n; i++)
       grp2 = grp2 + pow(2, i);

    // Min Difference between
    // the two groups
    cout << (abs(grp1 - grp2));
}

// Driver code
int main()
{
    int n = 4;
    MinDiff(n);
}

// This code is contributed by Bhupendra_Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// difference possible by splitting
// all powers of 2 up to N into two 
// sets of equal size 
import java.lang.Math;

class GFG{

public static void MinDiff(int n)
{

    // Store the largest
    int val = (int)Math.pow(2, n);

    // Form two separate groups
    int sep = n / 2;

    // Initialize the sum
    // for two groups as 0
    int grp1 = 0;
    int grp2 = 0;

    // Insert 2 ^ n in the
    // first group
    grp1 = grp1 + val;

    // Calculate the sum of
    // least n / 2 -1 elements
    // added to the first set
    for(int i = 1; i < sep; i++)
       grp1 = grp1 + (int)Math.pow(2, i);

    // Sum of remaining
    // n / 2 - 1 elements
    for(int i = sep; i < n; i++)
       grp2 = grp2 + (int)Math.pow(2, i);

    // Min difference between
    // the two groups
    System.out.println(Math.abs(grp1 - grp2));
}

// Driver Code
public static void main(String args[])
{
    int n = 4;

    MinDiff(n);
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# difference possible by splitting
# all powers of 2 up to N into two
# sets of equal size 

def MinDiff(n):

    # Store the largest
    val = 2 ** n

    # Form two separate groups
    sep = n // 2

    # Initialize the sum
    # for two groups as 0
    grp1 = 0
    grp2 = 0

    # Insert 2 ^ n in the
    # first group
    grp1 = grp1 + val

    # Calculate the sum of
    # least n / 2 -1 elements
    # added to the first set
    for i in range(1, sep):
        grp1 = grp1 + 2 ** i

    # sum of remaining
    # n / 2 - 1 elements
    for i in range(sep, n):
        grp2 = grp2 + 2 ** i

    # Min Difference between
    # the two groups
    print(abs(grp1 - grp2))    

# Driver code
if __name__=='__main__':
    n = 4
    MinDiff(n)
```

## C#

```
// C# program to find the minimum
// difference possible by splitting
// all powers of 2 up to N into two
// sets of equal size
using System;
class GFG{

public static void MinDiff(int n)
{

    // Store the largest
    int val = (int)Math.Pow(2, n);

    // Form two separate groups
    int sep = n / 2;

    // Initialize the sum
    // for two groups as 0
    int grp1 = 0;
    int grp2 = 0;

    // Insert 2 ^ n in the
    // first group
    grp1 = grp1 + val;

    // Calculate the sum of
    // least n / 2 -1 elements
    // added to the first set
    for(int i = 1; i < sep; i++)
    grp1 = grp1 + (int)Math.Pow(2, i);

    // Sum of remaining
    // n / 2 - 1 elements
    for(int i = sep; i < n; i++)
    grp2 = grp2 + (int)Math.Pow(2, i);

    // Min difference between
    // the two groups
    Console.Write(Math.Abs(grp1 - grp2));
}

// Driver Code
public static void Main()
{
    int n = 4;

    MinDiff(n);
}
}

// This code is contributed by Akanksha_Rai
```

## java 描述语言

```
<script>
// javascript program to find the minimum
// difference possible by splitting
// all powers of 2 up to N into two 
// sets of equal size 

    function MinDiff(n)
    {

        // Store the largest
        var val = parseInt( Math.pow(2, n));

        // Form two separate groups
        var sep = n / 2;

        // Initialize the sum
        // for two groups as 0
        var grp1 = 0;
        var grp2 = 0;

        // Insert 2 ^ n in the
        // first group
        grp1 = grp1 + val;

        // Calculate the sum of
        // least n / 2 -1 elements
        // added to the first set
        for (i = 1; i < sep; i++)
            grp1 = grp1 + parseInt( Math.pow(2, i));

        // Sum of remaining
        // n / 2 - 1 elements
        for (i = sep; i < n; i++)
            grp2 = grp2 + parseInt( Math.pow(2, i));

        // Min difference between
        // the two groups
        document.write(Math.abs(grp1 - grp2));
    }

    // Driver Code
        var n = 4;
        MinDiff(n);

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
6
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*