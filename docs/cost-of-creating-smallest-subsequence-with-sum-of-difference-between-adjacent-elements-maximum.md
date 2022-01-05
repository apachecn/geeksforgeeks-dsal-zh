# 创建相邻元素间差值之和最大的最小子序列的成本

> 原文:[https://www . geeksforgeeks . org/创建最小子序列的成本-相邻元素之间的差值总和-最大值/](https://www.geeksforgeeks.org/cost-of-creating-smallest-subsequence-with-sum-of-difference-between-adjacent-elements-maximum/)

给定两个 **N** 整数数组**arr【】**和**costArray【】**，表示与每个元素相关的移除成本。任务是从给定的最小成本数组中找到子序列，使得相邻元素之间的差值之和最大。移除每一个元素都会产生成本。
**示例:**

> **输入:** N = 3，arr[] = { 3，2，1 }，costArray[] = {0，1，0}
> **输出:** 4，1
> **解释:**
> 至少有 4 个长度为 2 的子序列:
> 【3，2】给出我们| 3–2 | = 1
> 【3，1】给出我们| 3–1 | = 2
> 【2， 1 ]给我们| 2–1 | = 1
> [ 3，2，1 ]给我们| 3–2 |+| 2–1 | = 2
> 所以答案要么是[ 3，1 ]要么是[3，2，1 ]。 因为我们希望子序列尽可能短，所以答案是[ 3，1 ]。移除元素 2 的成本为 1。
> 所以，序列的和是 4。
> 成本为 1。
> **输入:** N = 4，arr[] = { 1，3，4，2}，costArray[] = {0，1，0，0}
> **输出:** 7，1

