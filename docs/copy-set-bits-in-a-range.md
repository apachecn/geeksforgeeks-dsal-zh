# 在一个范围内复制设定位

> 原文:[https://www.geeksforgeeks.org/copy-set-bits-in-a-range/](https://www.geeksforgeeks.org/copy-set-bits-in-a-range/)

给定两个数字 x 和 y，以及一个范围[l，r]，其中 1 <= l, r <= 32\. The task is consider set bits of y in range [l, r] and set these bits in x also.
示例:

```
Input  : x = 10, y = 13, l = 2, r = 3
Output : x = 14
Binary representation of 10 is 1010 and 
that of y is 1101\. There is one set bit
in y at 3'rd position (in given range). 
After we copy this bit to x, x becomes 1110
which is binary representation of 14.

Input  : x = 8, y = 7, l = 1, r = 2
Output : x = 11
```

来源:[D·E·肖访谈](https://www.geeksforgeeks.org/d-e-shaw-interview-experience-set-16-on-campus-for-internship/)

**方法 1(一个一个复制位)**
我们可以通过遍历给定的范围，一个一个找到 y 的集合位。对于每个设置的位，我们将它与 x 的现有位进行 or 运算，这样，如果没有设置，它就会在 x 中设置。下面是 C++实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to rearrange array in alternating
// C++ program to copy set bits in a given
// range [l, r] from y to x.
#include <bits/stdc++.h>
using namespace std;

// Copy set bits in range [l, r] from y to x.
// Note that x is passed by reference and modified
// by this function.
void copySetBits(unsigned &x, unsigned y,
                 unsigned l, unsigned r)
{
   // l and r must be between 1 to 32
   // (assuming ints are stored using
   //  32 bits)
   if (l < 1 || r > 32)
      return ;

   // Traverse in given range
   for (int i=l; i<=r; i++)
   {
       // Find a mask (A number whose
       // only set bit is at i'th position)
       int mask = 1 << (i-1);

       // If i'th bit is set in y, set i'th
       // bit in x also.
       if (y & mask)
          x = x | mask;
   }
}

// Driver code
int main()
{
   unsigned x = 10, y = 13, l = 1, r = 32;
   copySetBits(x, y, l, r);
   cout << "Modified x is " << x;
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearrange array in alternating
// Java program to copy set bits in a given
// range [l, r] from y to x.
import java.util.*;

class GFG{

// Copy set bits in range [l, r] from y to x.
// Note that x is passed by reference and modified
// by this function.
static int copySetBits(int x, int y,
                 int l, int r)
{
   // l and r must be between 1 to 32
   // (assuming ints are stored using
   //  32 bits)
   if (l < 1 || r > 32)
      return x;

   // Traverse in given range
   for (int i = l; i <= r; i++)
   {
       // Find a mask (A number whose
       // only set bit is at i'th position)
       int mask = 1 << (i-1);

       // If i'th bit is set in y, set i'th
       // bit in x also.
       if ((y & mask)!=0)
          x = x | mask;
   }

   return x;
}

// Driver code
public static void main(String[] args)
{
   int x = 10, y = 13, l = 1, r = 32;
  x = copySetBits(x, y, l, r);
   System.out.print("Modified x is " +  x);
}
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# Python program to rearrange array in alternating
# Python program to copy set bits in a given
# range [l, r] from y to x.

# Copy set bits in range [l, r] from y to x.
# Note that x is passed by reference and modified
# by this function.
def copySetBits(x, y, l, r):

    # l and r must be between 1 to 32
    # (assuming ints are stored using
    # 32 bits)
    if (l < 1 or r > 32):
        return x;

    # Traverse in given range
    for i in range(l, r + 1):

        # Find a mask (A number whose
        # only set bit is at i'th position)
        mask = 1 << (i - 1);

        # If i'th bit is set in y, set i'th
        # bit in x also.
        if ((y & mask) != 0):
            x = x | mask;
    return x;

# Driver code
if __name__ == '__main__':
    x = 10;
    y = 13;
    l = 1;
    r = 32;
    x = copySetBits(x, y, l, r);
    print("Modified x is ", x);

# This code is contributed by gauravrajput1
```

## C#

```
// C# program to rearrange array in alternating
// C# program to copy set bits in a given
// range [l, r] from y to x.
using System;

public class GFG {

    // Copy set bits in range [l, r] from y to x.
    // Note that x is passed by reference and modified
    // by this function.
    static int copySetBits(int x, int y, int l, int r)
    {

        // l and r must be between 1 to 32
        // (assuming ints are stored using
        // 32 bits)
        if (l < 1 || r > 32)
            return x;

        // Traverse in given range
        for (int i = l; i <= r; i++)
        {

            // Find a mask (A number whose
            // only set bit is at i'th position)
            int mask = 1 << (i - 1);

            // If i'th bit is set in y, set i'th
            // bit in x also.
            if ((y & mask) != 0)
                x = x | mask;
        }

        return x;
    }

    // Driver code
    public static void Main(String[] args) {
        int x = 10, y = 13, l = 1, r = 32;
        x = copySetBits(x, y, l, r);
        Console.Write("Modified x is " + x);
    }
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>
// javascript program to rearrange array in alternating
// javascript program to copy set bits in a given
// range [l, r] from y to x.

    // Copy set bits in range [l, r] from y to x.
    // Note that x is passed by reference and modified
    // by this function.
    function copySetBits(x , y , l , r)
    {

        // l and r must be between 1 to 32
        // (assuming ints are stored using
        // 32 bits)
        if (l < 1 || r > 32)
            return x;

        // Traverse in given range
        for (i = l; i <= r; i++)
        {

            // Find a mask (A number whose
            // only set bit is at i'th position)
            var mask = 1 << (i - 1);

            // If i'th bit is set in y, set i'th
            // bit in x also.
            if ((y & mask) != 0)
                x = x | mask;
        }

        return x;
    }

    // Driver code
        var x = 10, y = 13, l = 1, r = 32;
        x = copySetBits(x, y, l, r);
        document.write("Modified x is " + x);

// This code is contributed by gauravrajput1
</script>
```

**Output**

```
Modified x is 15
```