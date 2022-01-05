# 查找下一个稀疏编号

> 原文:[https://www . geesforgeks . org/给定号码-查找-下一个-稀疏号码/](https://www.geeksforgeeks.org/given-a-number-find-next-sparse-number/)

如果一个数的二进制表示中没有两个相邻的 1，那么这个数就是稀疏的。例如，5(二进制表示:101)是稀疏的，但是 6(二进制表示:110)不是稀疏的。
给定一个数 x，求大于或等于 x 的最小稀疏数

**示例:**

```
Input: x = 6
Output: Next Sparse Number is 8

Input: x = 4
Output: Next Sparse Number is 4

Input: x = 38
Output: Next Sparse Number is 40

Input: x = 44
Output: Next Sparse Number is 64
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/next-sparse-binary-number0029/1)

一个**简单的解决方案**是做以下事情:

```
1) Write a utility function isSparse(x) that takes a number 
   and returns true if x is sparse, else false.  This function
   can be easily written by traversing the bits of input number.
2) Start from x and do following 
   while(1)
   {
      if (isSparse(x))
         return x;
      else 
         x++
   }
```

isSparse()的时间复杂度为 O(Log x)。这个解决方案的时间复杂度是 O(x Log x)。下一个稀疏数最多可以有 O(x)个距离。
感谢 **kk_angel** 提出上述解决方案。

一个**有效的解决方案**可以解决这个问题，而不用逐个检查所有的数字。以下是步骤。

```
1) Find binary of the given number and store it in a 
   boolean array.
2) Initialize last_finalized bit position as 0.
2) Start traversing the binary from least significant bit.
    a) If we get two adjacent 1's such that next (or third) 
       bit is not 1, then 
          (i)  Make all bits after this 1 to last finalized
               bit (including last finalized) as 0\. 
          (ii) Update last finalized bit as next bit. 
```

例如，让二进制表示为 010100010 **11** 101，我们将其更改为 01010001 **100000** (高亮 11 后的所有位都设置为 0)。同样，两个 1 是相邻的，因此将二进制表示更改为 010100**1000000**。这是我们的最终答案。

下面是上述解决方案的实现。

## C++

```
// C++ program to find next sparse number
#include<bits/stdc++.h>
using namespace std;

int nextSparse(int x)
{
    // Find binary representation of x and store it in bin[].
    // bin[0] contains least significant bit (LSB), next
    // bit is in bin[1], and so on.
    vector<bool> bin;
    while (x != 0)
    {
        bin.push_back(x&1);
        x >>= 1;
    }

    // There my be extra bit in result, so add one extra bit
    bin.push_back(0);
    int n = bin.size();  // Size of binary representation

    // The position till which all bits are finalized
    int last_final = 0;

    // Start from second bit (next to LSB)
    for (int i=1; i<n-1; i++)
    {
       // If current bit and its previous bit are 1, but next
       // bit is not 1.
       if (bin[i] == 1 && bin[i-1] == 1 && bin[i+1] != 1)
       {
            // Make the next bit 1
            bin[i+1] = 1;

            // Make all bits before current bit as 0 to make
            // sure that we get the smallest next number
            for (int j=i; j>=last_final; j--)
                bin[j] = 0;

            // Store position of the bit set so that this bit
            // and bits before it are not changed next time.
            last_final = i+1;
        }
    }

    // Find decimal equivalent of modified bin[]
    int ans = 0;
    for (int i =0; i<n; i++)
        ans += bin[i]*(1<<i);
    return ans;
}

