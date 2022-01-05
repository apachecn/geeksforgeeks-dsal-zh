# 一个数组中最小的元素，精确地重复‘k’次。

> 原文:[https://www . geesforgeks . org/最小元素-数组-重复-精确-k 次/](https://www.geeksforgeeks.org/smallest-element-array-repeated-exactly-k-times/)

给定一个大小为 n 的数组，目标是找出最小的重复次数正好为 k 的数，其中 k > 0？
假设数组只有正整数，1 < = arr[i] < 1000，每个 i = 0 到 n -1。
**例:**

```
Input : arr[] = {2 2 1 3 1}
        k = 2
Output: 1
Explanation:
Here in array,
2 is repeated 2 times
1 is repeated 2 times 
3 is repeated 1 time
Hence 2 and 1 both are repeated 'k' times
i.e 2 and min(2, 1) is 1

Input : arr[] = {3 5 3 2}
        k = 1
Output : 2
Explanation:
Both 2 and 5 are repeating 1 time but
min(5, 2) is 2
```

**简单方法**:简单的方法是使用两个嵌套循环。外部循环从最左边的元素开始一个接一个地选取一个元素。内部循环检查其右侧是否存在相同的元素。如果存在，增加计数，并使我们在右边得到的数字为负，以防止它再次计数。

## C++

```
// C++ program to find smallest number
// in array that is repeated exactly
// 'k' times.
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1000;

int findDuplicate(int arr[], int n, int k)
{
    // Since arr[] has numbers in range from
    // 1 to MAX
    int res = MAX + 1;
    for (int i = 0; i < n; i++) {
        if (arr[i] > 0) {

            // set count to 1 as number is present
            // once
            int count = 1;
            for (int j = i + 1; j < n; j++)
                if (arr[i] == arr[j])
                    count += 1;

            // If frequency of number is equal to 'k'
            if (count == k)
                res = min(res, arr[i]);
        }
    }
    return res;
}

// Driver code
int main()
{
    int arr[] = { 2, 2, 1, 3, 1 };
    int k = 2;
    int n = sizeof(arr) / (sizeof(arr[0]));
    cout << findDuplicate(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest number
// in array that is repeated exactly
// 'k' times.
public class GFG {
    static final int MAX = 1000;

    // finds the smallest number in arr[]
    // that is repeated k times
    static int findDuplicate(int arr[], int n, int k)
    {
        // Since arr[] has numbers in range from
        // 1 to MAX
        int res = MAX + 1;
        for (int i = 0; i < n; i++) {
            if (arr[i] > 0) {

                // set count to 1 as number is
                // present once
                int count = 1;
                for (int j = i + 1; j < n; j++)
                    if (arr[i] == arr[j])
                        count += 1;

                // If frequency of number is equal
                // to 'k'
                if (count == k)
                    res = Math.min(res, arr[i]);
            }
        }
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 2, 1, 3, 1 };
        int k = 2;
        int n = arr.length;
        System.out.println(findDuplicate(arr, n, k));
    }
}
// This article is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 program to find smallest
# number in array that is repeated
# exactly 'k' times.
MAX = 1000

def findDuplicate(arr, n, k):

    # Since arr[] has numbers in
    # range from 1 to MAX
    res = MAX + 1

    for i in range(0, n):
        if (arr[i] > 0):

            # set count to 1 as number
            # is present once
            count = 1
            for j in range(i + 1, n):
                if (arr[i] == arr[j]):
                    count += 1

            # If frequency of number is equal to 'k'
            if (count == k):
                res = min(res, arr[i])

    return res

# Driver code
arr = [2, 2, 1, 3, 1]
k = 2
n = len(arr)
print(findDuplicate(arr, n, k))

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to find smallest number
// in array that is repeated exactly
// 'k' times.
using System;

public class GFG {

    static int MAX = 1000;

    // finds the smallest number in arr[]
    // that is repeated k times
    static int findDuplicate(int[] arr,
                              int n, int k)
    {

        // Since arr[] has numbers in range
        // from 1 to MAX
        int res = MAX + 1;

        for (int i = 0; i < n; i++)
        {
            if (arr[i] > 0)
            {

                // set count to 1 as number
                // is present once
                int count = 1;
                for (int j = i + 1; j < n; j++)
                    if (arr[i] == arr[j])
                        count += 1;

                // If frequency of number is
                // equal to 'k'
                if (count == k)
                    res = Math.Min(res, arr[i]);
            }
        }

        return res;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 2, 2, 1, 3, 1 };
        int k = 2;
        int n = arr.Length;

        Console.WriteLine(
                      findDuplicate(arr, n, k));
    }
}

// This article is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find smallest number
// in array that is repeated exactly
// 'k' times.
function findDuplicate($arr, $n, $k)
{
    // Since arr[] has numbers in
    // range from 1 to MAX
    $MAX = 1000;
    $res = $MAX + 1;
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] > 0)
        {

            // set count to 1 as number is
            // present once
            $count = 1;
            for ($j = $i + 1; $j < $n; $j++)
                if ($arr[$i] == $arr[$j])
                    $count += 1;

            // If frequency of number is
            // equal to 'k'
            if ($count == $k)
                $res = min($res, $arr[$i]);
        }
    }
    return $res;
}

// Driver code
$arr = array(2, 2, 1, 3, 1);
$k = 2;
$n = count($arr);
echo findDuplicate($arr, $n, $k);

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>

// Javascript program to find smallest number
// in array that is repeated exactly
// 'k' times

    let MAX = 1000;

    // finds the smallest number in arr[]
    // that is repeated k times
    function findDuplicate(arr, n, k)
    {
        // Computing frequencies of all elements
        let freq = new Array(MAX).fill(0);

        for (let i = 0; i < n; i++) {
            if (arr[i] < 1 && arr[i] > MAX) {
                document.write("Out of range");
                return -1;
            }
            freq[arr[i]] += 1;
        }

        // Finding the smallest element with
        // frequency as k
        for (let i = 0; i < MAX; i++) {

            // If frequency of any of the number
            // is equal to k starting from 0
            // then return the number
            if (freq[i] == k)
                return i;
        }

        return -1;
    }

// driver program

        let arr = [ 2, 2, 1, 3, 1 ];
        let k = 2;
        let n = arr.length;
        document.write(findDuplicate(arr, n, k));

// This code is contributed by code_hunt.
</script>
```

**输出:**

```
1
```

**时间复杂度:** O(n <sup>2</sup> )
**辅助空间:** O(1)
这个解决方案不需要数组元素在有限的范围内。
**更好的解决方案**:对输入数组进行排序，找到出现次数正好为 k 的第一个元素。

## C++

```
// C++ program to find smallest number
// in array that is repeated exactly
// 'k' times.
#include <bits/stdc++.h>
using namespace std;

int findDuplicate(int arr[], int n, int k)
{
    // Sort the array
    sort(arr, arr + n);

    // Find the first element with exactly
    // k occurrences.
    int i = 0;
    while (i < n) {
        int j, count = 1;
        for (j = i + 1; j < n && arr[j] == arr[i]; j++)
            count++;

        if (count == k)
            return arr[i];

        i = j;
    }

    return -1;
}

// Driver code
int main()
{
    int arr[] = { 2, 2, 1, 3, 1 };
    int k = 2;
    int n = sizeof(arr) / (sizeof(arr[0]));
    cout << findDuplicate(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest number
// in array that is repeated exactly
// 'k' times.
import java.util.Arrays;
public class GFG {

    // finds the smallest number in arr[]
    // that is repeated k times
    static int findDuplicate(int arr[], int n, int k)
    {
        // Sort the array
        Arrays.sort(arr);

        // Find the first element with exactly
        // k occurrences.
        int i = 0;
        while (i < n) {
            int j, count = 1;
            for (j = i + 1; j < n && arr[j] == arr[i]; j++)
                count++;

            if (count == k)
                return arr[i];

            i = j;
        }

        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 2, 1, 3, 1 };
        int k = 2;
        int n = arr.length;
        System.out.println(findDuplicate(arr, n, k));
    }
}
// This article is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to find smallest number
# in array that is repeated exactly
# 'k' times.

def findDuplicate(arr, n, k):

    # Sort the array
    arr.sort()

    # Find the first element with exactly
    # k occurrences.
    i = 0
    while (i < n):
        j, count = i + 1, 1
        while (j < n and arr[j] == arr[i]):
            count += 1
            j += 1

        if (count == k):
            return arr[i]

        i = j

    return -1

# Driver code
arr = [ 2, 2, 1, 3, 1 ];
k = 2
n = len(arr)
print findDuplicate(arr, n, k)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find smallest number
// in array that is repeated exactly
// 'k' times.
using System;

public class GFG {

    // finds the smallest number in arr[]
    // that is repeated k times
    static int findDuplicate(int[] arr,
                             int n, int k)
    {

        // Sort the array
        Array.Sort(arr);

        // Find the first element with
        // exactly k occurrences.
        int i = 0;
        while (i < n) {
            int j, count = 1;
            for (j = i + 1; j < n &&
                     arr[j] == arr[i]; j++)
                count++;

            if (count == k)
                return arr[i];

            i = j;
        }

        return -1;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 2, 2, 1, 3, 1 };
        int k = 2;
        int n = arr.Length;

        Console.WriteLine(
               findDuplicate(arr, n, k));
    }
}

// This article is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find smallest number
// in array that is repeated exactly
// 'k' times.

// finds the smallest number in arr[]
// that is repeated k times
function findDuplicate($arr, $n, $k)
{
    // Sort the array
    sort($arr);

    // Find the first element with
    // exactly k occurrences.
    $i = 0;
    while ($i < $n)
    {
        $j; $count = 1;
        for ($j = $i + 1; $j < $n &&
             $arr[$j] == $arr[$i]; $j++)
            $count++;

        if ($count == $k)
            return $arr[$i];

        $i = $j;
    }

    return -1;
}

// Driver code
$arr = array( 2, 2, 1, 3, 1 );
$k = 2;
$n = sizeof($arr);
echo(findDuplicate($arr, $n, $k));

// This code is contributed
// by Code_Mech.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find smallest number
    // in array that is repeated exactly
    // 'k' times.

    // finds the smallest number in arr[]
    // that is repeated k times
    function findDuplicate(arr, n, k)
    {

        // Sort the array
        arr.sort();

        // Find the first element with
        // exactly k occurrences.
        let i = 0;
        while (i < n) {
            let j, count = 1;
            for (j = i + 1; j < n &&
                     arr[j] == arr[i]; j++)
                count++;

            if (count == k)
                return arr[i];

            i = j;
        }

        return -1;
    }

    let arr = [ 2, 2, 1, 3, 1 ];
    let k = 2;
    let n = arr.length;

    document.write(findDuplicate(arr, n, k));

</script>
```

**输出:**

```
1
```

**时间复杂度:** O(n Log n)
**辅助空间:** O(1)
**高效方法**:高效方法基于数组具有小范围(1 到 1000)的数字这一事实。我们通过使用最大大小的频率数组来解决这个问题，并将每个数字的频率存储在该数组中。

## C++

```
// C++ program to find smallest number
// in array that is repeated exactly
// 'k' times.
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1000;

int findDuplicate(int arr[], int n, int k)
{
    // Computing frequencies of all elements
    int freq[MAX];
    memset(freq, 0, sizeof(freq));
    for (int i = 0; i < n; i++) {
        if (arr[i] < 1 && arr[i] > MAX) {
            cout << "Out of range";
            return -1;
        }
        freq[arr[i]] += 1;
    }

    // Finding the smallest element with
    // frequency as k
    for (int i = 0; i < MAX; i++) {

        // If frequency of any of the number
        // is equal to k starting from 0
        // then return the number
        if (freq[i] == k)
            return i;
    }

    return -1;
}

// Driver code
int main()
{
    int arr[] = { 2, 2, 1, 3, 1 };
    int k = 2;
    int n = sizeof(arr) / (sizeof(arr[0]));
    cout << findDuplicate(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest number
// in array that is repeated exactly
// 'k' times.
public class GFG {

    static final int MAX = 1000;

    // finds the smallest number in arr[]
    // that is repeated k times
    static int findDuplicate(int arr[], int n, int k)
    {
        // Computing frequencies of all elements
        int[] freq = new int[MAX];

        for (int i = 0; i < n; i++) {
            if (arr[i] < 1 && arr[i] > MAX) {
                System.out.println("Out of range");
                return -1;
            }
            freq[arr[i]] += 1;
        }

        // Finding the smallest element with
        // frequency as k
        for (int i = 0; i < MAX; i++) {

            // If frequency of any of the number
            // is equal to k starting from 0
            // then return the number
            if (freq[i] == k)
                return i;
        }

        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 2, 1, 3, 1 };
        int k = 2;
        int n = arr.length;
        System.out.println(findDuplicate(arr, n, k));
    }
}
// This article is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to find smallest number
# in array that is repeated exactly
# 'k' times.

MAX = 1000

def findDuplicate(arr, n, k):

    # Computing frequencies of all elements
    freq = [0 for i in range(MAX)]

    for i in range(n):
        if (arr[i] < 1 and arr[i] > MAX):
            print "Out of range"
            return -1
        freq[arr[i]] += 1

    # Finding the smallest element with
    # frequency as k
    for i in range(MAX):

        # If frequency of any of the number
        # is equal to k starting from 0
        # then return the number
        if (freq[i] == k):
            return i

    return -1

# Driver code
arr = [ 2, 2, 1, 3, 1 ]
k = 2
n = len(arr)
print findDuplicate(arr, n, k)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find smallest number
// in array that is repeated exactly
// 'k' times.
using System;

public class GFG {

    static int MAX = 1000;

    // finds the smallest number in arr[]
    // that is repeated k times
    static int findDuplicate(int[] arr,
                            int n, int k)
    {

        // Computing frequencies of all
        // elements
        int[] freq = new int[MAX];

        for (int i = 0; i < n; i++)
        {
            if (arr[i] < 1 && arr[i] > MAX)
            {
                Console.WriteLine("Out of range");
                return -1;
            }

            freq[arr[i]] += 1;
        }

        // Finding the smallest element with
        // frequency as k
        for (int i = 0; i < MAX; i++) {

            // If frequency of any of the
            // number is equal to k starting
            // from 0 then return the number
            if (freq[i] == k)
                return i;
        }

        return -1;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 2, 2, 1, 3, 1 };
        int k = 2;
        int n = arr.Length;

        Console.WriteLine(
               findDuplicate(arr, n, k));
    }
}

// This article is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find smallest number
// in array that is repeated exactly
// 'k' times.

$MAX = 1000;

function findDuplicate($arr, $n, $k)
{
    global $MAX;

    // Computing frequencies of all elements
    $freq=array_fill(0, $MAX, 0);

    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] < 1 && $arr[$i] > $MAX)
        {
            echo "Out of range";
            return -1;
        }
        $freq[$arr[$i]] += 1;
    }

    // Finding the smallest element with
    // frequency as k
    for ($i = 0; $i < $MAX; $i++)
    {

        // If frequency of any of the number
        // is equal to k starting from 0
        // then return the number
        if ($freq[$i] == $k)
            return $i;
    }

    return -1;
}

    // Driver code
    $arr = array( 2, 2, 1, 3, 1 );
    $k = 2;
    $n = count($arr);
    echo findDuplicate($arr, $n, $k);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program to find smallest number
// in array that is repeated exactly
// 'k' times.

var MAX = 1000;

// finds the smallest number in arr
// that is repeated k times
function findDuplicate(arr , n , k)
{
    // Computing frequencies of all elements
    var freq = Array.from({length: MAX}, (_, i) => 0);

    for (var i = 0; i < n; i++) {
        if (arr[i] < 1 && arr[i] > MAX) {
            document.write("Out of range");
            return -1;
        }
        freq[arr[i]] += 1;
    }

    // Finding the smallest element with
    // frequency as k
    for (var i = 0; i < MAX; i++) {

        // If frequency of any of the number
        // is equal to k starting from 0
        // then return the number
        if (freq[i] == k)
            return i;
    }

    return -1;
}

// Driver code
var arr = [ 2, 2, 1, 3, 1 ];
var k = 2;
var n = arr.length;
document.write(findDuplicate(arr, n, k));

// This code is contributed by 29AjayKumar
</script>
```

**输出:**

```
1
```

**时间复杂度:**O(MAX+n)
T3】辅助空间: O(MAX)
**如果范围不受限制，我们能在 O(n)时间内求解吗？**
请看[最小元素精确重复‘k’次(不限于小范围)](https://www.geeksforgeeks.org/smallest-element-repeated-exactly-k-times-not-limited-small-range/)
本文由**阿必吉特·尚赫达尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。