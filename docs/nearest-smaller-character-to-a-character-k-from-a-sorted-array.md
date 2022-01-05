# 排序数组中距离字符 K 最近的较小字符

> 原文:[https://www . geeksforgeeks . org/最近的小字符到字符的 k-from-sorted-array/](https://www.geeksforgeeks.org/nearest-smaller-character-to-a-character-k-from-a-sorted-array/)

给定字符的排序数组 **arr[]** 和字符 **K** ，任务是从给定数组中找到 ASCII 值比 **K** 小的字符。如果没有发现字符的 ASCII 值小于 **K** ，则打印 **-1** 。
**举例:**

> **输入:** arr[] = {'e '，' g '，' t '，' y'}，K = 'u'
> **输出:** t
> **解释:**
> 从' u '开始 ASCII 值最近的较小字符是' t '。
> **输入:** arr[] = {'e '，' g '，' t '，' y'}，K = 'a'
> **输出:** -1
> **说明:**
> 不存在 ASCII 值小于' a '的字符。

**天真方法:**
解决问题最简单的方法是遍历数组，找到 ASCII 值小于 **K** 的字符，它们的 ASCII 值之差最小。
***时间复杂度:** O(N)*
***辅助空间:** O(1)*
**高效进场:**
思路是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找出[楼](https://www.geeksforgeeks.org/floor-in-a-sorted-array/)元素(最大字符刚好比关键小)。按照以下步骤解决问题:

*   在阵列上执行二分搜索法。
*   检查当前中间元素( **mid** )是否等于字符 ***K*** 。
*   如果是这样，那么将 **start** 设置为**mid–1**，因为我们只需要找到较小的元素。
*   如果**arr【mid】**比 *K* 小**，则将其存储在某个变量中，比如 ***ch*** 。将**开始**设置为**中间+ 1** 以搜索更靠近 **K** 的较小字符。**
*   **否则，将**终点**设置为**1 中**。**
*   **继续重复以上步骤。最后，打印完成搜索后获得的字符。如果没有得到字符，打印 **-1** 。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// nearest smaller character
char bs(char ar[], int n, int ele)
{
    int start = 0;
    int end = n - 1;

    // Stores the nearest smaller
    // character
    char ch = '@';

    // Iterate till starts cross end
    while (start <= end) {

        // Find the mid element
        int mid = start + (end - start) / 2;

        // Check if K is found
        if (ar[mid] == ele)
            end = mid - 1;

        // Check if current character
        // is less than K
        else if (ar[mid] < ele) {
            ch = ar[mid];

            // Increment the start
            start = mid + 1;
        }

        // Otherwise
        else

            // Increment end
            end = mid - 1;
    }
    // Return the character
    return ch;
}

// Driver Code
int main()
{
    char ar[] = { 'e', 'g', 't', 'y' };
    int n = sizeof(ar) / sizeof(ar[0]);

    char K = 'u';

    char ch = bs(ar, n, K);

    if (ch == '@')
        cout << "-1";
    else
        cout << ch;

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to return the
// nearest smaller character
static char bs(char ar[], int n, int ele)
{
    int start = 0;
    int end = n - 1;

    // Stores the nearest smaller
    // character
    char ch = '@';

    // Iterate till starts cross end
    while (start <= end)
    {

        // Find the mid element
        int mid = start + (end - start) / 2;

        // Check if K is found
        if (ar[mid] == ele)
            end = mid - 1;

        // Check if current character
        // is less than K
        else if (ar[mid] < ele)
        {
            ch = ar[mid];

            // Increment the start
            start = mid + 1;
        }

        // Otherwise
        else

            // Increment end
            end = mid - 1;
    }

    // Return the character
    return ch;
}

// Driver Code
public static void main(String[] args)
{
    char ar[] = { 'e', 'g', 't', 'y' };
    int n = ar.length;

    char K = 'u';

    char ch = bs(ar, n, K);

    if (ch == '@')
        System.out.print("-1");
    else
        System.out.print(ch);
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach

# Function to return the
# nearest smaller character
def bs(a, n, ele):

    start = 0
    end = n - 1

    # Stores the nearest smaller
    # character
    ch = '@'

    # Iterate till starts cross end
    while (start <= end):

        # Find the mid element
        mid = start + (end - start) // 2;

        # Check if K is found
        if(ar[mid] == ele):
            end = mid - 1

        # Check if current character
        # is less than K
        elif(ar[mid] < ele):
            ch = ar[mid]

            # Increment the start
            start = mid + 1;

        # Otherwise
        else:

            # Increment end
            end = mid - 1;

    # Return the character
    return ch

# Driver code
if __name__=='__main__':

    ar = [ 'e', 'g', 't', 'y' ]
    n = len(ar)
    K = 'u';

    ch = bs(ar, n, K);

    if (ch == '@'):
        print('-1')
    else:
        print(ch)

# This code is contributed by rutvik_56
```

## **C#**

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to return the
// nearest smaller character
static char bs(char []ar, int n, int ele)
{
    int start = 0;
    int end = n - 1;

    // Stores the nearest smaller
    // character
    char ch = '@';

    // Iterate till starts cross end
    while (start <= end)
    {

        // Find the mid element
        int mid = start + (end - start) / 2;

        // Check if K is found
        if (ar[mid] == ele)
            end = mid - 1;

        // Check if current character
        // is less than K
        else if (ar[mid] < ele)
        {
            ch = ar[mid];

            // Increment the start
            start = mid + 1;
        }

        // Otherwise
        else

            // Increment end
            end = mid - 1;
    }

    // Return the character
    return ch;
}

// Driver Code
public static void Main(String[] args)
{
    char []ar = { 'e', 'g', 't', 'y' };
    int n = ar.Length;

    char K = 'u';
    char ch = bs(ar, n, K);

    if (ch == '@')
        Console.Write("-1");
    else
        Console.Write(ch);
}
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to return the
// nearest smaller letacter
function bs(ar, n, ele)
{
    let start = 0;
    let end = n - 1;

    // Stores the nearest smaller
    // letacter
    let ch = '@';

    // Iterate till starts cross end
    while (start <= end)
    {

        // Find the mid element
        let mid = start + Math.floor((end - start) / 2);

        // Check if K is found
        if (ar[mid] == ele)
            end = mid - 1;

        // Check if current letacter
        // is less than K
        else if (ar[mid] < ele)
        {
            ch = ar[mid];

            // Increment the start
            start = mid + 1;
        }

        // Otherwise
        else

            // Increment end
            end = mid - 1;
    }

    // Return the letacter
    return ch;
}

// Driver Code
    let ar = [ 'e', 'g', 't', 'y' ];
    let n = ar.length;

    let K = 'u';

    let ch = bs(ar, n, K);

    if (ch == '@')
        document.write("-1");
    else
        document.write(ch);

// This code is contributed by sanjoy_62.
</script>
```

****Output:** 

```
t
```** 

*****时间复杂度:** O(logN)*
***辅助空间:** O(1)***