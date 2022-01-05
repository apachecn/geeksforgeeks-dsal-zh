# 按照字符 ASCII 值总和的递增顺序对字符串数组进行排序

> 原文:[https://www . geeksforgeeks . org/sort-字符串数组-按 ascii 字符值总和递增的顺序/](https://www.geeksforgeeks.org/sort-an-array-of-strings-in-increasing-order-of-sum-of-ascii-values-of-characters/)

给定一个由**N**T6】字符串组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是按照字符的 ASCII 值之和的递增顺序对[字符串](https://www.geeksforgeeks.org/string-data-structure/)进行排序。

**示例:**

> **输入:**arr[]= {“for”、“极客”、“app”、“best”}
> **输出:** app for best 极客
> **解释:**
> 各字符串字符的 ASCII 值之和为:{327，527，321，430}。
> 因此，字符串的排序顺序是{“app”、“for”、“best”、“geeks”}。
> 
> **输入:**arr[]= {“geeks forgeeks”、“a”、“computer”、“science”、“portal”、“for”、“geeks”}
> **输出:** a 为 geeks portal science computer geeks forgeeks
> **说明:**
> 各字符串字符的 ASCII 值之和为:{1381、97、879、730、658、327、527}。
> 因此，排序顺序为{“a”、“for”、“极客”、“门户”、“科学”、“计算机”、“极客 forgeeks”}。

**方法:**想法是使用辅助的[数组](https://www.geeksforgeeks.org/array-data-structure/)来存储字符串对及其各自的字符 ASCII 值之和。然后，根据对中的第一个值对数组进行排序，然后打印排序后的字符串。按照以下步骤解决问题:

*   初始化一对、**和**的[向量，将字符串的值和字符串本身存储为一对。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)
*   [使用变量 **i** : 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**
    *   找到**arr【I】**字符的 ASCII 值之和，并将其存储在一个变量中，比如 **val** 。
    *   在 **V** 中追加一对 **{val，arr[i]}** 。
*   [根据对](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)中的第一个值对向量 **V** 进行排序。
*   [使用变量 **i** : 在向量 **V** 上的范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，n-1】**中迭代
    *   打印字符串，即**v【I】. second .**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of ASCII
// value of all characters of a string
int getValue(string s)
{
    // Store the required result
    int sum = 0;

    // Traverse the string
    for (int i = 0; i < s.size(); i++) {
        sum += s[i];
    }

    // Return the sum
    return sum;
}

// Function to sort strings in increasing
// order of sum of their ASCII values
void sortStrings(string arr[], int n)
{

    // Store pairs of strings and
    // sum of their ASCII values
    vector<pair<int, string> > v;

    // Traverse the array, arr[]
    for (int i = 0; i < n; i++) {

        // Find the value of the string
        int val = getValue(arr[i]);

        // Append pair {val, arr[i]}
        v.push_back({ val, arr[i] });
    }

    // Sort the vector, V in increasing
    // order of the first value of pair
    sort(v.begin(), v.end());

    // Print the sorted strings
    for (int i = 0; i < n; i++) {
        cout << v[i].second << " ";
    }
}

// Driver Code
int main()
{

    // Given Input
    string arr[] = { "geeks", "for", "app", "best" };
    int n = 4;

    // Function Call
    sortStrings(arr, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the sum of ASCII
# value of all characters of a string
def getValue(s):

    # Store the required result
    sum = 0

    # Traverse the string
    for i in range(len(s)):
        sum += ord(s[i])

    # Return the sum
    return sum

# Function to sort strings in increasing
# order of sum of their ASCII values
def sortStrings(arr, n):

    # Store pairs of strings and
    # sum of their ASCII values
    v = []

    # Traverse the array, arr[]
    for i in range(n):

        # Find the value of the string
        val = getValue(arr[i])

        # Append pair {val, arr[i]}
        v.append([val, arr[i]])

    # Sort the vector, V in increasing
    # order of the first value of pair
    v = sorted(v)

    # Print the sorted strings
    for i in range(n):
        print(v[i][1], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ "geeks", "for", "app", "best" ]
    n = 4

    # Function Call
    sortStrings(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the sum of ASCII
// value of all characters of a string
static int getValue(String s)
{

    // Store the required result
    int sum = 0;

    // Traverse the string
    for(int i = 0; i < s.Length; i++)
    {
        sum += s[i];
    }

    // Return the sum
    return sum;
}

// Function to sort strings in increasing
// order of sum of their ASCII values
static void sortStrings(String[] arr, int n)
{

    // Store pairs of strings and
    // sum of their ASCII values
    List<Tuple<int,
               String>> v = new List<Tuple<int,
                                           String>>();

    // Traverse the array, arr[]
    for(int i = 0; i < n; i++)
    {

        // Find the value of the string
        int val = getValue(arr[i]);

        // Append pair {val, arr[i]}
        v.Add(new Tuple<int, String>(val, arr[i]));
    }

    // Sort the vector, V in increasing
    // order of the first value of pair
    v.Sort();

    // Print the sorted strings
    for(int i = 0; i < n; i++)
    {
        Console.Write(v[i].Item2 + " ");
    }
}

// Driver Code
static public void Main()
{

    // Given Input
    String[] arr = { "geeks", "for", "app", "best" };
    int n = 4;

    // Function Call
    sortStrings(arr, n);
}
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the sum of ASCII
// value of all characters of a string
function getValue(s)
{
    // Store the required result
    let sum = 0;

    // Traverse the string
    for (let i = 0; i < s.length; i++) {
        sum += s[i].charCodeAt(0);
    }

    // Return the sum
    return sum;
}

// Function to sort strings in increasing
// order of sum of their ASCII values
function sortStrings(arr, n)
{

    // Store pairs of strings and
    // sum of their ASCII values
    let v = [];

    // Traverse the array, arr[]
    for (let i = 0; i < n; i++) {

        // Find the value of the string
        let val = getValue(arr[i]);

        // Append pair {val, arr[i]}
        v.push([ val, arr[i] ]);
    }

    // Sort the vector, V in increasing
    // order of the first value of pair
    v.sort();

    // Print the sorted strings
    for (let i = 0; i < n; i++) {
        document.write(v[i][1] + " ");
    }
}

// Driver Code

    // Given Input
    let arr = ["geeks", "for", "app", "best" ];
    let n = 4;

    // Function Call
    sortStrings(arr, n);

</script>
```

**Output:** 

```
app for best geeks
```

***时间复杂度:** O(N*log(N) + N*M，其中 **M** 是数组中最长字符串的长度 **arr[]** 。*
***辅助空间:** O(N)*