**朴素方法:**
朴素方法是简单地通过递归生成所有子序列来检查它们，这需要非常高复杂度的 O(2^N 复杂度。并从中选择符合上述条件的子序列，其绝对和最大，长度最小，如上所述。
T4【高效途径:

1.  我们可以观察模式，让我们假设三个数字 a，b，c，这样 a = L，b = L + 6，c = L + 10(这里 L 是任意整数)。如果它们是一个接一个的连续模式，例如 a，b，c(这样 a < b < c)。
2.  然后

> | b–a |+| c–b | = | a–c | = 10

1.  这里我们可以去掉中间的元素来减少原始序列的大小。
2.  这样，通过从序列中移除中间元素来减小数组的大小不会影响总和，并且还会减小序列的长度。
3.  存储集合中所有移除的元素。添加移除元素的成本。最后，通过排除移除的元素来计算总和序列。
4.  然后打印后续要素和发生成本的总和。

这样，我们将指数复杂度 O(2^N)降低到线性复杂度 O(N)。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

void costOfSubsequence(
    int N, int arr[],
    int costArray[])
{
    int i, temp;
    // initializing cost=0
    int cost = 0;

    // to store the removed
    // element
    set<int> removedElements;

    // this will store the sum
    // of the subsequence
    int ans = 0;

    // checking all the element
    // of the vector
    for (i = 1; i < (N - 1); i++) {
        // storing the value of
        // arr[i] in temp variable
        temp = arr[i];

        // if the situation like
        // arr[i-1]<arr[i]<arr[i+1] or
        // arr[i-1]>arr[i]>arr[i+1] occur
        // remove arr[i] i.e, temp
        // from sequence
        if (((arr[i - 1] < temp)
             && (temp < arr[i + 1]))
            || ((arr[i - 1] > temp)
                && (temp > arr[i + 1]))) {
            // insert the element in the set
            // removedElements
            removedElements.insert(temp);
        }
    }
    for (i = 0; i < (N); i++) {
        // storing the value of
        // arr[i] in temp
        temp = arr[i];
        // taking the element not
        // in removedElements
        if (!(removedElements.count(temp) > 0)) {
            // adding the value of elements
            // of subsequence
            ans += arr[i];
        }
        else {
            // if we have to remove
            // the element then we
            // need to add the  cost
            // associated with the
            // element
            cost += costArray[i];
        }
    }

    // printing the sum of
    // the subsequence with
    // minimum length possible
    cout << ans << ", ";
    // printing the cost incurred
    // in creating subsequence
    cout << cost << endl;
}

// Driver code
int main()
{

    int N;
    N = 4;
    int arr[N]
        = { 1, 3, 4, 2 };
    int costArray[N]
        = { 0, 1, 0, 0 };

    // calling the function
    costOfSubsequence(
        N, arr,
        costArray);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
class GFG{

public static void costOfSubsequence(int N, int[] arr,
                                     int[] costArray)
{
    int i, temp;

    // Initializing cost=0
    int cost = 0;

    // To store the removed
    // element
    Set<Integer> removedElements = new HashSet<Integer>();

    // This will store the sum
    // of the subsequence
    int ans = 0;

    // Checking all the element
    // of the vector
    for(i = 1; i < (N - 1); i++)
    {

       // Storing the value of
       // arr[i] in temp variable
       temp = arr[i];

       // If the situation like
       // arr[i-1]<arr[i]<arr[i+1] or
       // arr[i-1]>arr[i]>arr[i+1] occur
       // remove arr[i] i.e, temp
       // from sequence
       if (((arr[i - 1] < temp) &&
          (temp < arr[i + 1])) ||
           ((arr[i - 1] > temp) &&
          (temp > arr[i + 1])))
       {

           // Insert the element in the set
           // removedElements
           removedElements.add(temp);
       }
    }
    for(i = 0; i < (N); i++)
    {

       // Storing the value of
       // arr[i] in temp
       temp = arr[i];

       // Taking the element not
       // in removedElements
       if (!(removedElements.contains(temp)))
       {

           // Adding the value of elements
           // of subsequence
           ans += arr[i];
       }
       else
       {

           // If we have to remove
           // the element then we
           // need to add the cost
           // associated with the
           // element
           cost += costArray[i];
       }
    }

    // Printing the sum of
    // the subsequence with
    // minimum length possible
    System.out.print(ans + ", ");

    // Printing the cost incurred
    // in creating subsequence
    System.out.print(cost);
}

// Driver code
public static void main(String[] args)
{
    int N;
    N = 4;

    int[] arr = { 1, 3, 4, 2 };
    int[] costArray = { 0, 1, 0, 0 };

    // Calling the function
    costOfSubsequence(N, arr, costArray);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
def costOfSubsequence(N, arr, costArray):

    # Initializing cost=0
    i, temp, cost = 0, 0, 0

    # To store the removed
    # element
    removedElements = {''}

    # This will store the sum
    # of the subsequence
    ans = 0

    # Checking all the element
    # of the vector
    for i in range(1, N - 1):

        # Storing the value of
        # arr[i] in temp variable
        temp = arr[i]

        # If the situation like
        # arr[i-1]<arr[i]<arr[i+1] or
        # arr[i-1]>arr[i]>arr[i+1] occur
        # remove arr[i] i.e, temp
        # from sequence
        if (((arr[i - 1] < temp) and
            (temp < arr[i + 1])) or
            ((arr[i - 1] > temp) and
            (temp > arr[i + 1]))) :

            # Insert the element in the set
            # removedElements
            removedElements.add(temp)

    for i in range(0, N):

        # Storing the value of
        # arr[i] in temp
        temp = arr[i]

        # Taking the element not
        # in removedElements
        if(temp not in removedElements):

            # Adding the value of elements
            # of subsequence
            ans = ans + arr[i]
        else:

            # If we have to remove
            # the element then we
            # need to add the cost
            # associated with the
            # element
            cost += costArray[i]

    # Printing the sum of
    # the subsequence with
    # minimum length possible
    print(ans, end = ", ")

    # Printing the cost incurred
    # in creating subsequence
    print(cost)

# Driver code
N = 4
arr = [ 1, 3, 4, 2 ]
costArray = [ 0, 1, 0, 0 ]

# Calling the function
costOfSubsequence(N, arr, costArray)

# This code is contributed by Sanjit_Prasad
```

## C#

```
using System;
using System.Collections.Generic;

class GFG{

public static void costOfSubsequence(int N, int[] arr,
                                     int[] costArray)
{
    int i, temp;

    // Initializing cost=0
    int cost = 0;

    // To store the removed
    // element
    HashSet<int> removedElements = new HashSet<int>();

    // This will store the sum
    // of the subsequence
    int ans = 0;

    // Checking all the element
    // of the vector
    for(i = 1; i < (N - 1); i++)
    {

        // Storing the value of
        // arr[i] in temp variable
        temp = arr[i];

        // If the situation like
        // arr[i-1]<arr[i]<arr[i+1] or
        // arr[i-1]>arr[i]>arr[i+1] occur
        // remove arr[i] i.e, temp
        // from sequence
        if (((arr[i - 1] < temp) &&
            (temp < arr[i + 1])) ||
            ((arr[i - 1] > temp) &&
            (temp > arr[i + 1])))
        {

            // Insert the element in the set
            // removedElements
            removedElements.Add(temp);
        }
    }
    for(i = 0; i < (N); i++)
    {

        // Storing the value of
        // arr[i] in temp
        temp = arr[i];

        // Taking the element not
        // in removedElements
        if (!(removedElements.Contains(temp)))
        {

            // Adding the value of elements
            // of subsequence
            ans += arr[i];
        }
        else
        {

            // If we have to remove
            // the element then we
            // need to add the cost
            // associated with the
            // element
            cost += costArray[i];
        }
    }

    // Printing the sum of
    // the subsequence with
    // minimum length possible
    Console.Write(ans + ", ");

    // Printing the cost incurred
    // in creating subsequence
    Console.Write(cost);
}

// Driver code
public static void Main(String[] args)
{
    int N;
    N = 4;

    int[] arr = { 1, 3, 4, 2 };
    int[] costArray = { 0, 1, 0, 0 };

    // Calling the function
    costOfSubsequence(N, arr, costArray);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

    function costOfSubsequence(N,arr,costArray)
    {
        let i, temp;
        // initializing cost=0
        let cost = 0;

        // to store the removed
        // element
        let removedElements = new Set();

        // this will store the sum
        // of the subsequence
        let ans = 0;

        // checking all the element
        // of the vector
        for (i = 1; i < (N - 1); i++) {
            // storing the value of
            // arr[i] in temp variable
            temp = arr[i];

            // if the situation like
            // arr[i-1]<arr[i]<arr[i+1] or
            // arr[i-1]>arr[i]>arr[i+1] occur
            // remove arr[i] i.e, temp
            // from sequence
            if (((arr[i - 1] < temp)
                && (temp < arr[i + 1]))
                || ((arr[i - 1] > temp)
                    && (temp > arr[i + 1]))) {
                // insert the element in the set
                // removedElements
                removedElements.add(temp);
            }
        }
        for (i = 0; i < (N); i++) {
            // storing the value of
            // arr[i] in temp
            temp = arr[i];
            // taking the element not
            // in removedElements
            if (!removedElements.has(temp)) {
                // adding the value of elements
                // of subsequence
                ans += arr[i];
            }
            else {
                // if we have to remove
                // the element then we
                // need to add the cost
                // associated with the
                // element
                cost += costArray[i];
            }
        }

        // printing the sum of
        // the subsequence with
        // minimum length possible
        document.write(ans + ", ");
        // printing the cost incurred
        // in creating subsequence
        document.write(cost);
    }

    // Driver code

    let N;
    N = 4;
    let arr= [ 1, 3, 4, 2 ];
    let costArray= [ 0, 1, 0, 0 ];

    // calling the function
    costOfSubsequence(N, arr,costArray);

</script>
```

**Output:** 

```
7, 1
```

***时间复杂度:**O(N)*T4】