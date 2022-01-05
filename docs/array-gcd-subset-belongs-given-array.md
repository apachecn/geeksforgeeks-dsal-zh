# 任何子集 GCD 的数组都属于给定数组

> 原文:[https://www . geesforgeks . org/array-gcd-subset-attributes-给定-array/](https://www.geeksforgeeks.org/array-gcd-subset-belongs-given-array/)

给定一组 N 个元素，使得 N ![\in [1, 1000]  ](img/8dfbb9117ecc2d9bd2fbae3a42670f28.png "Rendered by QuickLaTeX.com")，任务是生成一个数组，使得生成的数组的任何子集的 GCD 位于给定的元素组中。生成的数组**不应超过 GCD** 集合长度的三倍。
**先决条件:** [阵列的 GCD](https://www.geeksforgeeks.org/gcd-two-array-numbers/)|[阵列的子集](https://www.geeksforgeeks.org/finding-all-subsets-of-a-given-set-in-java/)
**示例:**

```
Input : 3
        1 2 7
Output :  1 1 2 1 7

Input : 4
        2 4 6 12
Output : 2 2 4 2 6 2 12

Input : 5
        2 5 6 7 11
Output : No array can be build
```

**说明:**
计算一个数组的 [GCD，或者在本例中是一个集合。现在，首先对给定的 GCD 集合进行排序。如果这个集合的 GCD 等于给定集合的最小数，那么只需将这个 GCD 放在每个数之间。但是，如果这个 GCD 不是给定集合的最小元素，那么不幸的是“不能构建数组”。](https://www.geeksforgeeks.org/gcd-two-array-numbers/) 

## C++

```
// C++ implementation to generate the
// required array
#include <bits/stdc++.h>
using namespace std;

// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
       return b;      
    return gcd(b % a, a);
}

// Function to find gcd of
// array of numbers
int findGCD(vector<int> arr, int n)
{
    int result = arr[0];   
    for (int i = 1; i < n; i++)
        result = gcd(arr[i], result);
    return result;
}

// Function to generate the array
// with required constraints.
void compute(vector<int> arr, int n)
{
    vector<int> answer;

    // computing GCD of the given set
    int GCD_of_array = findGCD(arr, n);

    // Solution exists if GCD of array is equal
    // to the minimum element of the array
    if(GCD_of_array == arr[0])
    {
        answer.push_back(arr[0]);
        for(int i = 1; i < n; i++)
        {
            answer.push_back(arr[0]);
            answer.push_back(arr[i]);
        }

        // Printing the built array
        for (int i = 0; i < answer.size(); i++)
            cout << answer[i] << " ";
    }
    else
        cout << "No array can be build";
}

// Driver function
int main()
{

    // Taking in the input and initializing
    // the set STL set in cpp has a property
    // that it maintains the elements in
    // sorted order, thus we do not need
    // to sort them externally
    int n = 3;
    int input[]= {2, 5, 6, 7, 11};
    set<int> GCD(input, input + n);
    vector<int> arr;
    set<int>::iterator it;

    for(it = GCD.begin(); it!= GCD.end(); ++it)
        arr.push_back(*it);

    // Calling the computing function.
    compute(arr,n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// to generate the
// required array
import java.io.*;
import java.util.*;

class GFG
{
// Function to return
// gcd of a and b
static int gcd(int a,
               int b)
{
    if (a == 0)
    return b;    
    return gcd(b % a, a);
}

// Function to find gcd
// of array of numbers
public static int findGCD(ArrayList<Integer>
                                 arr, int n)
{
    int result = arr.get(0);
    for (int i = 1; i < n; i++)
        result = gcd(arr.get(i),
                    result);
    return result;
}

// Function to generate
// the array with required
// constraints.
public static void compute(ArrayList<Integer>
                                  arr, int n)
{
    ArrayList<Integer> answer =
                    new ArrayList<Integer>();

    // computing GCD of
    // the given set
    int GCD_of_array = findGCD(arr, n);

    // Solution exists if GCD
    // of array is equal to the
    // minimum element of the array
    if(GCD_of_array == arr.get(0))
    {
        answer.add(arr.get(0));
        for(int i = 1; i < n; i++)
        {
            answer.add(arr.get(0));
            answer.add(arr.get(i));
        }

        // Printing the
        // built array
        for (int i = 0;
                 i < answer.size(); i++)
            System.out.print(answer.get(i) + " ");
    }
    else
        System.out.print("No array " +
                      "can be build");
}

// Driver Code
public static void main(String args[])
{

    // Taking in the input and
    // initializing the set STL
    // set in cpp has a property
    // that it maintains the
    // elements in sorted order,
    // thus we do not need to
    // sort them externally
    int n = 3;
    Integer input[]= {2, 5, 6, 7, 11};
    HashSet<Integer> GCD = new HashSet<Integer>
                        (Arrays.asList(input));
    ArrayList<Integer> arr =
                new ArrayList<Integer>();

    for (int v : GCD)
        arr.add(v);

    // Calling the
    // computing function.
    compute(arr, n);
}
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
from math import gcd
# Python 3 implementation to generate the
# required array

# Function to find gcd of
# array of numbers
def findGCD(arr, n):
    result = arr[0]
    for i in range(1,n):
        result = gcd(arr[i], result)
    return result

# Function to generate the array
# with required constraints.
def compute(arr, n):
    answer = []

    # computing GCD of the given set
    GCD_of_array = findGCD(arr, n)

    # Solution exists if GCD of array is equal
    # to the minimum element of the array
    if(GCD_of_array == arr[0]):
        answer.append(arr[0])
        for i in range(1,n):
            answer.append(arr[0])
            answer.append(arr[i])

        # Printing the built array
        for i in range(len(answer)):
            print(answer[i],end = " ")

    else:
        print("No array can be build")

# Driver function
if __name__ == '__main__':
    # Taking in the input and initializing
    # the set STL set in cpp has a property
    # that it maintains the elements in
    # sorted order, thus we do not need
    # to sort them externally
    n = 3
    input = [2, 5, 6, 7, 11]
    GCD = set()
    for i in range(len(input)):
        GCD.add(input[i])

    arr = []

    for i in GCD:
        arr.append(i)

    # Calling the computing function.
    compute(arr,n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation
// to generate the
// required array
using System;
using System.Collections.Generic;

class GFG
{
    // Function to return
    // gcd of a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
        return b;    
        return gcd(b % a, a);
    }

    // Function to find gcd
    // of array of numbers
    static int findGCD(List<int> arr,
                               int n)
    {
        int result = arr[0];
        for (int i = 1; i < n; i++)
            result = gcd(arr[i],
                         result);
        return result;
    }

    // Function to generate
    // the array with required
    // constraints.
    static void compute(List<int> arr,
                                int n)
    {
        List<int> answer = new List<int>();

        // computing GCD of
        // the given set
        int GCD_of_array = findGCD(arr, n);

        // Solution exists if GCD
        // of array is equal to the
        // minimum element of the array
        if(GCD_of_array == arr[0])
        {
            answer.Add(arr[0]);
            for(int i = 1; i < n; i++)
            {
                answer.Add(arr[0]);
                answer.Add(arr[i]);
            }

            // Printing the
            // built array
            for (int i = 0; i < answer.Count; i++)
                Console.Write(answer[i] + " ");
        }
        else
            Console.Write("No array " +
                          "can be build");
    }

    // Driver Code
    static void Main()
    {

        // Taking in the input and
        // initializing the set STL
        // set in cpp has a property
        // that it maintains the
        // elements in sorted order,
        // thus we do not need to
        // sort them externally
        int n = 3;
        int []input= new int[]{2, 5, 6, 7, 11};
        HashSet<int> GCD = new HashSet<int>(input);
        List<int> arr = new List<int>();

        foreach (int b in GCD)
            arr.Add(b);

        // Calling the
        // computing function.
        compute(arr, n);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## java 描述语言

```
<script>
// javascript implementation
// to generate the
// required array

    // Function to return
    // gcd of a and b
    function gcd(a , b) {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to find gcd
    // of array of numbers
    function findGCD( arr , n) {
        var result = arr[0];
        for (i = 1; i < n; i++)
            result = gcd(arr[i], result);
        return result;
    }

    // Function to generate
    // the array with required
    // constraints.
    function compute(arr , n) {
        var answer = new Array();

        // computing GCD of
        // the given set
        var GCD_of_array = findGCD(arr, n);

        // Solution exists if GCD
        // of array is equal to the
        // minimum element of the array
        if (GCD_of_array == arr[0]) {
            answer.add(arr[0]);
            for (i = 1; i < n; i++) {
                answer.add(arr[0]);
                answer.add(arr[i]);
            }

            // Printing the
            // built array
            for (var i = 0; i < answer.length; i++)
                document.write(answer[i] + " ");
        } else
            document.write("No array " + "can be build");
    }

    // Driver Code

        // Taking in the input and
        // initializing the set STL
        // set in cpp has a property
        // that it maintains the
        // elements in sorted order,
        // thus we do not need to
        // sort them externally
        var n = 3;
        var input = [ 2, 5, 6, 7, 11 ];

        // Calling the
        // computing function.
        compute(input, n);

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
No array can be build
```

**时间复杂度:** O(nlog(n))，其中 n 是给定数组的大小。