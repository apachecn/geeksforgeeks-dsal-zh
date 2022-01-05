# 第 k1 个和第 k2 个最小元素之间所有元素的总和

> 原文:[https://www . geesforgeks . org/sum-elements-k1th-k2th-minist-elements/](https://www.geeksforgeeks.org/sum-elements-k1th-k2th-smallest-elements/)

给定一个整数数组和两个数字 k1 和 k2。求数组中给定的第 k1 个和第 k2 个最小元素之间所有元素的和。可以假设(1 <= k1 < k2 <= n)和数组的所有元素都是不同的。

**示例:**

```
Input : arr[] = {20, 8, 22, 4, 12, 10, 14},  k1 = 3,  k2 = 6  
Output : 26          
         3rd smallest element is 10\. 6th smallest element 
         is 20\. Sum of all element between k1 & k2 is
         12 + 14 = 26

Input : arr[] = {10, 2, 50, 12, 48, 13}, k1 = 2, k2 = 6 
Output : 73 
```

**方法 1(排序)**
首先使用类似[合并排序](http://quiz.geeksforgeeks.org/merge-sort/)、[堆排序](http://quiz.geeksforgeeks.org/heap-sort/)等 O(n log n)排序算法对给定数组进行排序，并返回排序数组中索引 k1 和 k2 之间的所有元素的总和。

下面是上述想法的实现:

## C++

```
// C++ program to find sum of all element between
// to K1'th and k2'th smallest elements in array
#include <bits/stdc++.h>

using namespace std;

// Returns sum between two kth smallest elements of the array
int sumBetweenTwoKth(int arr[], int n, int k1, int k2)
{
    // Sort the given array
    sort(arr, arr + n);

    /* Below code is equivalent to
     int result = 0;
     for (int i=k1; i<k2-1; i++)
      result += arr[i]; */
    return accumulate(arr + k1, arr + k2 - 1, 0);
}

// Driver program
int main()
{
    int arr[] = { 20, 8, 22, 4, 12, 10, 14 };
    int k1 = 3, k2 = 6;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << sumBetweenTwoKth(arr, n, k1, k2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of all element
// between to K1'th and k2'th smallest
// elements in array
import java.util.Arrays;

class GFG {

    // Returns sum between two kth smallest
    // element of array
    static int sumBetweenTwoKth(int arr[],
                                int k1, int k2)
    {
        // Sort the given array
        Arrays.sort(arr);

        // Below code is equivalent to
        int result = 0;

        for (int i = k1; i < k2 - 1; i++)
            result += arr[i];

        return result;
    }

    // Driver code
    public static void main(String[] args)
    {

        int arr[] = { 20, 8, 22, 4, 12, 10, 14 };
        int k1 = 3, k2 = 6;
        int n = arr.length;

        System.out.print(sumBetweenTwoKth(arr,
                                          k1, k2));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find sum of
# all element between to K1'th and
# k2'th smallest elements in array

# Returns sum between two kth
# smallest element of array
def sumBetweenTwoKth(arr, n, k1, k2):

    # Sort the given array
    arr.sort()

    result = 0
    for i in range(k1, k2-1):
        result += arr[i]
    return result

# Driver code
arr = [ 20, 8, 22, 4, 12, 10, 14 ]
k1 = 3; k2 = 6
n = len(arr)
print(sumBetweenTwoKth(arr, n, k1, k2))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find sum of all element
// between to K1'th and k2'th smallest
// elements in array
using System;

class GFG {

    // Returns sum between two kth smallest
    // element of array
    static int sumBetweenTwoKth(int[] arr, int n,
                                int k1, int k2)
    {
        // Sort the given array
        Array.Sort(arr);

        // Below code is equivalent to
        int result = 0;

        for (int i = k1; i < k2 - 1; i++)
            result += arr[i];

        return result;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 20, 8, 22, 4, 12, 10, 14 };
        int k1 = 3, k2 = 6;
        int n = arr.Length;

        Console.Write(sumBetweenTwoKth(arr, n, k1, k2));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of all element between
// to K1'th and k2'th smallest elements in array

// Returns sum between two kth smallest elements of the array
function sumBetweenTwoKth($arr, $n, $k1, $k2)
{
    // Sort the given array
    sort($arr);

    // Below code is equivalent to
        $result = 0;

        for ($i = $k1; $i < $k2 - 1; $i++)
            $result += $arr[$i];

        return $result;
}

// Driver program

    $arr = array( 20, 8, 22, 4, 12, 10, 14 );
    $k1 = 3;
    $k2 = 6;
    $n = count($arr);;
    echo sumBetweenTwoKth($arr, $n, $k1, $k2);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of all element
// between to K1'th and k2'th smallest
// elements in array

// Returns sum between two kth smallest
// element of array
function sumBetweenTwoKth(arr, k1 , k2)
{

    // Sort the given array
    arr.sort(function(a, b){return a - b});

    // Below code is equivalent to
    var result = 0;

    for(var i = k1; i < k2 - 1; i++)
        result += arr[i];

    return result;
}

// Driver code
var arr = [ 20, 8, 22, 4, 12, 10, 14 ];
var k1 = 3, k2 = 6;
var n = arr.length;

document.write(sumBetweenTwoKth(arr,
                                k1, k2));

// This code is contributed by shikhasingrajput

</script>
```

**输出:**

```
 26
```

**时间复杂度** : O(n log n)

**方法 2(使用最小堆)**
我们可以使用最小堆来优化上述解决方案。
1)创建所有数组元素的最小堆。(此步骤需要 O(n)时间)
2)提取最小 k1 次(此步骤需要 O(K1 Log n)时间)
3)提取最小 k2–K1–1 次，并将所有提取的元素求和。(此步骤需要 O((K2–k1)* Log n)时间)

