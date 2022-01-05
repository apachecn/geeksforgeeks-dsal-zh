# 缩小数组，使每个元素最多出现 2 次

> 原文:[https://www . geesforgeks . org/reduce-the-array-so-每个元素最多出现 2 次/](https://www.geeksforgeeks.org/reduce-the-array-such-that-each-element-appears-at-most-2-times/)

给定一个大小为 **N** 的排序数组 **arr** ，任务是缩小数组，使每个元素最多出现两次。

**示例:**

> **输入:** arr[] = {1，2，2，2，3}
> **输出:** {1，2，2，3}
> **解释:**
> 去掉 2 一次，因为它出现 2 次以上。
> 
> **输入:** arr[] = {3，3，3}
> **输出:** {3，3}
> **解释:**
> 去掉 3 一次，因为它出现 2 次以上。

**进场:**这个可以借助[双指针算法](https://www.geeksforgeeks.org/two-pointers-technique/)解决。

1.  从左边开始移动数组，并保留两个指针。
2.  一个指针**(假设我)**用于迭代数组。
3.  第二个指针**(比如 st)** 向前移动，寻找下一个独特的元素。I 中的元素出现了两次以上。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to reduce the array
// such that each element appears
// at most 2 times

#include <bits/stdc++.h>
using namespace std;

// Function to remove duplicates
void removeDuplicates(int arr[], int n)
{
    // Initialise 2nd pointer
    int st = 0;

    // Iterate over the array
    for (int i = 0; i < n; i++) {

        if (i < n - 2
            && arr[i] == arr[i + 1]
            && arr[i] == arr[i + 2])
            continue;

        // Updating the 2nd pointer
        else {
            arr[st] = arr[i];
            st++;
        }
    }

    cout << "{";
    for (int i = 0; i < st; i++) {
        cout << arr[i];

        if (i != st - 1)
            cout << ", ";
    }
    cout << "}";
}

// Driver code
int main()
{
    int arr[]
        = { 1, 1, 1, 2,
            2, 2, 3, 3,
            3, 3, 3, 3,
            4, 5 };

    int n = sizeof(arr)
            / sizeof(arr[0]);

    // Function call
    removeDuplicates(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reduce the array
// such that each element appears
// at most 2 times
class GFG
{

// Function to remove duplicates
static void removeDuplicates(int arr[], int n)
{
    // Initialise 2nd pointer
    int st = 0;

    // Iterate over the array
    for (int i = 0; i < n; i++) {

        if (i < n - 2
            && arr[i] == arr[i + 1]
            && arr[i] == arr[i + 2])
            continue;

        // Updating the 2nd pointer
        else {
            arr[st] = arr[i];
            st++;
        }
    }

    System.out.print("{");
    for (int i = 0; i < st; i++) {
        System.out.print(arr[i]);

        if (i != st - 1)
            System.out.print(", ");
    }
    System.out.print("}");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 1, 2,
                  2, 2, 3, 3,
                  3, 3, 3, 3,
                  4, 5 };

    int n = arr.length;

    // Function call
    removeDuplicates(arr, n);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to reduce the array
# such that each element appears
# at most 2 times

# Function to remove duplicates
def removeDuplicates(arr, n) :

    # Initialise 2nd pointer
    st = 0;

    # Iterate over the array
    for i in range(n) :

        if (i < n - 2 and arr[i] == arr[i + 1]
            and arr[i] == arr[i + 2]) :
            continue;

        # Updating the 2nd pointer
        else :
            arr[st] = arr[i];
            st += 1;

    print("{",end="")
    for i in range(st) :
        print(arr[i],end="");

        if (i != st - 1) :
            print(", ",end="");

    print("}",end="");

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 1, 1, 2,
            2, 2, 3, 3,
            3, 3, 3, 3,
            4, 5 ];

    n = len(arr);

    # Function call
    removeDuplicates(arr, n);

# This code is contributed by Yash_R
```

## C#

```
// C# program to reduce the array
// such that each element appears
// at most 2 times
using System;

class GFG
{

// Function to remove duplicates
static void removeDuplicates(int []arr, int n)
{
    // Initialise 2nd pointer
    int st = 0;

    // Iterate over the array
    for (int i = 0; i < n; i++) {

        if (i < n - 2
            && arr[i] == arr[i + 1]
            && arr[i] == arr[i + 2])
            continue;

        // Updating the 2nd pointer
        else {
            arr[st] = arr[i];
            st++;
        }
    }

    Console.Write("{");
    for (int i = 0; i < st; i++) {
        Console.Write(arr[i]);

        if (i != st - 1)
            Console.Write(", ");
    }
    Console.Write("}");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 1, 1, 2,
                  2, 2, 3, 3,
                  3, 3, 3, 3,
                  4, 5 };

    int n = arr.Length;

    // Function call
    removeDuplicates(arr, n);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// Java program to reduce the array
// such that each element appears
// at most 2 times

// Function to remove duplicates
function removeDuplicates(arr,n)
{
    // Initialise 2nd pointer
    let st = 0;

    // Iterate over the array
    for (let i = 0; i < n; i++) {

        if (i < n - 2
            && arr[i] == arr[i + 1]
            && arr[i] == arr[i + 2])
            continue;

        // Updating the 2nd pointer
        else {
            arr[st] = arr[i];
            st++;
        }
    }

    document.write("{");
    for (let i = 0; i < st; i++) {
        document.write(arr[i]);

        if (i != st - 1)
            document.write(", ");
    }
    document.write("}");
}

// Driver code
let arr = [ 1, 1, 1, 2,
            2, 2, 3, 3,
            3, 3, 3, 3,
            4, 5 ];

let n = arr.length;

// Function call
removeDuplicates(arr, n);

// This code is contributed by sravan kumar
</script>
```

**Output**

```
{1, 1, 2, 2, 3, 3, 4, 5}
```

***时间复杂度:** O(N)*
***空间复杂度:** O(1)*

**另一种方法:使用 Counter()功能**

*   使用计数器函数计算所有元素的频率。
*   拿一张空单子。
*   遍历数组。
*   如果任何元素的频率大于或等于 2，将其频率设为 1 并将其附加到列表中。
*   如果任何元素的频率等于 1，则取其频率 0 并将其附加到列表中。
*   打印列表。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 program to reduce the array
# such that each element appears
# at most 2 times
from collections import Counter

# Function to remove duplicates
def removeDuplicates(arr, n):
    freq = Counter(arr)

    # Taking empty list
    l = []
    for i in range(n):

        if(freq[arr[i]] >= 2):

            # Making frequency to 1
            freq[arr[i]] = 1
            l.append(arr[i])

        elif(freq[arr[i]] == 1):

            # Making frequency to 0
            # and appending to list
            l.append(arr[i])
            freq[arr[i]] = 0

    # Printing the list
    for i in l:
        print(i, end=" ")

# Driver code
if __name__ == "__main__":

    arr = [1, 1, 1, 2,
           2, 2, 3, 3,
           3, 3, 3, 3,
           4, 5]

    n = len(arr)

    # Function call
    removeDuplicates(arr, n)

# This code is contributed by vikkycirus
```

**Output**

```
1 1 2 2 3 3 4 5 
```

**时间复杂度:** O(N)

**空间复杂度:** O(N)