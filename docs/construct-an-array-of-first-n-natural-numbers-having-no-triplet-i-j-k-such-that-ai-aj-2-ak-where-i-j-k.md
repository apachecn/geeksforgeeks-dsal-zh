# 构造一个没有三元组(I，j，k)的前 N 个自然数的数组，使得 a[i] + a[j] = 2* a[k]，其中 i < j < k

> 原文:[https://www . geeksforgeeks . org/construct-一组第一个 n 个自然数-有-无-三元组-I-j-k-so-ai-aj-2-AK-where-I-j-k/](https://www.geeksforgeeks.org/construct-an-array-of-first-n-natural-numbers-having-no-triplet-i-j-k-such-that-ai-aj-2-ak-where-i-j-k/)

给定一个正整数 **N** ，任务是使用第一个 **N** 自然数构建一个[数组](https://www.geeksforgeeks.org/vector-in-cpp-stl/)**a【】**，其中不包含满足 **a[k] * 2 = a[i] + a[j]** 和 **i < j < k** 的三元组 **(i，j，k)** 。

**示例:**

> **输入:** N = 3
> **输出:** {2，3，1 }
> **说明:**
> 由于满足条件的数组中不存在这样的三元组，所以需要的输出为{2，3，1 }。
> 
> **输入:** N = 10
> **输出:** { 8，4，6，10，2，7，3，5，9，1 }

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   递归查找结果数组的第一个 **(N / 2)** 元素和最后一个 **(N / 2)** 元素。
*   合并数组的两半，使得数组的前半部分包含[偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，数组的后半部分包含[奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。
*   最后，打印结果数组。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to construct the array of size N
// that contains no such triplet satisfying
// the given conditions
vector<int> constructArray(int N)
{

    // Base case
    if (N == 1) {

        return { 1 };
    }

    // Stores the first half
    // of the array
    vector<int> first
        = constructArray(N / 2);

    // Stores the last half
    // of the array
    vector<int> last
        = constructArray(N - (N / 2));

    // Stores the merged array
    vector<int> ans;

    // Insert even numbers
    for (auto e : first) {

        // Insert 2 * e
        ans.push_back(2 * e);
    }

    // Insert odd numbers
    for (auto o : last) {

        // Insert (2 * o - 1)
        ans.push_back((2 * o) - 1);
    }

    return ans;
}

// Function to print the resultant array
void printArray(vector<int> ans, int N)
{

    // Print resultant array
    cout << "{ ";
    for (int i = 0; i < N; i++) {

        // Print current element
        cout << ans[i];

        // If i is not the last index
        // of the resultant array
        if (i != N - 1) {
            cout << ", ";
        }
    }

    cout << " }";
}

// Driver Code
int main()
{
    int N = 10;

    // Store the resultant array
    vector<int> ans
        = constructArray(N);

    printArray(ans, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to construct the array of size N
// that contains no such triplet satisfying
// the given conditions
static ArrayList<Integer> constructArray(int N)
{

    // Base case
    if (N == 1)
    {
        ArrayList<Integer> a = new ArrayList<Integer>(1);
        a.add(1);
        return a;
    }

    // Stores the first half
    // of the array
    ArrayList<Integer> first = new ArrayList<Integer>(N);
    first = constructArray(N / 2);

    // Stores the last half
    // of the array
    ArrayList<Integer> last = new ArrayList<Integer>(N);
    last = constructArray(N - N / 2);

    ArrayList<Integer> ans = new ArrayList<Integer>(N);

    // Insert even numbers
    for(int i = 0; i < first.size(); i++)
    {

        // Insert 2 * first[i]
        ans.add(2 * first.get(i));
    }

    // Insert odd numbers
    for(int i = 0; i < last.size(); i++)
    {

        // Insert (2 * last[i] - 1)
        ans.add(2 * last.get(i) - 1);
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int N = 10;

    ArrayList<Integer> answer = new ArrayList<Integer>(N);
    answer = constructArray(N);

    System.out.print("{");
    for(int i = 0; i < answer.size(); i++)
    {
        System.out.print(answer.get(i));
        System.out.print(", ");
    }
    System.out.print("}");
}   
}

// This code is contributed by koulick_sadhu
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to construct the array of size N
# that contains no such triplet satisfying
# the given conditions
def constructArray(N) :

    # Base case
    if (N == 1) :
        a = []
        a.append(1)
        return a;

    # Stores the first half
    # of the array
    first = constructArray(N // 2);

    # Stores the last half
    # of the array
    last = constructArray(N - (N // 2));

    # Stores the merged array
    ans = [];

    # Insert even numbers
    for e in first :

        # Insert 2 * e
        ans.append(2 * e);

    # Insert odd numbers
    for o in last:

        # Insert (2 * o - 1)
        ans.append((2 * o) - 1);

    return ans;

# Function to print the resultant array
def printArray(ans, N) :

    # Print resultant array
    print("{ ", end = "");
    for i in range(N) :

        # Print current element
        print(ans[i], end = "");

        # If i is not the last index
        # of the resultant array
        if (i != N - 1) :
            print(", ",end = "");

    print(" }", end = "");

# Driver Code
if __name__ == "__main__" :
    N = 10;

    # Store the resultant array
    ans = constructArray(N);

    printArray(ans, N);

       # This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to construct the array of size N
// that contains no such triplet satisfying
// the given conditions
static List<int> constructArray(int N)
{

    // Base case
    if (N == 1)
    {
        List<int> a = new List<int>(1);
        a.Add(1);
        return a;
    }

    // Stores the first half
    // of the array
    List<int> first = new List<int>();
    first = constructArray(N / 2);

    // Stores the last half
    // of the array
    List<int> last = new List<int>();

    last = constructArray(N - N / 2);

    List<int> ans = new List<int>();

    // Insert even numbers
    for(int i = 0; i < first.Count; i++)
    {

        // Insert 2 * first[i]
        ans.Add(2 * first[i]);
    }

    // Insert odd numbers
    for(int i = 0; i < last.Count; i++)
    {

        // Insert (2 * last[i] - 1)
        ans.Add(2 * last[i] - 1);
    }
    return ans;
}

// Driver code
public static void Main()
{
    int N = 10;

    List<int> answer = new List<int>(N);
    answer = constructArray(N);

    Console.Write("{");
    for(int i = 0; i < answer.Count; i++)
    {
        Console.Write(answer[i]);
        Console.Write(", ");
    }
    Console.Write("}");
}   
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

    // JavaScript program to implement the above approach

    // Function to construct the array of size N
    // that contains no such triplet satisfying
    // the given conditions
    function constructArray(N)
    {

        // Base case
        if (N == 1)
        {
            let a = [];
            a.push(1);
            return a;
        }

        // Stores the first half
        // of the array
        let first = [];
        first = constructArray(parseInt(N / 2, 10));

        // Stores the last half
        // of the array
        let last = [];

        last = constructArray(N - parseInt(N / 2, 10));

        let ans = [];

        // Insert even numbers
        for(let i = 0; i < first.length; i++)
        {

            // Insert 2 * first[i]
            ans.push(2 * first[i]);
        }

        // Insert odd numbers
        for(let i = 0; i < last.length; i++)
        {

            // Insert (2 * last[i] - 1)
            ans.push(2 * last[i] - 1);
        }
        return ans;
    }

    let N = 10;

    let answer = [];
    answer = constructArray(N);

    document.write("{");
    for(let i = 0; i < answer.length; i++)
    {
        document.write(answer[i]);
        document.write(", ");
    }
    document.write("}");

</script>
```

**Output:** 

```
{ 8, 4, 6, 10, 2, 7, 3, 5, 9, 1 }
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*