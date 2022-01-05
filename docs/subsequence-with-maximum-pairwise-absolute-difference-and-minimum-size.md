# 具有最大成对绝对差和最小尺寸的子序列

> 原文:[https://www . geesforgeks . org/subsequence-with-maximum-pair-绝对差值和-minimum-size/](https://www.geeksforgeeks.org/subsequence-with-maximum-pairwise-absolute-difference-and-minimum-size/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是打印给定数组中相邻元素最大成对绝对差的子序列。如果存在多个这样的子序列，则打印具有最小长度的子序列。

**示例:**

> **输入:** arr[] = {1，2，4，3，5}
> **输出:** 1 4 3 5
> **解释:**
> 对于子序列{1，4，3，5}，
> 相邻对之间的绝对差为| 1–4 |+| 4–3 |+| 3–5 | = 6，这是最大可能的绝对差。
> 
> **输入:** arr[] = {1，2，5，6，3，4}
> **输出:** {1，6，4}
> **解释:**
> 对于子序列{1，6，4}，
> 相邻对之间的绝对差为| 1–6 |+| 6–4 | = 7，这是最大可能的绝对差。

**方法:**对于绝对差值最大的子序列，步骤如下:

1.  创建新的数组(比如 **ans[]** )来存储所需子序列的所有元素。
2.  插入数组 arr[]的第一个元素。
3.  找出数组中除第一个和最后一个元素之外的所有局部最小值和最大值，并插入到数组中 **ans[]** 。
4.  插入数组的最后一个元素 **arr[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the subsequence
// with maximum absolute difference
void getSubsequence(vector<int> ar)
{
    int N = ar.size();

    // To store the resultant subsequence
    vector<int> ans;

    // First element should be included
    // in the subsequence
    ans.push_back(ar[0]);

    // Traverse the given array arr[]
    for (int i = 1; i < N - 1; i++) {

        // If current element is greater
        // than the previous element
        if (ar[i] > ar[i - 1]) {

            // If the current element is
            // not the local maxima
            // then continue
            if (i < N - 1
                && ar[i] <= ar[i + 1]) {
                continue;
            }

            // Else push it in subsequence
            else {
                ans.push_back(ar[i]);
            }
        }

        // If the current element is less
        // then the previous element
        else {

            // If the current element is
            // not the local minima
            // then continue
            if (i < N - 1
                && ar[i + 1] < ar[i]) {
                continue;
            }

            // Else push it in subsequence
            else {
                ans.push_back(ar[i]);
            }
        }
    }

    // Last element should also be
    // included in subsequence
    ans.push_back(ar[N - 1]);

    // Print the element
    for (auto& it : ans)
        cout << it << ' ';
}

// Driver Code
int main()
{
    // Given array
    vector<int> arr = { 1, 2, 4, 3, 5 };

    // Function Call
    getSubsequence(arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the subsequence
// with maximum absolute difference
static void getSubsequence(int []ar)
{
    int N = ar.length;

    // To store the resultant subsequence
    Vector<Integer> ans = new Vector<Integer>();

    // First element should be included
    // in the subsequence
    ans.add(ar[0]);

    // Traverse the given array arr[]
    for(int i = 1; i < N - 1; i++)
    {

       // If current element is greater
       // than the previous element
       if (ar[i] > ar[i - 1])
       {

           // If the current element is
           // not the local maxima
           // then continue
           if (i < N - 1 && ar[i] <= ar[i + 1])
           {
               continue;
           }

           // Else push it in subsequence
           else
           {
               ans.add(ar[i]);
           }
       }

       // If the current element is less
       // then the previous element
       else
       {

           // If the current element is
           // not the local minima
           // then continue
           if (i < N - 1 && ar[i + 1] < ar[i])
           {
               continue;
           }

           // Else push it in subsequence
           else
           {
               ans.add(ar[i]);
           }
       }
    }

    // Last element should also be
    // included in subsequence
    ans.add(ar[N - 1]);

    // Print the element
    for(int it : ans)
       System.out.print(it + " ");
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int []arr = { 1, 2, 4, 3, 5 };

    // Function Call
    getSubsequence(arr);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the subsequence
# with maximum absolute difference
def getSubsequence(ar):

    N = len(ar)

    # To store the resultant subsequence
    ans = []

    # First element should be included
    # in the subsequence
    ans.append(ar[0])

    # Traverse the given array arr[]
    for i in range(1, N - 1):

        # If current element is greater
        # than the previous element
        if (ar[i] > ar[i - 1]):

            # If the current element is
            # not the local maxima
            # then continue
            if(i < N - 1 and
               ar[i] <= ar[i + 1]):
                continue

            # Else push it in subsequence
            else:
                ans.append(ar[i])

        # If the current element is less
        # then the previous element
        else:

            # If the current element is
            # not the local minima
            # then continue
            if (i < N - 1 and
                 ar[i + 1] < ar[i]):
                continue

                # Else push it in subsequence
            else:
                ans.append(ar[i])

    # Last element should also be
    # included in subsequence
    ans.append(ar[N - 1])

    # Print the element
    for it in ans:
        print(it, end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 1, 2, 4, 3, 5 ]

    # Function Call
    getSubsequence(arr)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the subsequence
// with maximum absolute difference
static void getSubsequence(int []ar)
{
    int N = ar.Length;

    // To store the resultant subsequence
    List<int> ans = new List<int>();

    // First element should be included
    // in the subsequence
    ans.Add(ar[0]);

    // Traverse the given array []arr
    for(int i = 1; i < N - 1; i++)
    {

        // If current element is greater
        // than the previous element
        if (ar[i] > ar[i - 1])
        {

            // If the current element is
            // not the local maxima
            // then continue
            if (i < N - 1 && ar[i] <= ar[i + 1])
            {
                continue;
            }

            // Else push it in subsequence
            else
            {
                ans.Add(ar[i]);
            }
        }

        // If the current element is less
        // then the previous element
        else
        {

            // If the current element is
            // not the local minima
            // then continue
            if (i < N - 1 && ar[i + 1] < ar[i])
            {
                continue;
            }

            // Else push it in subsequence
            else
            {
                ans.Add(ar[i]);
            }
        }
    }

    // Last element should also be
    // included in subsequence
    ans.Add(ar[N - 1]);

    // Print the element
    foreach(int it in ans)
        Console.Write(it + " ");
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 1, 2, 4, 3, 5 };

    // Function Call
    getSubsequence(arr);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the subsequence
    // with maximum absolute difference
    function getSubsequence(ar)
    {
        let N = ar.length;

        // To store the resultant subsequence
        let ans = [];

        // First element should be included
        // in the subsequence
        ans.push(ar[0]);

        // Traverse the given array arr[]
        for(let i = 1; i < N - 1; i++)
        {

           // If current element is greater
           // than the previous element
           if (ar[i] > ar[i - 1])
           {

               // If the current element is
               // not the local maxima
               // then continue
               if (i < N - 1 && ar[i] <= ar[i + 1])
               {
                   continue;
               }

               // Else push it in subsequence
               else
               {
                   ans.push(ar[i]);
               }
           }

           // If the current element is less
           // then the previous element
           else
           {

               // If the current element is
               // not the local minima
               // then continue
               if (i < N - 1 && ar[i + 1] < ar[i])
               {
                   continue;
               }

               // Else push it in subsequence
               else
               {
                   ans.push(ar[i]);
               }
           }
        }

        // Last element should also be
        // included in subsequence
        ans.push(ar[N - 1]);

        // Print the element
        for(let it = 0; it < ans.length; it++)
           document.write(ans[it] + " ");
    }

    // Given array
    let arr = [ 1, 2, 4, 3, 5 ];

    // Function Call
    getSubsequence(arr);

</script>
```

**Output:** 

```
1 4 3 5
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*