# 在只读数组中找到多个重复元素中的任意一个

> 原文:[https://www . geesforgeks . org/find-one-multi-repeating-elements-read-array/](https://www.geeksforgeeks.org/find-one-multiple-repeating-elements-read-array/)

给定一个大小为(n+1)的**只读**数组，在数组中找到多个重复元素之一，其中数组只包含 1 到 n 之间的整数。
只读数组意味着数组的内容不能被修改。
**示例:**

```
Input : n = 5
        arr[] = {1, 1, 2, 3, 5, 4}
Output : One of the numbers repeated in the array is: 1

Input : n = 10
        arr[] = {10, 1, 2, 3, 5, 4, 9, 8, 5, 6, 4}
Output : One of the numbers repeated in the array is: 4 OR 5
```

因为数组的大小是 n+1，元素的范围是 1 到 n，所以可以确定至少有一个重复的元素。
一个**简单的解决方案**是创建一个计数数组并存储所有元素的计数。一旦遇到计数大于 1 的元素，我们就返回它。此解决方案在 O(n)个时间内有效，并且需要 O(n)个额外空间。
一种**空间优化解决方案**是将给定的范围(从 1 到 n)分成大小等于 sqrt(n)的块。我们为每个块维护属于每个块的元素的计数。现在，由于数组的大小是(n+1)，而块的大小是 sqrt(n)，那么将有一个这样的块，其大小将大于 sqrt(n)。对于计数大于 sqrt(n)的块，我们可以对该块的元素使用哈希来查找哪个元素出现了多次。
**说明** :
上述方法之所以有效，有以下两个原因:

1.  由于一个额外的元素，总会有一个块的计数大于 sqrt(n)。即使添加了一个额外的元素，它也只会占据其中一个块中的一个位置，从而使该块被选中。
2.  选定的块肯定有重复元素。考虑选择了第 i <sup>个</sup>块。块的大小大于 sqrt(n)(因此，它被选中)此块中的最大不同元素= sqrt(n)。因此，只有在范围(i*sqrt(n)，(i+1)*sqrt(n) ]中有重复元素时，大小才能大于 sqrt(n)。

**注意:**最后形成的块的范围可能等于也可能不等于 sqrt(n)。因此，检查此块是否有重复元素将不同于其他块。然而，从实现的角度来看，这个困难可以通过用最后一个块初始化选定的块来克服。这是安全的，因为至少要选择一个块。
**下面是解决这个问题的分步算法** :

1.  将数组分成大小为 sqrt(n)的块。
2.  创建一个计数数组，存储每个块的元素计数。
3.  拾取计数大于 sqrt(n)的块，将最后一个块
    设置为默认值。
4.  对于属于所选块的元素，使用[散列](https://www.geeksforgeeks.org/hashing-set-1-introduction/)的方法(在下一步中解释)找到该块中的重复元素。
5.  我们可以创建一个键值对的散列数组，其中 key 是块中的元素，value 是给定键出现的次数。这可以在 C++ STL 中使用[无序 _ 映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)轻松实现。

以下是上述思路的实现:

## C++

```
// C++ program to find one of the repeating
// elements in a read only array
#include <bits/stdc++.h>
using namespace std;

// Function to find one of the repeating
// elements
int findRepeatingNumber(const int arr[], int n)
{
    // Size of blocks except the
    // last block is sq
    int sq = sqrt(n);

    // Number of blocks to incorporate 1 to
    // n values blocks are numbered from 0
    // to range-1 (both included)
    int range = (n / sq) + 1;

    // Count array maintains the count for
    // all blocks
    int count[range] = {0};

    // Traversing the read only array and
    // updating count
    for (int i = 0; i <= n; i++)
    {
        // arr[i] belongs to block number
        // (arr[i]-1)/sq i is considered
        // to start from 0
        count[(arr[i] - 1) / sq]++;
    }

    // The selected_block is set to last
    // block by default. Rest of the blocks
    // are checked
    int selected_block = range - 1;
    for (int i = 0; i < range - 1; i++)
    {
        if (count[i] > sq)
        {
            selected_block = i;
            break;
        }
    }

    // after finding block with size > sq
    // method of hashing is used to find
    // the element repeating in this block
    unordered_map<int, int> m;
    for (int i = 0; i <= n; i++)
    {
        // checks if the element belongs to the
        // selected_block
        if ( ((selected_block * sq) < arr[i]) &&
                (arr[i] <= ((selected_block + 1) * sq)))
        {
            m[arr[i]]++;

            // repeating element found
            if (m[arr[i]] > 1)
                return arr[i];
        }
    }

    // return -1 if no repeating element exists
    return -1;
}

// Driver Program
int main()
{
    // read only array, not to be modified
    const int arr[] = { 1, 1, 2, 3, 5, 4 };

    // array of size 6(n + 1) having
    // elements between 1 and 5
    int n = 5;

    cout << "One of the numbers repeated in"
         " the array is: "
         << findRepeatingNumber(arr, n) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find one of the repeating
// elements in a read only array
import java.io.*;
import java.util.*;

class GFG
{

    // Function to find one of the repeating
    // elements
    static int findRepeatingNumber(int[] arr, int n)
    {
        // Size of blocks except the
        // last block is sq
        int sq = (int) Math.sqrt(n);

        // Number of blocks to incorporate 1 to
        // n values blocks are numbered from 0
        // to range-1 (both included)
        int range = (n / sq) + 1;

        // Count array maintains the count for
        // all blocks
        int[] count = new int[range];

        // Traversing the read only array and
        // updating count
        for (int i = 0; i <= n; i++)
        {
            // arr[i] belongs to block number
            // (arr[i]-1)/sq i is considered
            // to start from 0
            count[(arr[i] - 1) / sq]++;
        }

        // The selected_block is set to last
        // block by default. Rest of the blocks
        // are checked
        int selected_block = range - 1;
        for (int i = 0; i < range - 1; i++)
        {
            if (count[i] > sq)
            {
                selected_block = i;
                break;
            }
        }

        // after finding block with size > sq
        // method of hashing is used to find
        // the element repeating in this block
        HashMap<Integer, Integer> m = new HashMap<>();
        for (int i = 0; i <= n; i++)
        {
            // checks if the element belongs to the
            // selected_block
            if ( ((selected_block * sq) < arr[i]) &&
                    (arr[i] <= ((selected_block + 1) * sq)))
            {
                m.put(arr[i], 1);

                // repeating element found
                if (m.get(arr[i]) == 1)
                    return arr[i];
            }
        }

        // return -1 if no repeating element exists
        return -1;
}

// Driver code
public static void main(String args[])
{
    // read only array, not to be modified
    int[] arr = { 1, 1, 2, 3, 5, 4 };

    // array of size 6(n + 1) having
    // elements between 1 and 5
    int n = 5;

    System.out.println("One of the numbers repeated in the array is: " +
                                    findRepeatingNumber(arr, n));
}
}

// This code is contributed by rachana soma
```

## 蟒蛇 3

```
# Python 3program to find one of the repeating
# elements in a read only array
from math import sqrt

# Function to find one of the repeating
# elements
def findRepeatingNumber(arr, n):

    # Size of blocks except the
    # last block is sq
    sq = sqrt(n)

    # Number of blocks to incorporate 1 to
    # n values blocks are numbered from 0
    # to range-1 (both included)
    range__= int((n / sq) + 1)

    # Count array maintains the count for
    # all blocks
    count = [0 for i in range(range__)]

    # Traversing the read only array and
    # updating count
    for i in range(0, n + 1, 1):

        # arr[i] belongs to block number
        # (arr[i]-1)/sq i is considered
        # to start from 0
        count[int((arr[i] - 1) / sq)] += 1

    # The selected_block is set to last
    # block by default. Rest of the blocks
    # are checked
    selected_block = range__ - 1
    for i in range(0, range__ - 1, 1):
        if (count[i] > sq):
            selected_block = i
            break

    # after finding block with size > sq
    # method of hashing is used to find
    # the element repeating in this block
    m = {i:0 for i in range(n)}
    for i in range(0, n + 1, 1):

        # checks if the element belongs
        # to the selected_block
        if (((selected_block * sq) < arr[i]) and
             (arr[i] <= ((selected_block + 1) * sq))):
            m[arr[i]] += 1

            # repeating element found
            if (m[arr[i]] > 1):
                return arr[i]

    # return -1 if no repeating element exists
    return -1

# Driver Code
if __name__ == '__main__':

    # read only array, not to be modified
    arr = [1, 1, 2, 3, 5, 4]

    # array of size 6(n + 1) having
    # elements between 1 and 5
    n = 5

    print("One of the numbers repeated in the array is:",
                             findRepeatingNumber(arr, n))

# This code is contributed by
# Sahil_shelangia
```

## C#

```
// C# program to find one of the repeating
// elements in a read only array
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find one of the repeating
    // elements
    static int findRepeatingNumber(int[] arr, int n)
    {
        // Size of blocks except the
        // last block is sq
        int sq = (int) Math.Sqrt(n);

        // Number of blocks to incorporate 1 to
        // n values blocks are numbered from 0
        // to range-1 (both included)
        int range = (n / sq) + 1;

        // Count array maintains the count for
        // all blocks
        int[] count = new int[range];

        // Traversing the read only array and
        // updating count
        for (int i = 0; i <= n; i++)
        {
            // arr[i] belongs to block number
            // (arr[i]-1)/sq i is considered
            // to start from 0
            count[(arr[i] - 1) / sq]++;
        }

        // The selected_block is set to last
        // block by default. Rest of the blocks
        // are checked
        int selected_block = range - 1;
        for (int i = 0; i < range - 1; i++)
        {
            if (count[i] > sq)
            {
                selected_block = i;
                break;
            }
        }

        // after finding block with size > sq
        // method of hashing is used to find
        // the element repeating in this block
        Dictionary<int,int> m = new Dictionary<int,int>();
        for (int i = 0; i <= n; i++)
        {
            // checks if the element belongs to the
            // selected_block
            if ( ((selected_block * sq) < arr[i]) &&
                    (arr[i] <= ((selected_block + 1) * sq)))
            {
                m.Add(arr[i], 1);

                // repeating element found
                if (m[arr[i]] == 1)
                    return arr[i];
            }
        }

        // return -1 if no repeating element exists
        return -1;
    }

// Driver code
public static void Main(String []args)
{
    // read only array, not to be modified
    int[] arr = { 1, 1, 2, 3, 5, 4 };

    // array of size 6(n + 1) having
    // elements between 1 and 5
    int n = 5;

    Console.WriteLine("One of the numbers repeated in the array is: " +
                                    findRepeatingNumber(arr, n));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find one of the repeating
// elements in a read only array

// Function to find one of the repeating
// elements
function findRepeatingNumber(arr, n) {
    // Size of blocks except the
    // last block is sq
    let sq = Math.sqrt(n);

    // Number of blocks to incorporate 1 to
    // n values blocks are numbered from 0
    // to range-1 (both included)
    let range = Math.floor(n / sq) + 1;

    // Count array maintains the count for
    // all blocks
    let count = new Array(range).fill(0);

    // Traversing the read only array and
    // updating count
    for (let i = 0; i <= n; i++) {
        // arr[i] belongs to block number
        // (arr[i]-1)/sq i is considered
        // to start from 0
        count[Math.floor((arr[i] - 1) / sq)]++;
    }

    // The selected_block is set to last
    // block by default. Rest of the blocks
    // are checked
    let selected_block = range - 1;
    for (let i = 0; i < range - 1; i++) {
        if (count[i] > sq) {
            selected_block = i;
            break;
        }
    }

    // after finding block with size > sq
    // method of hashing is used to find
    // the element repeating in this block
    let m = new Map();
    for (let i = 0; i <= n; i++) {
        // checks if the element belongs to the
        // selected_block
        if (((selected_block * sq) < arr[i]) &&
            (arr[i] <= ((selected_block + 1) * sq))) {
            m[arr[i]]++;

            if (m.has(arr[i])) {
                m.set(arr[i], m.get(arr[i]) + 1)
            } else {
                m.set(arr[i], 1)
            }

            // repeating element found
            if (m.get(arr[i]) > 1)
                return arr[i];
        }
    }

    // return -1 if no repeating element exists
    return -1;
}

// Driver Program

// read only array, not to be modified
const arr = [1, 1, 2, 3, 5, 4];

// array of size 6(n + 1) having
// elements between 1 and 5
let n = 5;

document.write("One of the numbers repeated in"
    + " the array is: "
    + findRepeatingNumber(arr, n) + "<br>");

</script>
```

**输出:**

```
One of the numbers repeated in the array is: 1
```

**时间复杂度** : O(N)
**辅助空间** : sqrt(N)
本文由**安雅金达尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。