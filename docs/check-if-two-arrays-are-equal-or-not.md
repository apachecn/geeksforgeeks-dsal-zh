# 检查两个数组是否相等

> 原文:[https://www . geesforgeks . org/check-如果两个数组相等或不相等/](https://www.geeksforgeeks.org/check-if-two-arrays-are-equal-or-not/)

给定两个长度相等的给定数组，任务是找出给定数组是否相等。如果两个数组都包含相同的元素集，则称这两个数组相等，但是元素的排列(或排列)可能不同。

**注意:**如果有重复，那么重复元素的计数也必须相同，两个数组才能相等。

**示例:**

```
Input  : arr1[] = {1, 2, 5, 4, 0};
         arr2[] = {2, 4, 5, 0, 1}; 
Output : Yes

Input  : arr1[] = {1, 2, 5, 4, 0, 2, 1};
         arr2[] = {2, 4, 5, 0, 1, 1, 2}; 
Output : Yes

Input : arr1[] = {1, 7, 1};
        arr2[] = {7, 7, 1};
Output : No
```

一个**简单的解决方案**是对两个数组进行排序，然后对元素进行线性比较。

## C++

```
// C++ program to find given two array
// are equal or not
#include <bits/stdc++.h>
using namespace std;

// Returns true if arr1[0..n-1] and arr2[0..m-1]
// contain same elements.
bool areEqual(int arr1[], int arr2[], int n, int m)
{
    // If lengths of array are not equal means
    // array are not equal
    if (n != m)
        return false;

    // Sort both arrays
    sort(arr1, arr1 + n);
    sort(arr2, arr2 + m);

    // Linearly compare elements
    for (int i = 0; i < n; i++)
        if (arr1[i] != arr2[i])
            return false;

    // If all elements were same.
    return true;
}

// Driver Code
int main()
{
    int arr1[] = { 3, 5, 2, 5, 2 };
    int arr2[] = { 2, 3, 5, 5, 2 };
    int n = sizeof(arr1) / sizeof(int);
    int m = sizeof(arr2) / sizeof(int);

    if (areEqual(arr1, arr2, n, m))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find given two array
// are equal or not
import java.io.*;
import java.util.*;

class GFG {
    // Returns true if arr1[0..n-1] and arr2[0..m-1]
    // contain same elements.
    public static boolean areEqual(int arr1[], int arr2[])
    {
        int n = arr1.length;
        int m = arr2.length;

        // If lengths of array are not equal means
        // array are not equal
        if (n != m)
            return false;

        // Sort both arrays
        Arrays.sort(arr1);
        Arrays.sort(arr2);

        // Linearly compare elements
        for (int i = 0; i < n; i++)
            if (arr1[i] != arr2[i])
                return false;

        // If all elements were same.
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr1[] = { 3, 5, 2, 5, 2 };
        int arr2[] = { 2, 3, 5, 5, 2 };

        if (areEqual(arr1, arr2))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python3 program to find given
# two array are equal or not

# Returns true if arr1[0..n-1] and
# arr2[0..m-1] contain same elements.

def areEqual(arr1, arr2, n, m):

    # If lengths of array are not
    # equal means array are not equal
    if (n != m):
        return False

    # Sort both arrays
    arr1.sort()
    arr2.sort()

    # Linearly compare elements
    for i in range(0, n - 1):
        if (arr1[i] != arr2[i]):
            return False

    # If all elements were same.
    return True

# Driver Code
arr1 = [3, 5, 2, 5, 2]
arr2 = [2, 3, 5, 5, 2]
n = len(arr1)
m = len(arr2)

if (areEqual(arr1, arr2, n, m)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Shivi_Aggarwal.
```

## C#

```
// C# program to find given two array
// are equal or not
using System;

class GFG {

    // Returns true if arr1[0..n-1] and
    // arr2[0..m-1] contain same elements.
    public static bool areEqual(int[] arr1, int[] arr2)
    {
        int n = arr1.Length;
        int m = arr2.Length;

        // If lengths of array are not
        // equal means array are not equal
        if (n != m)
            return false;

        // Sort both arrays
        Array.Sort(arr1);
        Array.Sort(arr2);

        // Linearly compare elements
        for (int i = 0; i < n; i++)
            if (arr1[i] != arr2[i])
                return false;

        // If all elements were same.
        return true;
    }

    // Driver code
    public static void Main()
    {
        int[] arr1 = { 3, 5, 2, 5, 2 };
        int[] arr2 = { 2, 3, 5, 5, 2 };

        if (areEqual(arr1, arr2))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find given
// two array are equal or not

// Returns true if arr1[0..n-1]
// and arr2[0..m-1] contain same elements.
function areEqual( $arr1, $arr2, $n, $m)
{
    // If lengths of array
    // are not equal means
    // array are not equal
    if ($n != $m)
        return false;

    // Sort both arrays
    sort($arr1);
    sort($arr2);

    // Linearly compare elements
    for ( $i = 0; $i < $n; $i++)
        if ($arr1[$i] != $arr2[$i])
            return false;

    // If all elements were same.
    return true;
}

// Driver Code
$arr1 = array( 3, 5, 2, 5, 2);
$arr2 = array( 2, 3, 5, 5, 2);
$n = count($arr1);
$m = count($arr2);

if (areEqual($arr1, $arr2, $n, $m))
    echo "Yes";
else
    echo "No";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Returns true if arr1[0..n-1] and arr2[0..m-1]
    // contain same elements.
    function areEqual(arr1, arr2)
    {
        let n = arr1.length;
        let m = arr2.length;

        // If lengths of array are not equal means
        // array are not equal
        if (n != m)
            return false;

        // Sort both arrays
        arr1.sort();
        arr2.sort();

        // Linearly compare elements
        for (let i = 0; i < n; i++)
            if (arr1[i] != arr2[i])
                return false;

        // If all elements were same.
        return true;
    }

// Driver Code
    let arr1 = [ 3, 5, 2, 5, 2 ];
    let arr2 = [ 2, 3, 5, 5, 2 ];

    if (areEqual(arr1, arr2))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by chinmoy1997pal.
</script>
```

**Output**

```
Yes
```

**时间复杂度:**O(n log n)
T3】辅助空间: O(1)

这种方法的有效解决方案是使用散列法。我们将 arr1[]的所有元素及其计数存储在哈希表中。然后我们遍历 arr2[]并检查 arr2[]中每个元素的计数是否与 arr1[]中的计数匹配。

以下是上述想法的实现。我们使用[无序 _ 映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)来存储计数。

## C++

```
// C++ program to find given two array
// are equal or not using hashing technique
#include <bits/stdc++.h>
using namespace std;

// Returns true if arr1[0..n-1] and arr2[0..m-1]
// contain same elements.
bool areEqual(int arr1[], int arr2[], int n, int m)
{
    // If lengths of arrays are not equal
    if (n != m)
        return false;

    // Store arr1[] elements and their counts in
    // hash map
    unordered_map<int, int> mp;
    for (int i = 0; i < n; i++)
        mp[arr1[i]]++;

    // Traverse arr2[] elements and check if all
    // elements of arr2[] are present same number
    // of times or not.
    for (int i = 0; i < n; i++) {
        // If there is an element in arr2[], but
        // not in arr1[]
        if (mp.find(arr2[i]) == mp.end())
            return false;

        // If an element of arr2[] appears more
        // times than it appears in arr1[]
        if (mp[arr2[i]] == 0)
            return false;

        mp[arr2[i]]--;
    }

    return true;
}

// Driver Code
int main()
{
    int arr1[] = { 3, 5, 2, 5, 2 };
    int arr2[] = { 2, 3, 5, 5, 2 };
    int n = sizeof(arr1) / sizeof(int);
    int m = sizeof(arr2) / sizeof(int);

    if (areEqual(arr1, arr2, n, m))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find given two array
// are equal or not using hashing technique
import java.util.*;
import java.io.*;

class GFG {
    // Returns true if arr1[0..n-1] and arr2[0..m-1]
    // contain same elements.
    public static boolean areEqual(int arr1[], int arr2[])
    {
        int n = arr1.length;
        int m = arr2.length;

        // If lengths of arrays are not equal
        if (n != m)
            return false;

        // Store arr1[] elements and their counts in
        // hash map
        Map<Integer, Integer> map
            = new HashMap<Integer, Integer>();
        int count = 0;
        for (int i = 0; i < n; i++) {
            if (map.get(arr1[i]) == null)
                map.put(arr1[i], 1);
            else {
                count = map.get(arr1[i]);
                count++;
                map.put(arr1[i], count);
            }
        }

        // Traverse arr2[] elements and check if all
        // elements of arr2[] are present same number
        // of times or not.
        for (int i = 0; i < n; i++) {
            // If there is an element in arr2[], but
            // not in arr1[]
            if (!map.containsKey(arr2[i]))
                return false;

            // If an element of arr2[] appears more
            // times than it appears in arr1[]
            if (map.get(arr2[i]) == 0)
                return false;

            count = map.get(arr2[i]);
            --count;
            map.put(arr2[i], count);
        }

        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr1[] = { 3, 5, 2, 5, 2 };
        int arr2[] = { 2, 3, 5, 5, 2 };

        if (areEqual(arr1, arr2))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python3 program to find if given
# two arrays are equal or not
# using dictionary
from collections import defaultdict

# Returns true if arr1[0..n-1] and
# arr2[0..m-1] contain same elements.

def areEqual(arr1, arr2, n, m):

    # If lengths of array are not
    # equal means array are not equal
    if (n != m):
        return False

    # Create a defaultdict count to
    # store counts
    count = defaultdict(int)

    # Store the elements of arr1
    # and their counts in the dictionary
    for i in arr1:
        count[i] += 1

    # Traverse through arr2 and compare
    # the elements and its count with
    # the elements of arr1
    for i in arr2:

        # Return false if the element
        # is not in arr2 or if any element
        # appears more no. of times than in arr1
        if (count[i] == 0):
            return False

        # If element is found, decrement
        # its value in the dictionary
        else:
            count[i] -= 1

    # Return true if both arr1 and
    # arr2 are equal
    return True

# Driver Code
arr1 = [3, 5, 2, 5, 2]
arr2 = [2, 3, 5, 5, 2]

n = len(arr1)
m = len(arr2)

if areEqual(arr1, arr2, n, m):
    print("Yes")
else:
    print("No")

# This code is contributed by Karthik_Aravind
```

## C#

```
// C# program to find given two array
// are equal or not using hashing technique
using System;
using System.Collections.Generic;

class GFG {
    // Returns true if arr1[0..n-1] and arr2[0..m-1]
    // contain same elements.
    public static bool areEqual(int[] arr1, int[] arr2)
    {
        int n = arr1.Length;
        int m = arr2.Length;

        // If lengths of arrays are not equal
        if (n != m)
            return false;

        // Store arr1[] elements and their counts in
        // hash map
        Dictionary<int, int> map
            = new Dictionary<int, int>();
        int count = 0;
        for (int i = 0; i < n; i++) {
            if (!map.ContainsKey(arr1[i]))
                map.Add(arr1[i], 1);
            else {
                count = map[arr1[i]];
                count++;
                map.Remove(arr1[i]);
                map.Add(arr1[i], count);
            }
        }

        // Traverse arr2[] elements and check if all
        // elements of arr2[] are present same number
        // of times or not.
        for (int i = 0; i < n; i++) {
            // If there is an element in arr2[], but
            // not in arr1[]
            if (!map.ContainsKey(arr2[i]))
                return false;

            // If an element of arr2[] appears more
            // times than it appears in arr1[]
            if (map[arr2[i]] == 0)
                return false;

            count = map[arr2[i]];
            --count;

            if (!map.ContainsKey(arr2[i]))
                map.Add(arr2[i], count);
        }
        return true;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr1 = { 3, 5, 2, 5, 2 };
        int[] arr2 = { 2, 3, 5, 5, 2 };

        if (areEqual(arr1, arr2))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

//  Javascript program to find given two array
// are equal or not using hashing technique

    // Returns true if arr1[0..n-1] and arr2[0..m-1]
    // contain same elements.
    function areEqual(arr1, arr2)
    {
        let n = arr1.length;
        let m = arr2.length;

        // If lengths of arrays are not equal
        if (n != m)
            return false;

        // Store arr1[] elements and their counts in
        // hash map
        let map
            = new Map();
        let count = 0;
        for (let i = 0; i < n; i++) {
            if (map.get(arr1[i]) == null)
                map.set(arr1[i], 1);
            else {
                count = map.get(arr1[i]);
                count++;
                map.set(arr1[i], count);
            }
        }

        // Traverse arr2[] elements and check if all
        // elements of arr2[] are present same number
        // of times or not.
        for (let i = 0; i < n; i++) {
            // If there is an element in arr2[], but
            // not in arr1[]
            if (!map.has(arr2[i]))
                return false;

            // If an element of arr2[] appears more
            // times than it appears in arr1[]
            if (map.get(arr2[i]) == 0)
                return false;

            count = map.get(arr2[i]);
            --count;
            map.set(arr2[i], count);
        }

        return true;
    }

    // Driver code

    let arr1 = [ 3, 5, 2, 5, 2 ];
    let arr2 = [ 2, 3, 5, 5, 2 ];

        if (areEqual(arr1, arr2))
            document.write("Yes");
        else
            document.write("No");

</script>
```

**Output**

```
Yes
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)

不比较数组的每个元素，不使用无序映射(通过异或)的**替代方案**。只有当每个元素在一个数组中只存在一次时，这种方法才有效。例如:数组 a : { 3，3 }和数组 b : { 5，5 }，xor_of_array_a(比如 b1) = 0，xor_of_array_b = 0(比如 b2)和 b1^b2 = 0，但是数组 a 和数组 b 不相等。

## C++14

```
// C++ program to find given two array
// are equal or not
#include <bits/stdc++.h>
using namespace std;

// Returns true if arr1[0..n-1] and arr2[0..m-1]
// contain same elements.
bool areEqual(int arr1[], int arr2[], int n, int m)
{
    // If lengths of array are not equal means
    // array are not equal
    if (n != m)
        return false;

    // to store xor of both arrays
    int b1 = arr1[0];
    int b2 = arr2[0];

    // find xor of each elements in array
    for (int i = 1; i < n; i++) {
        b1 ^= arr1[i];
    }

    for (int i = 1; i < m; i++) {
        b2 ^= arr2[i];
    }
    int all_xor = b1 ^ b2;

    // if xor is zero means they are equal (5^5=0)
    if (all_xor == 0)
        return true;

    // If all elements were not same, then xor will not be
    // zero
    return false;
}

// Driver Code
int main()
{
    int arr1[] = { 3, 6, 7, 5, 2 };
    int arr2[] = { 2, 3, 5, 6, 7 };
    int n = sizeof(arr1) / sizeof(int);
    int m = sizeof(arr2) / sizeof(int);

    // Function call
    if (areEqual(arr1, arr2, n, m))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find given two array
// are equal or not
import java.io.*;
import java.util.*;

class GFG{

// Returns true if arr1[0..n-1] and arr2[0..m-1]
// contain same elements.
public static boolean areEqual(int arr1[],
                               int arr2[])
{

    // Length of the two array
    int n = arr1.length;
    int m = arr2.length;

    // If lengths of arrays are not equal
    if (n != m)
        return false;

    // To store xor of both arrays
    int b1 = arr1[0];
    int b2 = arr2[0];

    // Find xor of each elements in array
    for(int i = 1; i < n; i++)
    {
        b1 ^= arr1[i];
    }
    for(int i = 1; i < m; i++)
    {
        b2 ^= arr2[i];
    }
    int all_xor = b1 ^ b2;

    // If xor is zero means they are
    // equal (5^5=0)
    if (all_xor == 0)
        return true;

    // If all elements were not same,
    // then xor will not be zero
    return false;
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = { 3, 5, 2, 5, 2 };
    int arr2[] = { 2, 3, 5, 5, 2 };

    // Function call
    if (areEqual(arr1, arr2))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by sayantanbose2001
```

## 蟒蛇 3

```
# Python3 program to find given
# two array are equal or not

# Returns true if arr1[0..n-1] and
# arr2[0..m-1] contain same elements.

def areEqual(arr1, arr2, n, m):

    # If lengths of array are not
    # equal means array are not equal
    if (n != m):
        return False
    b1 = arr1[0]
    b2 = arr2[0]

    # find xor of all elements
    for i in range(1, n - 1):
        b1 ^= arr1[i]

    for i in range(1, m - 1):
        b2 ^= arr2[i]

    all_xor = b1 ^ b2

    # If all elements were same then xor will be zero
    if(all_xor == 0):
        return True

    return False

# Driver Code
arr1 = [3, 5, 2, 5, 2]
arr2 = [2, 3, 5, 5, 2]
n = len(arr1)
m = len(arr2)

# Function call
if (areEqual(arr1, arr2, n, m)):
    print("Yes")
else:
    print("No")
```

## java 描述语言

```
<script>
// Java Script program to find given two array
// are equal or not

// Returns true if arr1[0..n-1] and arr2[0..m-1]
// contain same elements.
function areEqual(arr1,arr2)
{

    // Length of the two array
    let n = arr1.length;
    let m = arr2.length;

    // If lengths of arrays are not equal
    if (n != m)
        return false;

    // To store xor of both arrays
    let b1 = arr1[0];
    let b2 = arr2[0];

    // Find xor of each elements in array
    for(let i = 1; i < n; i++)
    {
        b1 ^= arr1[i];
    }
    for(let i = 1; i < m; i++)
    {
        b2 ^= arr2[i];
    }
    let all_xor = b1 ^ b2;

    // If xor is zero means they are
    // equal (5^5=0)
    if (all_xor == 0)
        return true;

    // If all elements were not same,
    // then xor will not be zero
    return false;
}

// Driver code

    let arr1 = [ 3, 5, 2, 5, 2 ];
    let arr2 = [ 2, 3, 5, 5, 2 ];

    // Function call
    if (areEqual(arr1, arr2))
        document.write("Yes");
    else
        document.write("No");

//contributed by sravan kumar Gottumukkala
</script>
```

**Output**

```
Yes
```

**时间复杂度:** O(n)
**辅助空间:** O(1)

本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。

改进者: **vt_m，Shivi_Aggarwal，imrohan，princiraj1992，karthikaravindt88，**[**anupriyanishad**](https://www.linkedin.com/in/anupriyanishad/)