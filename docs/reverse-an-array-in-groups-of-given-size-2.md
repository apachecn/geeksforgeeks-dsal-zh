# 反转给定大小的数组|集合 2(集合 1 的变体)

> 原文:[https://www . geesforgeks . org/reverse-a-a-in-a-group-of-size-2/](https://www.geeksforgeeks.org/reverse-an-array-in-groups-of-given-size-2/)

给定一个数组，反转每个满足给定约束的子数组。
我们已经讨论了一种解决方案，其中我们反转由[集合 1](https://www.geeksforgeeks.org/reverse-an-array-in-groups-of-given-size/) 中的连续 k 个元素形成的每个子阵列。在这一集里，我们将讨论这个问题的各种有趣的变化。

**变异 1(反转交替组):**
反转由连续 k 个元素组成的每个交替子阵列。

**示例:**

```
Input: 
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
k = 3
Output:  
[3, 2, 1, 4, 5, 6, 9, 8, 7]

Input: 
arr = [1, 2, 3, 4, 5, 6, 7, 8]
k = 2
Output:  
[2, 1, 3, 4, 6, 5, 7, 8]
```

以下是实施–

## C++

```
// C++ program to reverse every alternate sub-array
// formed by consecutive k elements
#include <iostream>
using namespace std;

// Function to reverse every alternate sub-array
// formed by consecutive k elements
void reverse(int arr[], int n, int k)
{
    // increment i in multiples of 2*k
    for (int i = 0; i < n; i += 2*k)
    {
        int left = i;

        // to handle case when 2*k is not multiple of n
        int right = min(i + k - 1, n - 1);

        // reverse the sub-array [left, right]
        while (left < right)
            swap(arr[left++], arr[right--]);
    }   
}

// Driver code
int main()
{
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14};
    int k = 3;

    int n = sizeof(arr) / sizeof(arr[0]);

    reverse(arr, n, k);

    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse
// every alternate sub-array
// formed by consecutive k elements
class GFG
{

// Function to reverse every
// alternate sub-array formed
// by consecutive k elements
    static void reverse(int arr[], int n, int k)
    {

        // increment i in multiples of 2*k
        for (int i = 0; i < n; i += 2 * k)
        {
            int left = i;

            // to handle case when 2*k is not multiple of n
            int right = Math.min(i + k - 1, n - 1);

            // reverse the sub-array [left, right]
            while (left < right) {
                swap(arr, left++, right--);
            }
        }
    }

    static int[] swap(int[] array, int i, int j)
    {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
        return array;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 3, 4, 5, 6, 7, 8,
                    9, 10, 11, 12, 13, 14};
        int k = 3;
        int n = arr.length;

        reverse(arr, n, k);
        for (int i = 0; i < n; i++)
        {
            System.out.print(arr[i] + " ");
        }
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to reverse every alternate sub-array
# formed by consecutive k elements

# Function to reverse every alternate sub-array
# formed by consecutive k elements
def reverse(arr, n, k):
    # increment i in multiples of 2*k
    for i in range(0,n,2*k):
        left = i

        # to handle case when 2*k is not multiple of n
        right = min(i + k - 1, n - 1)

        # reverse the sub-array [left, right]
        while (left < right):
            temp = arr[left]
            arr[left] = arr[right]
            arr[right] = temp
            left += 1
            right -= 1

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
    k = 3

    n = len(arr)

    reverse(arr, n, k)

    for i in range(0,n,1):
        print(arr[i],end =" ")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to reverse every alternate
// sub-array formed by consecutive k elements
using System;

class GFG
{

    // Function to reverse every
    // alternate sub-array formed
    // by consecutive k elements
    static void reverse(int []arr,
                        int n, int k)
    {

        // increment i in multiples of 2*k
        for (int i = 0; i < n; i += 2 * k)
        {
            int left = i;

            // to handle case when 2*k is
            // not multiple of n
            int right = Math.Min(i + k - 1, n - 1);

            // reverse the sub-array [left, right]
            while (left < right)
            {
                swap(arr, left++, right--);
            }
        }
    }

    static int[] swap(int[] array, int i, int j)
    {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
        return array;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {1, 2, 3, 4, 5, 6, 7, 8,
                     9, 10, 11, 12, 13, 14};
        int k = 3;
        int n = arr.Length;

        reverse(arr, n, k);
        for (int i = 0; i < n; i++)
        {
            Console.Write(arr[i] + " ");
        }
    }
}

// This code is ontributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to reverse
// every alternate sub-array
// formed by consecutive k elements

// Function to reverse every
// alternate sub-array formed
// by consecutive k elements
function reverse(arr, n, k)
{

    // Increment i in multiples of 2*k
    for(let i = 0; i < n; i += 2 * k)
    {

        let left = i;

        // To handle case when 2*k is
        // not multiple of n
        let right = Math.min(i + k - 1,
                                 n - 1);

        // reverse the sub-array [left, right]
        while (left < right)
        {
            swap(arr, left++, right--);
        }
    }
}

function swap(array, i, j)
{
    let temp = array[i];
    array[i] = array[j];
    array[j] = temp;
    return array;
}

// Driver code
let arr = [ 1, 2, 3, 4, 5, 6, 7, 8,
            9, 10, 11, 12, 13, 14 ];
let k = 3;
let n = arr.length;

reverse(arr, n, k);

for(let i = 0; i < n; i++)
{
    document.write(arr[i] + " ");
}

// This code is contributed by rag2127

</script>
```

**输出:**

```
3 2 1 4 5 6 9 8 7 10 11 12 14 13
```

**变化 2(给定距离反转):**
反转由给定距离的连续 k 个元素形成的每个子阵列。

示例:

```
Input: 
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
k = 3
m = 2
Output:  
[3, 2, 1, 4, 5, 8, 7, 6, 9, 10]

Input: 
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
k = 3
m = 1
Output:  
[3, 2, 1, 4, 7, 6, 5, 8, 10, 9]

Input: 
arr = [1, 2, 3, 4, 5, 6, 7, 8]
k = 2
m = 0
Output:  
[2, 1, 4, 3, 6, 5, 8, 7]
```

以下是它的实现–

## C++

```
// C++ program to reverse every sub-array formed by
// consecutive k elements at given distance apart
#include <iostream>
using namespace std;

// Function to reverse every sub-array formed by
// consecutive k elements at m distance apart
void reverse(int arr[], int n, int k, int m)
{
    // increment i in multiples of k + m
    for (int i = 0; i < n; i += k + m)
    {
        int left = i;

        // to handle case when k + m is not multiple of n
        int right = min(i + k - 1, n - 1);

        // reverse the sub-array [left, right]
        while (left < right)
            swap(arr[left++], arr[right--]);
    }
}

// Driver code
int main()
{
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14};
    int k = 3;
    int m = 2;

    int n = sizeof(arr) / sizeof(arr[0]);

    reverse(arr, n, k, m);

    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to reverse every sub-array formed by
// consecutive k elements at given distance apart
class GFG
{

// Function to reverse every sub-array formed by
// consecutive k elements at m distance apart
static void reverse(int[] arr, int n, int k, int m)
{
    // increment i in multiples of k + m
    for (int i = 0; i < n; i += k + m)
    {
        int left = i;

        // to handle case when k + m is not multiple of n
        int right = Math.min(i + k - 1, n - 1);

        // reverse the sub-array [left, right]
        while (left < right)
            swap(arr,left++, right--);
    }
}
 static int[] swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

// Driver code
 public static void main(String[] args)
    {
        int arr[] = {1, 2, 3, 4, 5, 6, 7, 8,
                    9, 10, 11, 12, 13, 14};
        int k = 3;
        int m = 2;
        int n = arr.length;

        reverse(arr, n, k, m );
        for (int i = 0; i < n; i++)
        {
            System.out.print(arr[i] + " ");
        }
    }
}
// This code has been contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to reverse every
# sub-array formed by consecutive
# k elements at given distance apart

# Function to reverse every
# sub-array formed by consecutive
# k elements at m distance apart
def reverse(arr, n, k, m):

    # increment i in multiples of k + m
    for i in range(0, n, k + m):
        left = i;

        # to handle case when k + m
        # is not multiple of n
        right = min(i + k - 1, n - 1);

        # reverse the sub-array [left, right]
        while (left < right):
            arr = swap(arr,left, right);
            left += 1;
            right -= 1;
    return arr;

def swap(arr, i, j):

    temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;

# Driver code
arr = [1, 2, 3, 4, 5, 6, 7,
       8, 9, 10, 11, 12, 13, 14];
k = 3;
m = 2;
n = len(arr);

arr = reverse(arr, n, k, m );
for i in range(0, n):
    print(arr[i], end = " ");

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to reverse every sub-array
// formed by consecutive k elements at
// given distance apart
using System;

class GFG
{

// Function to reverse every sub-array
// formed by consecutive k elements
// at m distance apart
static void reverse(int[] arr, int n,
                    int k, int m)
{
    // increment i in multiples of k + m
    for (int i = 0; i < n; i += k + m)
    {
        int left = i;

        // to handle case when k + m is
        // not multiple of n
        int right = Math.Min(i + k - 1, n - 1);

        // reverse the sub-array [left, right]
        while (left < right)
            swap(arr, left++, right--);
    }
}

static int[] swap(int[] arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = {1, 2, 3, 4, 5, 6, 7, 8,
                 9, 10, 11, 12, 13, 14};
    int k = 3;
    int m = 2;
    int n = arr.Length;

    reverse(arr, n, k, m );
    for (int i = 0; i < n; i++)
    {
        Console.Write(arr[i] + " ");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript program to reverse every sub-array formed by
// consecutive k elements at given distance apart

// Function to reverse every sub-array formed by
// consecutive k elements at m distance apart
function reverse(arr,n,k,m)
{
    // increment i in multiples of k + m
    for (let i = 0; i < n; i += k + m)
    {
        let left = i;

        // to handle case when k + m is not multiple of n
        let right = Math.min(i + k - 1, n - 1);

        // reverse the sub-array [left, right]
        while (left < right)
            swap(arr,left++, right--);
    }
}

function swap(arr,i,j)
{
    let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
}

// Driver code
let arr=[1, 2, 3, 4, 5, 6, 7, 8,
                    9, 10, 11, 12, 13, 14];
let k = 3;
let m = 2;
let n = arr.length;

reverse(arr, n, k, m );
for (let i = 0; i < n; i++)
{
    document.write(arr[i] + " ");
}

// This code is contributed by ab2127
</script>
```

**输出:**

```
3 2 1 4 5 8 7 6 9 10 13 12 11 14
```

**变化 3(通过将组大小加倍来反转):**
反转由连续的 k 个元素形成的每个子阵列，其中 k 随着每个子阵列自身加倍。

示例:

```
Input: 
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
k = 1
Output:  
[1], [3, 2], [7, 6, 5, 4], [15, 14, 13, 12, 11, 10, 9, 8]
```

以下是它的实现–

## C++

```
// C++ program to reverse every sub-array formed by
// consecutive k elements where k doubles itself with
// every sub-array.
#include <iostream>
using namespace std;

// Function to reverse every sub-array formed by
// consecutive k elements where k doubles itself
// with every sub-array.
void reverse(int arr[], int n, int k)
{
    // increment i in multiples of k where value
    // of k is doubled with each iteration
    for (int i = 0; i < n; i += k/2)
    {
        int left = i;

        // to handle case when number of elements in
        // last group is less than k
        int right = min(i + k - 1, n - 1);

        // reverse the sub-array [left, right]
        while (left < right)
            swap(arr[left++], arr[right--]);

        // double value of k with each iteration
        k = k*2;
    }
}

// Driver code
int main()
{
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16};
    int k = 1;

    int n = sizeof(arr) / sizeof(arr[0]);

    reverse(arr, n, k);

    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse every sub-array
// formed by consecutive k elements where
// k doubles itself with every sub-array.
import java.util.*;

class GFG
{

// Function to reverse every sub-array formed by
// consecutive k elements where k doubles itself
// with every sub-array.
static void reverse(int arr[], int n, int k)
{
    // increment i in multiples of k where value
    // of k is doubled with each iteration
    for (int i = 0; i < n; i += k / 2)
    {
        int left = i;

        // to handle case when number of elements in
        // last group is less than k
        int right = Math.min(i + k - 1, n - 1);

        // reverse the sub-array [left, right]
        while (left < right)
            swap(arr, left++, right--);

        // double value of k with each iteration
        k = k * 2;
    }
}

static int[] swap(int[] arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9,
                10, 11, 12, 13, 14, 15, 16};
    int k = 1;

    int n = arr.length;

    reverse(arr, n, k);

    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to reverse every
# sub-array formed by consecutive
# k elements where k doubles itself
# with every sub-array

# Function to reverse every sub-array
# formed by consecutive k elements
# where k doubles itself with every
# sub-array
def reverse(arr, n, k):

    i = 0

    # Increment i in multiples of k where
    # value of k is doubled with each
    # iteration
    while (i < n):
        left = i

        # To handle case when number of elements
        # in last group is less than k
        right = min(i + k - 1, n - 1)

        # Reverse the sub-array [left, right]
        while (left < right):
            arr[left], arr[right] = arr[right], arr[left]
            left += 1
            right -= 1

        # Double value of k with each iteration
        k = k * 2
        i += int(k / 2)

# Driver code
arr = [ 1, 2, 3, 4, 5, 6, 7, 8, 9,
        10, 11, 12, 13, 14, 15, 16]
k = 1

n = len(arr)

reverse(arr, n, k)

print(*arr, sep = ' ')

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to reverse every sub-array
// formed by consecutive k elements where
// k doubles itself with every sub-array.
using System;

class GFG
{

// Function to reverse every sub-array formed by
// consecutive k elements where k doubles itself
// with every sub-array.
static void reverse(int []arr, int n, int k)
{
    // increment i in multiples of k where value
    // of k is doubled with each iteration
    for (int i = 0; i < n; i += k / 2)
    {
        int left = i;

        // to handle case when number of elements in
        // last group is less than k
        int right = Math.Min(i + k - 1, n - 1);

        // reverse the sub-array [left, right]
        while (left < right)
            swap(arr, left++, right--);

        // double value of k with each iteration
        k = k * 2;
    }
}

static int[] swap(int[] arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = {1, 2, 3, 4, 5, 6, 7, 8, 9,
                10, 11, 12, 13, 14, 15, 16};
    int k = 1;

    int n = arr.Length;

    reverse(arr, n, k);

    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to reverse every sub-array
// formed by consecutive k elements where
// k doubles itself with every sub-array.

// Function to reverse every sub-array formed by
// consecutive k elements where k doubles itself
// with every sub-array.
function reverse(arr,n,k)
{
    // increment i in multiples of k where value
    // of k is doubled with each iteration
    for (let i = 0; i < n; i += k / 2)
    {
        let left = i;

        // to handle case when number of elements in
        // last group is less than k
        let right = Math.min(i + k - 1, n - 1);

        // reverse the sub-array [left, right]
        while (left < right)
            swap(arr, left++, right--);

        // double value of k with each iteration
        k = k * 2;
    }
}

function  swap(arr,i,j)
{
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
let arr=[1, 2, 3, 4, 5, 6, 7, 8, 9,
                10, 11, 12, 13, 14, 15, 16];
let k = 1;
let  n = arr.length;
reverse(arr, n, k);

document.write(arr.join(" "));

// This code is contributed by unknown2108
</script>
```

**输出:**

```
1 3 2 7 6 5 4 15 14 13 12 11 10 9 8 16
```

**上述所有解的时间复杂度**为 O(n)。
**辅助空间**所使用的程序是 O(1)。

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。