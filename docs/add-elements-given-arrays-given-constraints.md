# 用给定的约束添加给定数组的元素

> 原文:[https://www . geesforgeks . org/add-elements-给定-arrays-给定-constraints/](https://www.geeksforgeeks.org/add-elements-given-arrays-given-constraints/)

给定两个整数数组，通过满足以下约束将它们的元素添加到第三个数组中–
1。应该从两个数组的第 0 个索引开始添加。
2。如果总和不是单个数字，则将其拆分，并将数字存储在输出数组的相邻位置。
3。输出数组应该容纳较大输入数组的任何剩余数字。

**示例:**

```
Input: 
a = [9, 2, 3, 7, 9, 6]
b = [3, 1, 4, 7, 8, 7, 6, 9]
Output: 
[1, 2, 3, 7, 1, 4, 1, 7, 1, 3, 6, 9]

Input:     
a = [9343, 2, 3, 7, 9, 6]
b = [34, 11, 4, 7, 8, 7, 6, 99]
Output: 
[9, 3, 7, 7, 1, 3, 7, 1, 4, 1, 7, 1, 3, 6, 9, 9]

Input:     
a = []
b = [11, 2, 3 ]
Output: 
[1, 1, 2, 3 ]

Input: 
a = [9, 8, 7, 6, 5, 4, 3, 2, 1]
b = [1, 2, 3, 4, 5, 6, 7, 8, 9]
Output: 
[1, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0]
```

**难度等级:**菜鸟

想法很简单。我们维护一个输出数组，并从两个数组的第 0 个索引运行一个循环。对于循环的每次迭代，我们考虑两个数组中的下一个元素并添加它们。如果总和大于 9，我们将总和的单个数字推送到输出数组，否则我们将推总和本身。最后，我们将较大输入数组的剩余元素推送到输出数组。

以下是上述想法的实现:

## C++

```
// C++ program to add two arrays following given
// constraints
#include<bits/stdc++.h>
using namespace std;

// Function to push individual digits of a number
// to output vector from left to right
void split(int num, vector<int> &out)
{
    vector<int> arr;
    while (num)
    {
        arr.push_back(num%10);
        num = num/10;
    }
    // reverse the vector arr and append it to output vector
    out.insert(out.end(), arr.rbegin(), arr.rend());
}

// Function to add two arrays keeping given
// constraints
void addArrays(int arr1[], int arr2[], int m, int n)
{
    // create a vector to store output
    vector<int> out;

    // maintain a variable to store current index in
    // both arrays
    int i = 0;

    // loop till arr1 or arr2 runs out
    while (i < m && i < n)
    {
        // read next elements from both arrays and
        // add them
        int sum = arr1[i] + arr2[i];

        // if sum is single digit number
        if (sum < 10)
            out.push_back(sum);

        else
        {
            // if sum is not a single digit number, push
            // individual digits to output vector
            split(sum, out);
        }

        // increment to next index
        i++;
    }

    // push remaining elements of first input array
    // (if any) to output vector
    while (i < m)
        split(arr1[i++], out);

    // push remaining elements of second input array
    // (if any) to output vector
    while (i < n)
        split(arr2[i++], out);

    // print the output vector
    for (int x : out)
        cout << x << " ";
}

// Driver code
int main()
{
    int arr1[] = {9343, 2, 3, 7, 9, 6};
    int arr2[] = {34, 11, 4, 7, 8, 7, 6, 99};

    int m = sizeof(arr1) / sizeof(arr1[0]);
    int n = sizeof(arr2) / sizeof(arr2[0]);

    addArrays(arr1, arr2, m, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to add two arrays following given
// constraints
import java.util.Vector;

class GFG
{

    // Function to push individual digits of a number
    // to output vector from left to right
    static void split(int num, Vector<Integer> out)
    {
        Vector<Integer> arr = new Vector<>();
        while (num > 0)
        {
            arr.add(num % 10);
            num /= 10;
        }

        // reverse the vector arr and
        // append it to output vector
        for (int i = arr.size() - 1; i >= 0; i--)
            out.add(arr.elementAt(i));
    }

    // Function to add two arrays keeping given
    // constraints
    static void addArrays(int[] arr1, int[] arr2,
                          int m, int n)
    {

        // create a vector to store output
        Vector<Integer> out = new Vector<>();

        // maintain a variable to store
        //  current index in both arrays
        int i = 0;

        // loop till arr1 or arr2 runs out
        while (i < m && i < n)
        {

            // read next elements from both arrays
            // and add them
            int sum = arr1[i] + arr2[i];

            // if sum is single digit number
            if (sum < 10)
                out.add(sum);
            else

                // if sum is not a single digit number,
                // push individual digits to output vector
                split(sum, out);

            // increment to next index
            i++;
        }

        // push remaining elements of first input array
        // (if any) to output vector
        while (i < m)
            split(arr1[i++], out);

        // push remaining elements of second input array
        // (if any) to output vector
        while (i < n)
            split(arr2[i++], out);

        // print the output vector
        for (int x : out)
            System.out.print(x + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr1 = { 9343, 2, 3, 7, 9, 6 };
        int[] arr2 = { 34, 11, 4, 7, 8, 7, 6, 99 };

        int m = arr1.length;
        int n = arr2.length;

        addArrays(arr1, arr2, m, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## C#

```
// C# program to add two arrays following given
// constraints
using System;
using System.Collections.Generic;

class GFG
{

    // Function to push individual digits of a number
    // to output vector from left to right
    static void split(int num, List<int> outs)
    {
        List<int> arr = new List<int>();
        while (num > 0)
        {
            arr.Add(num % 10);
            num /= 10;
        }

        // reverse the vector arr and
        // append it to output vector
        for (int i = arr.Count - 1; i >= 0; i--)
            outs.Add(arr[i]);
    }

    // Function to add two arrays keeping given
    // constraints
    static void addArrays(int[] arr1, int[] arr2,
                        int m, int n)
    {

        // create a vector to store output
        List<int> outs = new List<int>();

        // maintain a variable to store
        // current index in both arrays
        int i = 0;

        // loop till arr1 or arr2 runs out
        while (i < m && i < n)
        {

            // read next elements from both arrays
            // and add them
            int sum = arr1[i] + arr2[i];

            // if sum is single digit number
            if (sum < 10)
                outs.Add(sum);
            else

                // if sum is not a single digit number,
                // push individual digits to output vector
                split(sum, outs);

            // increment to next index
            i++;
        }

        // push remaining elements of first input array
        // (if any) to output vector
        while (i < m)
            split(arr1[i++], outs);

        // push remaining elements of second input array
        // (if any) to output vector
        while (i < n)
            split(arr2[i++], outs);

        // print the output vector
        foreach (int x in outs)
            Console.Write(x + " ");
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr1 = { 9343, 2, 3, 7, 9, 6 };
        int[] arr2 = { 34, 11, 4, 7, 8, 7, 6, 99 };

        int m = arr1.Length;
        int n = arr2.Length;

        addArrays(arr1, arr2, m, n);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to add two arrays
// following given constraints

// Function to push individual digits
// of a number to output vector from
// left to right
function split(num, out)
{
    let arr = [];
    while (num)
    {
        arr.push(num % 10);
        num = Math.floor(num / 10);
    }

    for(let i = arr.length - 1; i >= 0; i--)
        out.push(arr[i]);
}

// Function to add two arrays keeping given
// constraints
function addArrays(arr1, arr2, m, n)
{

    // Create a vector to store output
    let out = [];

    // Maintain a variable to store
    // current index in both arrays
    let i = 0;

    // Loop till arr1 or arr2 runs out
    while (i < m && i < n)
    {

        // Read next elements from both
        // arrays and add them
        let sum = arr1[i] + arr2[i];

        // If sum is single digit number
        if (sum < 10)
            out.push(sum);

        else
        {

            // If sum is not a single digit
            // number, push individual digits
            // to output vector
            split(sum, out);
        }

        // Increment to next index
        i++;
    }

    // Push remaining elements of first
    // input array (if any) to output vector
    while (i < m)
        split(arr1[i++], out);

    // Push remaining elements of second
    // input array (if any) to output vector
    while (i < n)
        split(arr2[i++], out);

    // Print the output vector
    for(let x of out)
        document.write(x + " ");
}

// Driver code
let arr1 = [ 9343, 2, 3, 7, 9, 6 ];
let arr2 = [ 34, 11, 4, 7, 8, 7, 6, 99 ];

let m = arr1.length;
let n = arr2.length;

addArrays(arr1, arr2, m, n);

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
9 3 7 7 1 3 7 1 4 1 7 1 3 6 9 9
```

**上述解的时间复杂度**为 O(m + n)，因为我们正好遍历两个数组一次。

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。