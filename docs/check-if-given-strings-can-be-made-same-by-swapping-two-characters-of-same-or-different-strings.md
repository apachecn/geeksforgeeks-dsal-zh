# 检查给定字符串是否可以通过交换相同或不同字符串的两个字符而变得相同

> 原文:[https://www . geesforgeks . org/check-if-给定字符串-可以通过交换相同或不同字符串的两个字符来制作相同的字符串/](https://www.geeksforgeeks.org/check-if-given-strings-can-be-made-same-by-swapping-two-characters-of-same-or-different-strings/)

给定大小为 **N** 的等长字符串**arr[]**的[数组，任务是通过重复交换给定数组中相同或不同字符串的任意一对字符来检查是否所有字符串都可以相等。如果发现为真，则打印**“是”**。否则，打印**“否”**。](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/)

**示例:**

> **输入:**arr[]= {“acbdd”、“abcee”}
> **输出:** YES
> **解释:**
> 交换 arr[0][1]和 arr[0][2]将 arr[]修改为{“abcdd”、“abcee”}
> 交换 arr[0][3]和 arr[1][4]将 arr[]修改为{“abced”、“abced”}
> 因此，需要的输出为**“YES”**
> 
> **输入**:arr[]= {“abb”、“acc”、“abc”}
> **输出:**是
> **解释:**
> 用 arr[1][1]交换 arr[0][2]将 arr[]修改为{“ABC”、“ABC”、“ABC”}。
> 因此，需要的输出是**“是”**。

**方法:**思路是[统计所有字符串](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)中每个不同字符的频率，检查每个不同字符的频率是否可以被 **N** 整除。如果发现为真，则打印**“是”**。否则，打印**“否”**。按照以下步骤解决问题:

*   初始化一个数组，比如 **cntFreq[]** ，来存储所有字符串中每个不同字符的频率。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于遇到的每个字符串，计算字符串中每个不同字符的频率。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **cntFreq[]** 。对于每个 **i <sup>第</sup>** 个字符，检查**cntFreq【I】**是否可被 **N** 整除。如果发现是假的，则打印**“否”**。
*   否则，打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if all strings can be
// made equal by swapping any pair of
// characters from the same or different strings
bool isEqualStrings(string arr[], int N)
{
    // Stores length of string
    int M = arr[0].length();

    // Store frequency of each distinct
    // character of the strings
    int cntFreq[256] = { 0 };

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Iterate over the characters
        for (int j = 0; j < M; j++) {

            // Update frequency
            // of arr[i][j]
            cntFreq[arr[i][j] - 'a']++;
        }
    }

    // Traverse the array cntFreq[]
    for (int i = 0; i < 256; i++) {

        // If cntFreq[i] is
        // divisible by N or not
        if (cntFreq[i] % N != 0) {

            return false;
        }
    }

    return true;
}

// Driver Code
int main()
{
    string arr[] = { "aab", "bbc", "cca" };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    if (isEqualStrings(arr, N)) {

        cout << "YES";
    }
    else {

        cout << "NO";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach 
class GFG{

// Function to check if all strings can be
// made equal by swapping any pair of
// characters from the same or different strings
static boolean isEqualStrings(String[] arr, int N)
{

    // Stores length of string
    int M = arr[0].length();

    // Store frequency of each distinct
    // character of the strings
    int[] cntFreq = new int[256];
    for(int i = 0; i < N; i++)
    {
        cntFreq[i] = 0;
    }

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Iterate over the characters
        for(int j = 0; j < M; j++)
        {

            // Update frequency
            // of arr[i].charAt(j)
            cntFreq[arr[i].charAt(j) - 'a'] += 1;
        }
    }

    // Traverse the array cntFreq[]
    for(int i = 0; i < 256; i++)
    {

        // If cntFreq[i] is
        // divisible by N or not
        if (cntFreq[i] % N != 0)
        {
            return false;
        }
    }
    return true;
}

// Driver Code
public static void main(String[] args)
{
    String[] arr = { "aab", "bbc", "cca" };
    int N = arr.length;

    // Function Call
    if (isEqualStrings(arr, N))
    {
        System.out.println("YES");
    }
    else
    {
        System.out.println("NO");
    }
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if all strings can
# be made equal by swapping any pair of
# characters from the same or different
# strings
def isEqualStrings(arr, N):

    # Stores length of string
    M = len(arr[0])

    # Store frequency of each distinct
    # character of the strings
    cntFreq = [0] * 256

    # Traverse the array
    for i in range(N):

        # Iterate over the characters
        for j in range(M): 

            # Update frequency
            # of arr[i][j]
            cntFreq[ord(arr[i][j]) - ord('a')] += 1

    # Traverse the array cntFreq[]
    for i in range(256):

        # If cntFreq[i] is
        # divisible by N or not
        if (cntFreq[i] % N != 0):
            return False

    return True

# Driver Code
if __name__ == "__main__" :

    arr = [ "aab", "bbc", "cca" ]
    N = len(arr)

    # Function Call
    if isEqualStrings(arr, N):
        print("YES")
    else:
        print("NO")

# This code is contributed by jana_sayantan
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to check if all strings can be
// made equal by swapping any pair of
// characters from the same or different strings
static bool isEqualStrings(string[] arr, int N)
{

    // Stores length of string
    int M = arr[0].Length;

    // Store frequency of each distinct
    // character of the strings
    int[] cntFreq = new int[256];
    for(int i = 0; i < N; i++)
    {
        cntFreq[i] = 0;
    }

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Iterate over the characters
        for(int j = 0; j < M; j++)
        {

            // Update frequency
            // of arr[i][j]
            cntFreq[arr[i][j] - 'a'] += 1;
        }
    }

    // Traverse the array cntFreq[]
    for(int i = 0; i < 256; i++)
    {

        // If cntFreq[i] is
        // divisible by N or not
        if (cntFreq[i] % N != 0)
        {
            return false;
        }
    }
    return true;
}

// Driver Code
public static void Main()
{
    string[] arr = { "aab", "bbc", "cca" };
    int N = arr.Length;

    // Function Call
    if (isEqualStrings(arr, N))
    {
        Console.WriteLine("YES");
    }
    else
    {
        Console.WriteLine("NO");
    }
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// javascript program of the above approach

// Function to check if all strings can be
// made equal by swapping any pair of
// characters from the same or different strings
function isEqualStrings(arr, N)
{

    // Stores length of string
    let M = arr[0].length;

    // Store frequency of each distinct
    // character of the strings
    let cntFreq = new Array(256).fill(0);
    for(let i = 0; i < N; i++)
    {
        cntFreq[i] = 0;
    }

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // Iterate over the characters
        for(let j = 0; j < M; j++)
        {

            // Update frequency
            // of arr[i].charAt(j)
            cntFreq[arr[i][j] - 'a'] += 1;
        }
    }

    // Traverse the array cntFreq[]
    for(let i = 0; i < 256; i++)
    {

        // If cntFreq[i] is
        // divisible by N or not
        if (cntFreq[i] % N != 0)
        {
            return false;
        }
    }
    return true;
}

    // Driver Code

    let arr = [ "aab", "bbc", "cca" ];
    let N = arr.length;

    // Function Call
    if (isEqualStrings(arr, N))
    {
        document.write("YES");
    }
    else
    {
        document.write("NO");
    }

// This code is contributed by target_2.
</script>
```

**Output:** 

```
YES
```

***时间复杂度** : O(N * M + 256)，其中 **M** 为弦的长度*
***辅助空间:** O(256)*