**方法二实施**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

int n = 7;

void minheapify(int a[], int index)
{

    int small = index;
    int l = 2 * index + 1;
    int r = 2 * index + 2;

    if (l < n && a[l] < a[small])
        small = l;

    if (r < n && a[r] < a[small])
        small = r;

    if (small != index) {
        swap(a[small], a[index]);
        minheapify(a, small);
    }
}

int main()
{
    int i = 0;
    int k1 = 3;
    int k2 = 6;

    int a[] = { 20, 8, 22, 4, 12, 10, 14 };

    int ans = 0;

    for (i = (n / 2) - 1; i >= 0; i--) {
        minheapify(a, i);
    }

    // decreasing value by 1 because we want min heapifying k times and it starts
    // from 0 so we have to decrease it 1 time
    k1--;
    k2--;

    // Step 1: Do extract minimum k1 times (This step takes O(K1 Log n) time)
    for (i = 0; i <= k1; i++) {
        // cout<<a[0]<<endl;
        a[0] = a[n - 1];
        n--;
        minheapify(a, 0);
    }

    /*Step 2: Do extract minimum k2 – k1 – 1 times and sum all
   extracted elements. (This step takes O ((K2 – k1) * Log n) time)*/
    for (i = k1 + 1; i < k2; i++) {
        // cout<<a[0]<<endl;
        ans += a[0];
        a[0] = a[n - 1];
        n--;
        minheapify(a, 0);
    }

    cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

static int n = 7;

static void minheapify(int []a, int index)
{

    int small = index;
    int l = 2 * index + 1;
    int r = 2 * index + 2;

    if (l < n && a[l] < a[small])
        small = l;

    if (r < n && a[r] < a[small])
        small = r;

    if (small != index)
    {
        int t = a[small];
        a[small] = a[index];
        a[index] = t;
        minheapify(a, small);
    }
}

// Driver code
public static void main (String[] args)
{
    int i = 0;
    int k1 = 3;
    int k2 = 6;

    int []a = { 20, 8, 22, 4, 12, 10, 14 };

    int ans = 0;

    for (i = (n / 2) - 1; i >= 0; i--)
    {
        minheapify(a, i);
    }

    // decreasing value by 1 because we want
    // min heapifying k times and it starts
    // from 0 so we have to decrease it 1 time
    k1--;
    k2--;

    // Step 1: Do extract minimum k1 times
    // (This step takes O(K1 Log n) time)
    for (i = 0; i <= k1; i++)
    {
        a[0] = a[n - 1];
        n--;
        minheapify(a, 0);
    }

    for (i = k1 + 1; i < k2; i++)
    {
        // cout<<a[0]<<endl;
        ans += a[0];
        a[0] = a[n - 1];
        n--;
        minheapify(a, 0);
    }

    System.out.println(ans);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 implementation of above approach
n = 7

def minheapify(a, index):
    small = index
    l = 2 * index + 1
    r = 2 * index + 2

    if (l < n and a[l] < a[small]):
        small = l

    if (r < n and a[r] < a[small]):
        small = r

    if (small != index):
        (a[small], a[index]) = (a[index], a[small])
        minheapify(a, small)

# Driver Code
i = 0
k1 = 3
k2 = 6

a = [ 20, 8, 22, 4, 12, 10, 14 ]
ans = 0

for i in range((n //2) - 1, -1, -1):
    minheapify(a, i)

# decreasing value by 1 because we want
# min heapifying k times and it starts
# from 0 so we have to decrease it 1 time
k1 -= 1
k2 -= 1

# Step 1: Do extract minimum k1 times
# (This step takes O(K1 Log n) time)
for i in range(0, k1 + 1):
    a[0] = a[n - 1]
    n -= 1
    minheapify(a, 0)

# Step 2: Do extract minimum k2 – k1 – 1 times and
# sum all extracted elements.
# (This step takes O ((K2 – k1) * Log n) time)*/
for i in range(k1 + 1, k2) :
    ans += a[0]
    a[0] = a[n - 1]
    n -= 1
    minheapify(a, 0)

print (ans)

# This code is contributed
# by Atul_kumar_Shrivastava
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

static int n = 7;

static void minheapify(int []a, int index)
{

    int small = index;
    int l = 2 * index + 1;
    int r = 2 * index + 2;

    if (l < n && a[l] < a[small])
        small = l;

    if (r < n && a[r] < a[small])
        small = r;

    if (small != index)
    {
        int t = a[small];
        a[small] = a[index];
        a[index] = t;
        minheapify(a, small);
    }
}

// Driver code
static void Main()
{
    int i = 0;
    int k1 = 3;
    int k2 = 6;

    int []a = { 20, 8, 22, 4, 12, 10, 14 };

    int ans = 0;

    for (i = (n / 2) - 1; i >= 0; i--)
    {
        minheapify(a, i);
    }

    // decreasing value by 1 because we want
    // min heapifying k times and it starts
    // from 0 so we have to decrease it 1 time
    k1--;
    k2--;

    // Step 1: Do extract minimum k1 times
    // (This step takes O(K1 Log n) time)
    for (i = 0; i <= k1; i++)
    {
        // cout<<a[0]<<endl;
        a[0] = a[n - 1];
        n--;
        minheapify(a, 0);
    }

    /*Step 2: Do extract minimum k2 – k1 – 1 times
    and sum all extracted elements. (This step
    takes O ((K2 – k1) * Log n) time)*/
    for (i = k1 + 1; i < k2; i++)
    {
        // cout<<a[0]<<endl;
        ans += a[0];
        a[0] = a[n - 1];
        n--;
        minheapify(a, 0);
    }

    Console.Write(ans);
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

// Javascript implementation of above approach
let n = 7;

function minheapify(a, index)
{
    let small = index;
    let l = 2 * index + 1;
    let r = 2 * index + 2;

    if (l < n && a[l] < a[small])
        small = l;

    if (r < n && a[r] < a[small])
        small = r;

    if (small != index)
    {
        let t = a[small];
        a[small] = a[index];
        a[index] = t;
        minheapify(a, small);
    }
}

// Driver code
let i = 0;
let k1 = 3;
let k2 = 6;

let a = [ 20, 8, 22, 4, 12, 10, 14 ];

let ans = 0;

for(i = parseInt(n / 2, 10) - 1; i >= 0; i--)
{
    minheapify(a, i);
}

// decreasing value by 1 because we want
// min heapifying k times and it starts
// from 0 so we have to decrease it 1 time
k1--;
k2--;

// Step 1: Do extract minimum k1 times
// (This step takes O(K1 Log n) time)
for(i = 0; i <= k1; i++)
{
    a[0] = a[n - 1];
    n--;
    minheapify(a, 0);
}

for(i = k1 + 1; i < k2; i++)
{

    // cout<<a[0]<<endl;
    ans += a[0];
    a[0] = a[n - 1];
    n--;
    minheapify(a, 0);
}

document.write(ans);

// This code is contributed by vaibhavrabadiya117

</script>
```

**输出:**

```
 26
```

该方法的整体时间复杂度为 O(n + k2 Log n)，优于基于排序的方法。
***参考文献**:*[*https://www.geeksforgeeks.org/heap-sort*](https://www.geeksforgeeks.org/heap-sort/)

本文由[**Nishant _ Singh(Pintu)**](https://practice.geeksforgeeks.org/user-profile.php?user=_code)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。