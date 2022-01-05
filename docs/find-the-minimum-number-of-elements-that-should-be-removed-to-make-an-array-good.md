# 找出应该移除的元素的最小数量，使数组良好

> 原文:[https://www . geeksforgeeks . org/find-要使数组良好，需要移除的元素数量最少/](https://www.geeksforgeeks.org/find-the-minimum-number-of-elements-that-should-be-removed-to-make-an-array-good/)

给定一个大小为 **N** 的数组和一个整数 **K** 。数组仅由数字{0，1，2，3，…k-1}组成。任务是通过移除一些元素来使数组良好。如果 x 可以被 k 整除，并且可以将给定的数组拆分成 x/k 个子序列，并且每个子序列的形式为{0，1，2，3，…k-1}，则长度为 x 的数组称为好数组。
**注:**空阵也是好阵
**例:**

> **输入:** a[] = {0，1，2，3，4，0，1，0，1，2，3，4}，K = 5
> **输出:** 2
> 第一序列由第一、第二、第三、第四
> 和第五元素组成，第二序列由第八、第九、第十、第十一
> 和第十二元素组成。所以，去掉最后第五个和第六个元素。
> **输入:** a[] = {0，2，1，3}，k = 4
> **输出:** 4
> 移除所有元素。人们无法生成
> {0，1，2，3}形式的子序列

**进场:**

*   设 cnt <sub>0</sub> 为【0】的子序列数，cnt <sub>1</sub> 为子序列数【0，1】，cnt <sub>2</sub> —子序列数【0，1，2】等等，cnt <sub>k-1</sub> 为完成的子序列数【0，1，2，3，…k-1】。
*   从左到右依次遍历 arr 的所有元素。如果阵列中的当前元素为零，则将 cnt <sub>0</sub> 的计数增加 1。
*   如果数组中的当前元素不为零，则检查它在序列计数中的前一个元素是否大于零。
*   如果序列中的前一个元素大于零，则将前一个元素的计数减 1，将当前元素的计数增 1。

下面是上述方法的实现:

## C++

```
// C++ program to remove minimum elements to
// make the given array good
#include <bits/stdc++.h>
using namespace std;

// Function to remove minimum elements to
// make the given array good
int MinRemove(int a[], int n, int k)
{
    // To store count of each subsequence
    vector<int> cnt(k, 0);

    for (int i = 0; i < n; i++) {
        // Increase the count of subsequence [0]
        if (a[i] == 0)
            cnt[0]++;

        // If Previous element subsequence count
        // is greater than zero then increment
        // subsequence count of current element
        // and decrement subsequence count of
        // the previous element.
        else if (cnt[a[i] - 1] > 0) {
            cnt[a[i] - 1]--;
            cnt[a[i]]++;
        }
    }

    // Return the required answer
    return n - (k * cnt[k - 1]);
}

// Driver code
int main()
{

    int a[] = { 0, 1, 2, 3, 4, 0,
                1, 0, 1, 2, 3, 4 },
        k = 5;

    int n = sizeof(a) / sizeof(a[0]);

    // Function call
    cout << MinRemove(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove minimum elements to
// make the given array good
import java.util.Collections;
import java.util.Vector;

class GFG
{
    // Function to remove minimum elements to
    // make the given array good
    static int MinRemove(int[] a, int n, int k)
    {
        // To store count of each subsequence
        int []cnt = new int[n];
        for (int i = 0; i < n; i++)
        {
            // Increase the count of subsequence [0]
            if (a[i] == 0)
                cnt[0]++;

            // If Previous element subsequence count
            // is greater than zero then increment
            // subsequence count of current element
            // and decrement subsequence count of
            // the previous element.
            else if (cnt[a[i] - 1] > 0)
            {
                cnt[a[i] - 1]--;
                cnt[a[i]]++;
            }
        }

        // Return the required answer
        return n - (k * cnt[k - 1]);
    }

    // Driver code
    public static void main(String[] args)
    {

        int a[] = { 0, 1, 2, 3, 4, 0,
                    1, 0, 1, 2, 3, 4 };
        int k = 5;

        int n = a.length;

        // Function call
        System.out.println(MinRemove(a, n, k));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to remove minimum elements to
# make the given array good

# Function to remove minimum elements to
# make the given array good
def MinRemove(a, n, k) :

    # To store count of each subsequence
    cnt = [0] * k

    for i in range(n) :
        # Increase the count of subsequence [0]
        if (a[i] == 0) :
            cnt[0] += 1;

        # If Previous element subsequence count
        # is greater than zero then increment
        # subsequence count of current element
        # and decrement subsequence count of
        # the previous element.
        elif (cnt[a[i] - 1] > 0) :
            cnt[a[i] - 1] -= 1;
            cnt[a[i]] += 1;

    # Return the required answer
    return n - (k * cnt[k - 1]);

# Driver code
if __name__ == "__main__" :

    a = [ 0, 1, 2, 3, 4, 0,
                1, 0, 1, 2, 3, 4 ]
    k = 5;

    n = len(a);

    # Function call
    print(MinRemove(a, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to remove minimum elements to
// make the given array good
using System;

class GFG
{
    // Function to remove minimum elements to
    // make the given array good
    static int MinRemove(int[] a, int n, int k)
    {
        // To store count of each subsequence
        int []cnt = new int[n];
        for (int i = 0; i < n; i++)
        {
            // Increase the count of subsequence [0]
            if (a[i] == 0)
                cnt[0]++;

            // If Previous element subsequence count
            // is greater than zero then increment
            // subsequence count of current element
            // and decrement subsequence count of
            // the previous element.
            else if (cnt[a[i] - 1] > 0)
            {
                cnt[a[i] - 1]--;
                cnt[a[i]]++;
            }
        }

        // Return the required answer
        return n - (k * cnt[k - 1]);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []a = { 0, 1, 2, 3, 4, 0,
                    1, 0, 1, 2, 3, 4 };
        int k = 5;
        int n = a.Length;

        // Function call
        Console.WriteLine(MinRemove(a, n, k));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to remove minimum elements to
// make the given array good

// Function to remove minimum elements to
// make the given array good
function MinRemove(a, n, k)
{
    // To store count of each subsequence
    let cnt = new Array(k).fill(0);

    for (let i = 0; i < n; i++) {
        // Increase the count of subsequence [0]
        if (a[i] == 0)
            cnt[0]++;

        // If Previous element subsequence count
        // is greater than zero then increment
        // subsequence count of current element
        // and decrement subsequence count of
        // the previous element.
        else if (cnt[a[i] - 1] > 0) {
            cnt[a[i] - 1]--;
            cnt[a[i]]++;
        }
    }

    // Return the required answer
    return n - (k * cnt[k - 1]);
}

// Driver code

    let a = [ 0, 1, 2, 3, 4, 0,
                1, 0, 1, 2, 3, 4 ],
        k = 5;

    let n = a.length;

    // Function call
    document.write(MinRemove(a, n, k));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)