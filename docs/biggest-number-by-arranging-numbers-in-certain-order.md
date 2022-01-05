# 按一定顺序排列的最大数字

> 原文:[https://www . geesforgeks . org/按一定顺序排列最大数字/](https://www.geeksforgeeks.org/biggest-number-by-arranging-numbers-in-certain-order/)

给定一组 n 个数字。以产生最大价值的方式排列它们。同时应该分别保持偶数相对于彼此的顺序和奇数相对于彼此的顺序。
**例:**

```
Input : {78, 81, 88, 79, 117, 56}
Output : 8179788856117
The numbers are arranged in the order:
81 79 78 88 56 117 and then 
concatenated.
The odd numbers 81 79 117 and
The even numbers 78 88 56 maintain
their orders as in the original array.

Input : {400, 99, 76, 331, 65, 18}
Output : 99400763316518
```

这个问题是问题[的变型，将给定的数字排列成最大的数字](https://www.geeksforgeeks.org/given-an-array-of-numbers-arrange-the-numbers-to-form-the-biggest-number/)。在这个问题中，我们找到了具有一定限制的最大数，即奇数和偶数的顺序需要在最终结果中保持，因此目标是有一个 O(n)时间复杂度的解。
以下是寻找保持奇数和偶数顺序的最大数的步骤。

1.  将原数组的个数分成 2 个数组**偶数[]****奇数[]** 。同时划分数字的顺序应该保持。
2.  合并**偶数**和**奇数**数组，合并时遵循条件。设 X 是一个数组的元素，Y 是另一个数组的元素。比较**XY**(X 后加 Y)和**YX**(Y 后加 X)。如果 XY 较大，则将 X 加到最终结果上，否则将 Y 加到最终结果上。

## C++

```
// C++ implementation to form the biggest number
// by arranging numbers in certain order
#include <bits/stdc++.h>
using namespace std;

// function to merge the even and odd list
// to form the biggest number
string merge(vector<string> arr1, vector<string> arr2)
{
    int n1 = arr1.size();
    int n2 = arr2.size();
    int i = 0, j = 0;

    // to store the final biggest number
    string big = "";

    while (i < n1 && j < n2)
    {
        // if true then add arr1[i] to big
        if ((arr1[i]+arr2[j]).compare((arr2[j]+arr1[i])) > 0)
            big += arr1[i++];

        // else add arr2[j] to big
        else
            big += arr2[j++];
    }

    // add remaining elements
    // of arr1 to big
    while (i < n1)
        big += arr1[i++];

    // add remaining elements
    // of arr2 to big
    while (j < n2)
        big += arr2[j++] ;

    return big;
}

// function to find the biggest number
string printLargest(vector<string> arr, int n)
{
    vector<string> even, odd;

    for (int i=0; i<n; i++)
    {
        int lastDigit = arr[i].at(arr[i].size() - 1) - '0';

        // inserting even numbers
        if (lastDigit % 2 == 0)
            even.push_back(arr[i]);

        // inserting odd numbers
        else
            odd.push_back(arr[i]);
    }

    // merging both the array
    string biggest = merge(even, odd);

    // final required biggest number
    return biggest;
}

// Driver program to test above
int main()
{
    // arr[] = {78, 81, 88, 79, 117, 56}
    vector<string> arr;
    arr.push_back("78");
    arr.push_back("81");
    arr.push_back("88");
    arr.push_back("79");
    arr.push_back("117");
    arr.push_back("56");

    int n = arr.size();
    cout << "Biggest number = "
         << printLargest(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Vector;

// Java implementation to form the biggest number
// by arranging numbers in certain order
class GFG
{

    // function to merge the even and odd list
    // to form the biggest number
    static String merge(Vector<String> arr1,
                        Vector<String> arr2)
    {
        int n1 = arr1.size();
        int n2 = arr2.size();
        int i = 0, j = 0;

        // to store the final biggest number
        String big = "";

        while (i < n1 && j < n2)
        {

            // if true then add arr1[i] to big
            if ((arr1.get(i) + arr2.get(j)).
                    compareTo((arr2.get(j) + arr1.get(i))) > 0)
            {
                big += arr1.get(i++);
            }

            // else add arr2[j] to big
            else
            {
                big += arr2.get(j++);
            }
        }

        // add remaining elements
        // of arr1 to big
        while (i < n1)
        {
            big += arr1.get(i++);
        }

        // add remaining elements
        // of arr2 to big
        while (j < n2)
        {
            big += arr2.get(j++);
        }
        return big;
    }

    // function to find the biggest number
    static String printLargest(Vector<String> arr, int n)
    {
        Vector<String> even = new Vector<String>(),
                        odd = new Vector<String>();

        for (int i = 0; i < n; i++)
        {
            int lastDigit = arr.get(i).
                charAt(arr.get(i).length() - 1) - '0';

            // inserting even numbers
            if (lastDigit % 2 == 0)
            {
                even.add(arr.get(i));
            }

            // inserting odd numbers
            else
            {
                odd.add(arr.get(i));
            }
        }

        // merging both the array
        String biggest = merge(even, odd);

        // final required biggest number
        return biggest;
    }

    // Driver code
    public static void main(String[] args)
    {
        Vector<String> arr = new Vector<String>();
        arr.add("78");
        arr.add("81");
        arr.add("88");
        arr.add("79");
        arr.add("117");
        arr.add("56");

        int n = arr.size();
        System.out.println("Biggest number = " +
                            printLargest(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation to form the biggest number
// by arranging numbers in certain order
using System;
using System.Collections.Generic;

class GFG
{

    // function to merge the even and odd list
    // to form the biggest number
    static String merge(List<String> arr1,
                        List<String> arr2)
    {
        int n1 = arr1.Count;
        int n2 = arr2.Count;
        int i = 0, j = 0;

        // to store the final biggest number
        String big = "";

        while (i < n1 && j < n2)
        {

            // if true then Add arr1[i] to big
            if ((arr1[i] + arr2[j]).CompareTo((arr2[j] +
                                               arr1[i])) > 0)
            {
                big += arr1[i++];
            }

            // else Add arr2[j] to big
            else
            {
                big += arr2[j++];
            }
        }

        // Add remaining elements
        // of arr1 to big
        while (i < n1)
        {
            big += arr1[i++];
        }

        // Add remaining elements
        // of arr2 to big
        while (j < n2)
        {
            big += arr2[j++];
        }
        return big;
    }

    // function to find the biggest number
    static String printLargest(List<String> arr, int n)
    {
        List<String> even = new List<String>(),
                     odd = new List<String>();

        for (int i = 0; i < n; i++)
        {
            int lastDigit = arr[i][arr[i].Length - 1] - '0';

            // inserting even numbers
            if (lastDigit % 2 == 0)
            {
                even.Add(arr[i]);
            }

            // inserting odd numbers
            else
            {
                odd.Add(arr[i]);
            }
        }

        // merging both the array
        String biggest = merge(even, odd);

        // final required biggest number
        return biggest;
    }

    // Driver code
    public static void Main()
    {
        List<String> arr = new List<String>();
        arr.Add("78");
        arr.Add("81");
        arr.Add("88");
        arr.Add("79");
        arr.Add("117");
        arr.Add("56");

        int n = arr.Count;
        Console.WriteLine("Biggest number = " +
                           printLargest(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript implementation to form the biggest number
// by arranging numbers in certain order

// function to merge the even and odd list
// to form the biggest number
function merge(arr1, arr2)
{
    let n1 = arr1.length;
    let n2 = arr2.length;
    let i = 0, j = 0;

    // to store the final biggest number
    let big = "";

    while (i < n1 && j < n2)
    {

        // if true then add arr1[i] to big
        if ((arr1[i]+arr2[j]).localeCompare((arr2[j]+arr1[i])) > 0)
            big += arr1[i++];

        // else add arr2[j] to big
        else
            big += arr2[j++];
    }

    // add remaining elements
    // of arr1 to big
    while (i < n1)
        big += arr1[i++];

    // add remaining elements
    // of arr2 to big
    while (j < n2)
        big += arr2[j++] ;

    return big;
}

// function to find the biggest number
function printLargest(arr, n)
{
    let even = [];
    let odd = [];

    for (let i=0; i<n; i++)
    {
        let lastDigit = arr[i].charCodeAt(arr[i].length - 1) - '0';

        // inserting even numbers
        if (lastDigit % 2 == 0)
            even.push(arr[i]);

        // inserting odd numbers
        else
            odd.push(arr[i]);
    }

    // merging both the array
    let biggest = merge(even, odd);

    // final required biggest number
    return biggest;
}

// Driver program to test above
    // arr[] = {78, 81, 88, 79, 117, 56}
    let arr = [];
    arr.push("78");
    arr.push("81");
    arr.push("88");
    arr.push("79");
    arr.push("117");
    arr.push("56");

    let n = arr.length;
    document.write("Biggest number = "
        + printLargest(arr, n));

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
8179788856117
```

**时间复杂度:** O(n)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。