// Driver program
int main()
{
    int x = 38;
    cout << "Next Sparse Number is " << nextSparse(x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find next sparse number
import java.util.*;

class GFG{
static int nextSparse(int x)
{
    // Find binary representation of x and store it in bin.get(].
    // bin.get(0] contains least significant bit (LSB), next
    // bit is in bin.get(1], and so on.
    ArrayList<Integer> bin = new ArrayList<Integer>();
    while (x != 0)
    {
        bin.add(x&1);
        x >>= 1;
    }

    // There my be extra bit in result, so add one extra bit
    bin.add(0);
    int n = bin.size(); // Size of binary representation

    // The position till which all bits are finalized
    int last_final = 0;

    // Start from second bit (next to LSB)
    for (int i=1; i<n-1; i++)
    {
    // If current bit and its previous bit are 1, but next
    // bit is not 1.
    if (bin.get(i) == 1 && bin.get(i-1) == 1 && bin.get(i+1) != 1)
    {
            // Make the next bit 1
            bin.set(i+1,1);

            // Make all bits before current bit as 0 to make
            // sure that we get the smallest next number
            for (int j=i; j>=last_final; j--)
                bin.set(j,0);

            // Store position of the bit set so that this bit
            // and bits before it are not changed next time.
            last_final = i+1;
        }
    }

    // Find decimal equivalent of modified bin.get(]
    int ans = 0;
    for (int i =0; i<n; i++)
        ans += bin.get(i)*(1<<i);
    return ans;
}

// Driver program
public static void main(String[] args)
{
    int x = 38;
    System.out.println("Next Sparse Number is "+nextSparse(x));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find next
# sparse number

def nextSparse(x):

    # Find binary representation of
    # x and store it in bin[].
    # bin[0] contains least significant
    # bit (LSB), next bit is in bin[1],
    # and so on.
    bin = []
    while (x != 0):
        bin.append(x & 1)
        x >>= 1

    # There my be extra bit in result,
    # so add one extra bit
    bin.append(0)
    n = len(bin) # Size of binary representation

    # The position till which all
    # bits are finalized
    last_final = 0

    # Start from second bit (next to LSB)
    for i in range(1,n - 1):

        # If current bit and its previous
        # bit are 1, but next bit is not 1.
        if ((bin[i] == 1 and bin[i - 1] == 1
            and bin[i + 1] != 1)):

            # Make the next bit 1
            bin[i + 1] = 1

            # Make all bits before current
            # bit as 0 to make sure that
            # we get the smallest next number
            for j in range(i,last_final-1,-1):
                bin[j] = 0

            # Store position of the bit set
            # so that this bit and bits
            # before it are not changed next time.
            last_final = i + 1

    # Find decimal equivalent
    # of modified bin[]
    ans = 0
    for i in range(n):
        ans += bin[i] * (1 << i)
    return ans

# Driver Code
if __name__=='__main__':
    x = 38
    print("Next Sparse Number is",nextSparse(x))

# This code is contributed by
# mits
```

## C#

```
// C# program to find next sparse number
using System;
using System.Collections;

class GFG{
static int nextSparse(int x)
{
    // Find binary representation of x and store it in bin.get(].
    // bin.get(0] contains least significant bit (LSB), next
    // bit is in bin.get(1], and so on.
    ArrayList bin = new ArrayList();
    while (x != 0)
    {
        bin.Add(x&1);
        x >>= 1;
    }

    // There my be extra bit in result, so add one extra bit
    bin.Add(0);
    int n = bin.Count; // Size of binary representation

    // The position till which all bits are finalized
    int last_final = 0;

    // Start from second bit (next to LSB)
    for (int i = 1; i < n-1; i++)
    {
    // If current bit and its previous bit are 1, but next
    // bit is not 1.
    if ((int)bin[i] == 1 && (int)bin[i-1] == 1 && (int)bin[i+1] != 1)
    {
            // Make the next bit 1
            bin[i+1]=1;

            // Make all bits before current bit as 0 to make
            // sure that we get the smallest next number
            for (int j = i; j >= last_final; j--)
                bin[j]=0;

            // Store position of the bit set so that this bit
            // and bits before it are not changed next time.
            last_final = i + 1;
        }
    }

    // Find decimal equivalent of modified bin.get(]
    int ans = 0;
    for (int i = 0; i < n; i++)
        ans += (int)bin[i]*(1<<i);
    return ans;
}

// Driver program
static void Main()
{
    int x = 38;
    Console.WriteLine("Next Sparse Number is "+nextSparse(x));
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find next sparse number

function nextSparse($x)
{
    // Find binary representation of
    // x and store it in bin[].
    // bin[0] contains least significant
    // bit (LSB), next bit is in bin[1],
    // and so on.
    $bin = array();
    while ($x != 0)
    {
        array_push($bin, $x & 1);
        $x >>= 1;
    }

    // There my be extra bit in result,
    // so add one extra bit
    array_push($bin, 0);
    $n = count($bin); // Size of binary representation

    // The position till which all
    // bits are finalized
    $last_final = 0;

    // Start from second bit (next to LSB)
    for ($i = 1; $i < $n - 1; $i++)
    {
    // If current bit and its previous
    // bit are 1, but next bit is not 1.
    if ($bin[$i] == 1 &&
        $bin[$i - 1] == 1 &&
        $bin[$i + 1] != 1)
    {
        // Make the next bit 1
        $bin[$i + 1] = 1;

        // Make all bits before current
        // bit as 0 to make sure that
        // we get the smallest next number
        for ($j = $i; $j >= $last_final; $j--)
            $bin[$j] = 0;

        // Store position of the bit set
        // so that this bit and bits
        // before it are not changed next time.
        $last_final = $i + 1;
    }
    }

    // Find decimal equivalent
    // of modified bin[]
    $ans = 0;
    for ($i = 0; $i < $n; $i++)
        $ans += $bin[$i] * (1 << $i);
    return $ans;
}

// Driver Code
$x = 38;
echo "Next Sparse Number is " .
                nextSparse($x);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find next sparse number
function nextSparse(x)
{

    // Find binary representation of
    // x and store it in bin[].
    // bin[0] contains least significant
    // bit (LSB), next bit is in bin[1],
    // and so on.
    let bin = new Array();
    while (x != 0)
    {
        bin.push(x & 1);
        x >>= 1;
    }

    // There my be extra bit in result,
    // so add one extra bit
    bin.push(0);

    // Size of binary representation
    n = bin.length;

    // The position till which all
    // bits are finalized
    let last_final = 0;

    // Start from second bit (next to LSB)
    for(let i = 1; i < n - 1; i++)
    {

        // If current bit and its previous
        // bit are 1, but next bit is not 1.
        if (bin[i] == 1 &&
            bin[i - 1] == 1 &&
            bin[i + 1] != 1)
        {

            // Make the next bit 1
            bin[i + 1] = 1;

            // Make all bits before current
            // bit as 0 to make sure that
            // we get the smallest next number
            for(let j = i; j >= last_final; j--)
                bin[j] = 0;

            // Store position of the bit set
            // so that this bit and bits
            // before it are not changed next time.
            last_final = i + 1;
        }
    }

    // Find decimal equivalent
    // of modified bin[]
    let ans = 0;
    for(let i = 0; i < n; i++)
        ans += bin[i] * (1 << i);

    return ans;
}

// Driver Code
let x = 38;
document.write("Next Sparse Number is " +
               nextSparse(x));

// This code is contributed by gfgking

</script>
```

**输出:**

```
Next Sparse Number is 40
```

这个解决方案的时间复杂度是 O(Log x)。

辅助空间:O(log x)
感谢 **gccode** 提出上述解决方案。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。