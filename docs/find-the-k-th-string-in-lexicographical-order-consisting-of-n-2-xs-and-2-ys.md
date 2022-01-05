# 按照由 n-2 个 X 和 2 个 Y 组成的字典顺序找到第 k 个字符串

> 原文:[https://www . geeksforgeeks . org/find-the-k-th-string-in-coding-n-2-xs-and-2-ys/](https://www.geeksforgeeks.org/find-the-k-th-string-in-lexicographical-order-consisting-of-n-2-xs-and-2-ys/)

给定两个数字 **N** 和 **K** ，如果起始字符串首先包含 **(N-2) x 的**，然后包含 **2 Y 的**
**注:**

> 1 ≤ K ≤ N*(N-1)/2，N*(N-1)/2 为可能的排列数量

**例:**

> **输入:** N = 5，K = 7
> **输出:**yxxy
> 按字典顺序排列的可能字符串
> 1。XXXYY
> 2。xxxy
> 3。XXYYX
> 4。XYXXY
> 5。XYXX
> 6。XYYXX
> 7。yxxy
> 8。yxyx
> 9。yxxx
> 10。YYXXX
> **输入:** N = 8，K = 20
> **输出:**xyxxxx

**接近** :
为了找到 **k <sup>th</sup>** 位置字符串，我们必须遵循以下步骤-

1.  我们必须通过迭代从 **n-2** 到 **0** 的所有位置来找到**‘Y’**最左边出现的位置。
2.  现在迭代的时候，如果 **k < =n-i-1** 那么这就是**‘Y’**最左边出现的必选位置，最右边出现的位置是 **n-k** 这样就可以打印答案了。
3.  否则，让我们用 **n-i-1** 减少 **k** ，即去掉当前位置最左边**‘Y’**的所有弦，进入下一个位置。这样，我们按照字典顺序考虑所有可能的字符串。

**以下是上述办法的实施情况。**

## C++

```
// C++ program find the Kth string in
// lexicographical order consisting
// of N-2 x’s and 2 y’s
#include <bits/stdc++.h>
using namespace std;

// Function to find the Kth string
// in lexicographical order which
// consists of N-2 x’s and 2 y’s
void kth_string(int n, int k)
{
    // Iterate for all possible positions of
    // Left most Y
    for (int i = n - 2; i >= 0; i--) {
        // If i is the left most position of Y
        if (k <= (n - i - 1)) {
            // Put Y in their positions
            for (int j = 0; j < n; j++) {
                if (j == i or j == n - k)
                    cout << 'Y';
                else
                    cout << 'X';
            }

            break;
        }
        k -= (n - i - 1);
    }
}

// Driver code
int main()
{
    int n = 5, k = 7;

    // Function call
    kth_string(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program find the Kth String in
// lexicographical order consisting
// of N-2 x’s and 2 y’s
class GFG{

// Function to find the Kth String
// in lexicographical order which
// consists of N-2 x’s and 2 y’s
static void kth_String(int n, int k)
{

    // Iterate for all possible
    // positions of eft most Y
    for(int i = n - 2; i >= 0; i--)
    {
       // If i is the left
       // most position of Y
       if (k <= (n - i - 1))
       {
           // Put Y in their positions
           for(int j = 0; j < n; j++)
           {
              if (j == i || j == n - k)
                  System.out.print('Y');
              else
                  System.out.print('X');
           }

            break;
        }

        k -= (n - i - 1);
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 5, k = 7;

    // Function call
    kth_String(n, k);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program find the Kth string in
# lexicographical order consisting
# of N-2 x’s and 2 y’s

# Function to find the Kth string
# in lexicographical order which
# consists of N-2 x’s and 2 y’s
def kth_string(n, k):

    # Iterate for all possible positions of
    # left most Y
    for i in range(n - 2, -1, -1):

        # If i is the left most position of Y
        if k <= (n - i - 1):

            # Put Y in their positions
            for j in range(n):
                if (j == i or j == n - k):
                    print('Y', end = "")
                else:
                    print('X', end = "")
            break

        k -= (n - i - 1)

# Driver code
n = 5
k = 7

# Function call
kth_string(n, k)

# This code is contributed by divyamohan123
```

## C#

```
// C# program find the Kth String in
// lexicographical order consisting
// of N-2 x’s and 2 y’s
using System;

class GFG{

// Function to find the Kth String
// in lexicographical order which
// consists of N-2 x’s and 2 y’s
static void kth_String(int n, int k)
{

    // Iterate for all possible
    // positions of eft most Y
    for(int i = n - 2; i >= 0; i--)
    {

       // If i is the left
       // most position of Y
       if (k <= (n - i - 1))
       {

           // Put Y in their positions
           for(int j = 0; j < n; j++)
           {
               if (j == i || j == n - k)
                   Console.Write('Y');
               else
                   Console.Write('X');
           }
           break;
       }
       k -= (n - i - 1);
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 5, k = 7;

    // Function call
    kth_String(n, k);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program find the Kth String in
// lexicographical order consisting
// of N-2 x’s and 2 y’s

// Function to find the Kth String
// in lexicographical order which
// consists of N-2 x’s and 2 y’s
function kth_String(n , k)
{

    // Iterate for all possible
    // positions of eft most Y
    for(i = n - 2; i >= 0; i--)
    {
       // If i is the left
       // most position of Y
       if (k <= (n - i - 1))
       {
           // Put Y in their positions
           for(j = 0; j < n; j++)
           {
              if (j == i || j == n - k)
                  document.write('Y');
              else
                  document.write('X');
           }
            break;
        }   
        k -= (n - i - 1);
    }
}

// Driver code
var n = 5, k = 7;

// Function call
kth_String(n, k);

// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
YXXXY
```