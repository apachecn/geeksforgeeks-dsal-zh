# 检查给定数组是否可以用偶数和分成对

> 原文:[https://www . geeksforgeeks . org/check-if-a-给定数组可以用偶数和进行成对划分/](https://www.geeksforgeeks.org/check-if-a-given-array-can-be-divided-into-pairs-with-even-sum/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是检查是否有可能将整个数组分成几对，使得每对的**和为**偶数**。如果可能，打印**“是”**。否则，打印**“否”**。**

**示例:**

> **输入:** arr[] = {3，2，1，4，7，5，}
> **输出:**是
> **解释:**
> 给定的数组可以分成几对:{1，3}、{2，4}、{5，7}。
> 
> **输入:** arr[] = {1，2，3，4，5，6}
> **输出:**否
> **解释:**
> 不存在任何可能的对分布，因此每个对的和都是偶数。

**天真方法:**解决这个问题最简单的方法是[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，[找到一个具有相同奇偶性](https://www.geeksforgeeks.org/count-of-all-possible-pairs-of-array-elements-with-same-parity/)的元素，这个元素还没有被拾取，并且标记两个被拾取的元素以避免重复。如果对于任何元素，没有找到合适的元素，打印**“否”**。否则，如果整个阵列可以分割成所需的对，则打印**“是”**。

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)

**高效方法:**其思想是观察这样一个事实，即如果给定数组中出现的偶数和奇数的计数都是偶数，那么只有这样，给定数组才能被奇数和偶数分成具有偶数和的对。按照以下步骤解决问题:

1.  找到给定数组中奇数和偶数元素的总数[，并将其存储在两个变量中，分别为**计数偶数**和**计数奇数**。](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)
2.  [检查**计数偶数**和**计数奇数**是否为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。如果发现是真的，打印**“是”**。
3.  否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if we can split
// array into pairs of even sum or not
bool canPairs(int arr[], int n)
{
    // If the length is odd then it
    // is not possible to make pairs
    if (n % 2 == 1)
        return false;

    // Initialize count of odd & even
    int odd_count = 0, even_count = 0;

    // Iterate through the array
    for (int i = 0; i < n; i++)
    {
        // Count even element
        if (arr[i] % 2 == 0)
            even_count++;
        else
            odd_count++;
    }

    // If count of even elements
    // and odd elements are even
    if (even_count % 2 == 0 && odd_count % 2 == 0)
    {
        return true;
    }

    return false;
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 1, 4, 7, 5 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    if (canPairs(arr, N)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to check if we can split
    // array into pairs of even sum or not
    static boolean canPairs(int[] arr, int n)
    {
        // If the length is odd then it
        // is not possible to make pairs
        if (n % 2 == 1)
            return false;

        // Initialize count of odd & even
        int odd_count = 0, even_count = 0;

        // Iterate through the array
        for (int i = 0; i < n; i++)
        {
            // Count even element
            if (arr[i] % 2 == 0)
                even_count++;
            else
                odd_count++;
        }

        // If count of even elements
        // and odd elements are even
        if (even_count % 2 == 0 && odd_count % 2 == 0)
        {
            return true;
        }
        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 3, 2, 1, 4, 7, 5 };
        int N = arr.length;

        // Function call
        if (canPairs(arr, N))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if we can split
# array into pairs of even sum or not

def canPairs(arr, n):

    # If the length is odd then it
    # is not possible to make pairs
    if (n % 2 == 1):
        return False

    # Initialize count of odd & even
    odd_count = 0
    even_count = 0

    # Iterate through the array
    for i in range(0, n):

        # Count even element
        if (arr[i] % 2 == 0):
            even_count = even_count + 1
        else:
            odd_count = odd_count + 1

    # If count of even elements
    # and odd elements are even
    if ((even_count % 2 == 0) and
            (odd_count % 2 == 0)):
        return True

    return False

# Driver Code
if __name__ == '__main__':

    arr = [3, 2, 1, 4, 7, 5]
    N = len(arr)

    # Function call
    if (canPairs(arr, N)):
        print("Yes")
    else:
        print("No")

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to check if we can split
    // array into pairs of even sum or not
    static bool canPairs(int[] arr, int n)
    {

        // If the length is odd then it
        // is not possible to make pairs
        if (n % 2 == 1)
            return false;

        // Initialize count of odd & even
        int odd_count = 0, even_count = 0;

        // Iterate through the array
        for (int i = 0; i < n; i++)
        {
            // Count even element
            if (arr[i] % 2 == 0)
                even_count++;
            else
                odd_count++;
        }

        // If count of even elements
        // and odd elements are even
        if (even_count % 2 == 0 && odd_count % 2 == 0)
        {
            return true;
        }
        return false;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 3, 2, 1, 4, 7, 5 };
        int N = arr.Length;

        // Function call
        if (canPairs(arr, N))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if we can split
// array into pairs of even sum or not
function canPairs(arr, n)
{

    // If the length is odd then it
    // is not possible to make pairs
    if (n % 2 == 1)
        return false;

    // Initialize count of odd & even
    let odd_count = 0, even_count = 0;

    // Iterate through the array
    for(let i = 0; i < n; i++)
    {

        // Count even element
        if (arr[i] % 2 == 0)
            even_count++;
        else
            odd_count++;
    }

    // If count of even elements
    // and odd elements are even
    if (even_count % 2 == 0 &&
         odd_count % 2 == 0)
    {
        return true;
    }
    return false;
}

// Driver Code
let arr = [ 3, 2, 1, 4, 7, 5 ];
let N = arr.length;

// Function call
if (canPairs(arr, N))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by target_2  

</script>
```

**Output**

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)