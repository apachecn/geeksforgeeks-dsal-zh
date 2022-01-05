# 将数组元素拆分成严格的递增和递减顺序

> 原文:[https://www . geeksforgeeks . org/将数组元素拆分为严格递增和递减的序列/](https://www.geeksforgeeks.org/split-the-array-elements-into-strictly-increasing-and-decreasing-sequence/)

给定一组 **N 个**元素。任务是将元素分成两个数组，比如 a1[]和 a2[]，一个包含**严格的** **递增的**元素，另一个包含**严格的递减的**元素和**a1 . size()+a2 . size()= a . size()**。如果不能这样做，打印 **-1** 或打印两个阵列。

**注**:可以有多个答案，子数组中元素的顺序不需要相同。

**示例:**

> **输入:** a[] = {7，2，7，3，3，1，4}
> **输出:** a1[] = {1，2，3，4，7}，a2[] = {7，3}
> 
> **输入:** a[] = {1，2，2，1，1}
> **输出:** -1
> 不可能

**接近**:按照以下步骤解决上述问题:

*   初始化存储递增和递减数字的两个向量 v1 和 v2。
*   使用散列法知道数组中数字的出现。
*   如果这个数字看起来是第一次出现，那么把它存储在 v1 中。
*   如果数字似乎是第二次出现，则将其存储在 v2 中。
*   如果数字出现超过 2 次，那么就不可能存储创建严格递增和严格递减的数组。
*   最后将第一个向量按递增顺序排序，第二个向量按递减顺序排序并打印出来。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print both the arrays
void PrintBothArrays(int a[], int n)
{

    // Store both arrays
    vector<int> v1, v2;

    // Used for hashing
    unordered_map<int, int> mpp;

    // Iterate for every element
    for (int i = 0; i < n; i++) {

        // Increase the count
        mpp[a[i]]++;

        // If first occurrence
        if (mpp[a[i]] == 1)
            v1.push_back(a[i]);

        // If second occurrence
        else if (mpp[a[i]] == 2)
            v2.push_back(a[i]);

        // If occurs more than 2 times
        else {
            cout << "Not possible";
            return;
        }
    }

    // Sort in increasing order
    sort(v1.begin(), v1.end());

    // Print the increasing array
    cout << "Strictly increasing array is:\n";
    for (auto it : v1)
        cout << it << " ";

    // Sort in reverse order
    sort(v2.begin(), v2.end(), greater<int>());

    // Print the decreasing array
    cout << "\nStrictly decreasing array is:\n";
    for (auto it : v2)
        cout << it << " ";
}

// Driver code
int main()
{

    int a[] = { 7, 2, 7, 3, 3, 1, 4 };
    int n = sizeof(a) / sizeof(a[0]);
    PrintBothArrays(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{

// Function to print both the arrays
static void PrintBothArrays(int a[], int n)
{

    // Store both arrays
    Vector<Integer> v1 = new Vector<Integer>(),
                    v2 = new Vector<Integer>();

    // Used for hashing
    HashMap<Integer, Integer> mpp = new HashMap<>();

    // Iterate for every element
    for (int i = 0; i < n; i++)
    {

        // Increase the count
        mpp.put(a[i],(mpp.get(a[i]) == null?0:mpp.get(a[i]))+1);

        // If first occurrence
        if (mpp.get(a[i]) == 1)
            v1.add(a[i]);

        // If second occurrence
        else if (mpp.get(a[i]) == 2)
            v2.add(a[i]);

        // If occurs more than 2 times
        else
        {
            System.out.println( "Not possible");
            return;
        }
    }

    // Sort in increasing order
    Collections.sort(v1);

    // Print the increasing array
    System.out.println("Strictly increasing array is:");
    for (int i = 0; i < v1.size(); i++)
        System.out.print(v1.get(i) + " ");

    // Sort
    Collections.sort(v2);
    Collections.reverse(v2);

    // Print the decreasing array
    System.out.println("\nStrictly decreasing array is:");
    for (int i = 0; i < v2.size(); i++)
        System.out.print(v2.get(i) + " ");
}

// Driver code
public static void main(String args[])
{
    int a[] = { 7, 2, 7, 3, 3, 1, 4 };
    int n = a.length;
    PrintBothArrays(a, n);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print both the arrays
def PrintBothArrays(a, n) :

    # Store both arrays
    v1, v2 = [], [];

    # Used for hashing
    mpp = dict.fromkeys(a, 0);

    # Iterate for every element
    for i in range(n) :

        # Increase the count
        mpp[a[i]] += 1;

        # If first occurrence
        if (mpp[a[i]] == 1) :
            v1.append(a[i]);

        # If second occurrence
        elif (mpp[a[i]] == 2) :
            v2.append(a[i]);

        # If occurs more than 2 times
        else :
            print("Not possible");
            return;

    # Sort in increasing order
    v1.sort();

    # Print the increasing array
    print("Strictly increasing array is:");
    for it in v1:
        print(it, end = " ");

    # Sort in reverse order
    v2.sort(reverse = True);

    # Print the decreasing array
    print("\nStrictly decreasing array is:");
    for it in v2 :
        print(it, end = " ")

# Driver code
if __name__ == "__main__" :

    a = [ 7, 2, 7, 3, 3, 1, 4 ];
    n = len(a);
    PrintBothArrays(a, n);

# This code is contributed by Ryuga
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

    // Function to print both the arrays
    static void PrintBothArrays(int [] a, int n)
    {

        // Store both arrays
        List<int> v1 = new List<int>();
        List<int> v2 = new List<int>();

        // Used for hashing
        Dictionary<int, int> mpp = new Dictionary<int, int>();

        // Iterate for every element
        for (int i = 0; i < n; i++)
        {

            // Increase the Count
            if(mpp.ContainsKey(a[i]))
                mpp[a[i]] = mpp[a[i]] + 1;
            else
                mpp[a[i]] = 1;

            // If first occurrence
            if (mpp[a[i]] == 1)
                v1.Add(a[i]);

            // If second occurrence
            else if (mpp[a[i]] == 2)
                v2.Add(a[i]);

            // If occurs more than 2 times
            else
            {
                Console.WriteLine( "Not possible");
                return;
            }
        }

        // Sort in increasing order
        v1.Sort();

        // Print the increasing array
        Console.WriteLine("Strictly increasing array is:");
        for (int i = 0; i < v1.Count; i++)
            Console.Write(v1[i] + " ");

        // Sort
        v2.Sort();
        v2.Reverse();

        // Print the decreasing array
        Console.WriteLine("\nStrictly decreasing array is:");
        for (int i = 0; i < v2.Count; i++)
            Console.Write(v2[i] + " ");
    }

    // Driver code
    public static void Main()
    {
        int [] a = { 7, 2, 7, 3, 3, 1, 4 };
        int n = a.Length;
        PrintBothArrays(a, n);
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

// Function to print both the arrays
function PrletBothArrays(a, n)
{

    // Store both arrays
    let v1 = [], v2 = [];

    // Used for hashing
    let mpp = new Map();

    // Iterate for every element
    for (let i = 0; i < n; i++)
    {

        // Increase the count
        mpp.set(a[i],(mpp.get(a[i]) == null?0:mpp.get(a[i]))+1);

        // If first occurrence
        if (mpp.get(a[i]) == 1)
            v1.push(a[i]);

        // If second occurrence
        else if (mpp.get(a[i]) == 2)
            v2.push(a[i]);

        // If occurs more than 2 times
        else
        {
            document.write( "Not possible");
            return;
        }
    }

    // Sort in increasing order
    v1.sort();

    // Print the increasing array
    document.write("Strictly increasing array is:" + "<br/>");
    for (let i = 0; i < v1.length; i++)
        document.write(v1[i] + " ");

    // Sort
    v2.sort();
    v2.reverse();

    // Print the decreasing array
    document.write("<br/>" + "\nStrictly decreasing array is:" + "<br/>");
    for (let i = 0; i < v2.length; i++)
        document.write(v2[i] + " ");
}

    // Driver code

     let a = [ 7, 2, 7, 3, 3, 1, 4 ];
    let n = a.length;
    PrletBothArrays(a, n);

 // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
Strictly increasing array is:
1 2 3 4 7 
Strictly decreasing array is:
7 3
```