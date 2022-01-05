# 求一个数的所有指数的递归程序

> 原文:[https://www . geesforgeks . org/递归程序查找数字的所有索引/](https://www.geeksforgeeks.org/recursive-program-to-find-all-indices-of-a-number/)

给定一个大小为 **N** 的数组**和一个整数 **X** 。任务是在数组
**中找到整数 **X** 的所有索引示例:**** 

> **输入:** arr = {1，2，3，2，2，5}，X = 2
> **输出:** 1 3 4
> 元素 2 出现在索引 1，3，4(基于 0 的索引)
> **输入:** arr[] = {7，7，7}，X = 7
> **输出:** 0 1 2

**迭代方法**很简单，只需遍历给定的数组，并继续将元素的索引存储在另一个数组中。
T3】递归方法:T5】

*   如果起始索引达到数组的长度，则返回空数组
*   否则，保留数组的第一个元素，并将数组的其余部分传递给递归。
    *   如果起始索引处的元素不等于 x，那么只需简单地返回来自递归的答案。

    *   否则，如果起始索引处的元素等于 x，则将数组的元素(这是递归的答案)向右移动一步，然后将起始索引放在数组的前面(通过递归得出)

以下是上述方法的实现:

## C++

```
// CPP program to find all indices of a number
#include <bits/stdc++.h>
using namespace std;

// A recursive function to find all
// indices of a number
int AllIndexesRecursive(int input[], int size,
                    int x, int output[])
{

    // If an empty array comes
    // to the function, then
    // return zero
    if (size == 0) {
        return 0;
    }

    // Getting the recursive answer
    int smallAns = AllIndexesRecursive(input + 1,
                                    size - 1, x, output);

    // If the element at index 0 is equal
    // to x then add 1 to the array values
    // and shift them right by 1 step
    if (input[0] == x) {
        for (int i = smallAns - 1; i >= 0; i--) {
            output[i + 1] = output[i] + 1;
        }

        // Put the start index in front
        // of the array
        output[0] = 0;
        smallAns++;
    }
    else {

        // If the element at index 0 is not equal
        // to x then add 1 to the array values
        for (int i = smallAns - 1; i >= 0; i--) {
            output[i] = output[i] + 1;
        }
    }
    return smallAns;
}

// Function to find all indices of a number
void AllIndexes(int input[], int n, int x)
{
    int output[n];
    int size = AllIndexesRecursive(input, n,
                                x, output);
    for (int i = 0; i < size; i++) {
        cout << output[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 2, 2, 5 }, x = 2;

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    AllIndexes(arr, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all
// indices of a number
public class GFG {

    public int[] AllIndexesRecursive(int input[],
                                int x, int start)
    {
        // If the start index reaches the
        // length of the array, then
        // return empty array
        if (start == input.length) {
            int[] ans = new int[0]; // empty array
            return ans;
        }

        // Getting the recursive answer in
        // smallIndex array
        int[] smallIndex = AllIndexesRecursive(input, x,
                                              start + 1);

        // If the element at start index is equal
        // to x then
        // (which is the answer of recursion) and then
        // (which came through recursion)
        if (input[start] == x) {
            int[] myAns = new int[smallIndex.length + 1];

            // Put the start index in front
            // of the array
            myAns[0] = start;
            for (int i = 0; i < smallIndex.length; i++) {

                // Shift the elements of the array
                // one step to the right
                // and putting them in
                // myAns array
                myAns[i + 1] = smallIndex[i];
            }
            return myAns;
        }
        else {

            // If the element at start index is not
            // equal to x then just simply return the
            // answer which came from recursion.
            return smallIndex;
        }
    }

    public int[] AllIndexes(int input[], int x)
    {

        return AllIndexesRecursive(input, x, 0);
    }

    // Driver Code
    public static void main(String args[])
    {
        GFG g = new GFG();
        int arr[] = { 1, 2, 3, 2, 2, 5 }, x = 2;

        int output[] = g.AllIndexes(arr, x);

        // Printing the output array
        for (int i = 0; i < output.length; i++) {
            System.out.print(output[i] + " ");
        }
    }
}
```

## 蟒蛇 3

```
# Python3 program to find all
# indices of a number
def AllIndexesRecursive(input, x, start):

    # If the start index reaches the
    # length of the array, then
    # return empty array
    if (start == len(input)):
        ans = [] # empty array
        return ans

    # Getting the recursive answer in
    # smallIndex array
    smallIndex = AllIndexesRecursive(input, x,
                                     start + 1)

    # If the element at start index is equal
    # to x then
    # (which is the answer of recursion) and then
    # (which came through recursion)
    if (input[start] == x):
        myAns = [0 for i in range(len(smallIndex) + 1)]

        # Put the start index in front
        # of the array
        myAns[0] = start
        for i in range(len(smallIndex)):

            # Shift the elements of the array
            # one step to the right
            # and putting them in
            # myAns array
            myAns[i + 1] = smallIndex[i]

        return myAns
    else:

        # If the element at start index is not
        # equal to x then just simply return the
        # answer which came from recursion.
        return smallIndex

# Function to find all indices of a number
def AllIndexes(input, x):

    return AllIndexesRecursive(input, x, 0)

# Driver Code
arr = [ 1, 2, 3, 2, 2, 5 ]
x = 2

output=AllIndexes(arr, x)

# Printing the output array
for i in output:
    print(i, end = " ")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find all
// indices of a number
using System;
class GFG
{
    public int[] AllIndexesRecursive(int []input,
                                        int x, int start)
    {
        // If the start index reaches the
        // length of the array, then
        // return empty array
        if (start == input.Length)
        {
            int[] ans = new int[0]; // empty array
            return ans;
        }

        // Getting the recursive answer in
        // smallIndex array
        int[] smallIndex = AllIndexesRecursive(input, x,
                                               start + 1);

        // If the element at start index is equal
        // to x then
        // (which is the answer of recursion) and
        // then (which came through recursion)
        if (input[start] == x)
        {
            int[] myAns = new int[smallIndex.Length + 1];

            // Put the start index in front
            // of the array
            myAns[0] = start;
            for (int i = 0; i < smallIndex.Length; i++)
            {

                // Shift the elements of the array
                // one step to the right
                // and putting them in
                // myAns array
                myAns[i + 1] = smallIndex[i];
            }
            return myAns;
        }
        else
        {

            // If the element at start index is not
            // equal to x then just simply return the
            // answer which came from recursion.
            return smallIndex;
        }
    }

    public int[] AllIndexes(int []input, int x)
    {
        return AllIndexesRecursive(input, x, 0);
    }

    // Driver Code
    public static void Main()
    {
        GFG g = new GFG();
        int []arr = { 1, 2, 3, 2, 2, 5 };
        int x = 2;

        int []output = g.AllIndexes(arr, x);

        // Printing the output array
        for (int i = 0; i < output.Length; i++)
        {
            Console.Write(output[i] + " ");
        }
    }
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
    // Javascript program to find all indices of a number

    function AllIndexesRecursive(input, x, start)
    {
        // If the start index reaches the
        // length of the array, then
        // return empty array
        if (start == input.length)
        {
            let ans = new Array(0); // empty array
            return ans;
        }

        // Getting the recursive answer in
        // smallIndex array
        let smallIndex = AllIndexesRecursive(input, x, start + 1);

        // If the element at start index is equal
        // to x then
        // (which is the answer of recursion) and
        // then (which came through recursion)
        if (input[start] == x)
        {
            let myAns = new Array(smallIndex.length + 1);

            // Put the start index in front
            // of the array
            myAns[0] = start;
            for (let i = 0; i < smallIndex.length; i++)
            {

                // Shift the elements of the array
                // one step to the right
                // and putting them in
                // myAns array
                myAns[i + 1] = smallIndex[i];
            }
            return myAns;
        }
        else
        {

            // If the element at start index is not
            // equal to x then just simply return the
            // answer which came from recursion.
            return smallIndex;
        }
    }

    function AllIndexes(input, x)
    {
        return AllIndexesRecursive(input, x, 0);
    }

    let arr = [ 1, 2, 3, 2, 2, 5 ];
    let x = 2;

    let output = AllIndexes(arr, x);

    // Printing the output array
    for(let i = 0; i < output.length; i++)
    {
      document.write(output[i] + " ");
    }

    // This code is contributed by mukesh07.
</script>
```

**Output**

```
1 3 4 
```

**更简单的递归方法:(从末尾遍历)**

*   如果最后一个索引达到数组的长度，则返回空数组
*   否则，减少最后一个索引，并将整个数组传递给递归。
*   如果最后一个索引处的元素不等于 x，那么只需简单地返回来自递归的答案。
*   否则，如果最后一个索引处的元素等于 x，那么只需将最后一个索引处的最后一个元素插入 ans 指向的索引中。

这避免了将所有元素移动一个索引以及增加输出数组中所有元素的复杂性。

下面是上述方法的实现:

## C++

```
// CPP program to find all indices of a number
#include <bits/stdc++.h>
using namespace std;

// A recursive function to find all
// indices of a number
int AllIndexesRecursive(int input[], int size,
                    int x, int output[])
{

    // If the input array becomes empty
      if(size == 0)
        return 0;

    // Getting the recursive answer
      int smallAns = AllIndexesRecursive(input, size - 1, x, output);

      // If the last element of input array is equal to x
    if(input[size - 1] == x)
    {
      // Insert the index of last element of the input array into the output array
      // And increment ans
      output[smallAns++] = size - 1;
    }
    return smallAns;
}

// Function to find all indices of a number
void AllIndexes(int input[], int n, int x)
{
    int output[n];
    int size = AllIndexesRecursive(input, n,
                                x, output);
    for (int i = 0; i < size; i++) {
        cout << output[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 2, 2, 5 }, x = 2;

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    AllIndexes(arr, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all indices of a number
public class Main
{
    // A recursive function to find all
    // indices of a number
    static int AllIndexesRecursive(int[] input, int size, int x, int[] output)
    {

        // If the input array becomes empty
          if(size == 0)
            return 0;

        // Getting the recursive answer
        int smallAns = AllIndexesRecursive(input, size - 1, x, output);

          // If the last element of input array is equal to x
        if(input[size - 1] == x)
        {
          // Insert the index of last element of the input array into the output array
          // And increment ans
          output[smallAns++] = size - 1;
        }
        return smallAns;
    }

    // Function to find all indices of a number
    static void AllIndexes(int[] input, int n, int x)
    {
        int[] output = new int[n];
        int size = AllIndexesRecursive(input, n, x, output);
        for (int i = 0; i < size; i++) {
            System.out.print(output[i] + " ");
        }
    }

    public static void main(String[] args) {
        int[] arr = { 1, 2, 3, 2, 2, 5 };
        int x = 2;

        int n = arr.length;

        // Function call
        AllIndexes(arr, n, x);
    }
}

// This code is contributed by suresh07.
```

## 蟒蛇 3

```
# Python3 program to find all indices of a number

# A recursive function to find all
# indices of a number
def AllIndexesRecursive(Input, size, x, output):
    # If the input array becomes empty
    if size == 0:
        return 0

    # Getting the recursive answer
    smallAns = AllIndexesRecursive(Input, size - 1, x, output)

    # If the last element of input array is equal to x
    if Input[size - 1] == x:

      # Insert the index of last element of the input array into the output array
      # And increment ans
      output[smallAns] = size - 1
      smallAns+=1
    return smallAns

# Function to find all indices of a number
def AllIndexes(Input, n, x):
    output = [0]*n
    size = AllIndexesRecursive(Input, n, x, output)
    for i in range(size):
        print(output[i], "", end = "")

arr = [ 1, 2, 3, 2, 2, 5 ]
x = 2

n = len(arr)

# Function call
AllIndexes(arr, n, x)

# This code is contributed by rameshtravel07
```

## C#

```
// C# program to find all indices of a number
using System;
using System.Collections.Generic;
class GFG {

    // A recursive function to find all
    // indices of a number
    static int AllIndexesRecursive(int[] input, int size, int x, int[] output)
    {

        // If the input array becomes empty
          if(size == 0)
            return 0;

        // Getting the recursive answer
        int smallAns = AllIndexesRecursive(input, size - 1, x, output);

          // If the last element of input array is equal to x
        if(input[size - 1] == x)
        {
          // Insert the index of last element of the input array into the output array
          // And increment ans
          output[smallAns++] = size - 1;
        }
        return smallAns;
    }

    // Function to find all indices of a number
    static void AllIndexes(int[] input, int n, int x)
    {
        int[] output = new int[n];
        int size = AllIndexesRecursive(input, n, x, output);
        for (int i = 0; i < size; i++) {
            Console.Write(output[i] + " ");
        }
    }

  static void Main() {
    int[] arr = { 1, 2, 3, 2, 2, 5 };
    int x = 2;

    int n = arr.Length;

    // Function call
    AllIndexes(arr, n, x);
  }
}

// This code is contributed by decode22007.
```

## java 描述语言

```
<script>
    // Javascript program to find all indices of a number

    // A recursive function to find all
    // indices of a number
    function AllIndexesRecursive(input, size, x, output)
    {

        // If the input array becomes empty
          if(size == 0)
            return 0;

        // Getting the recursive answer
        let smallAns = AllIndexesRecursive(input, size - 1, x, output);

          // If the last element of input array is equal to x
        if(input[size - 1] == x)
        {
          // Insert the index of last element of the input array into the output array
          // And increment ans
          output[smallAns++] = size - 1;
        }
        return smallAns;
    }

    // Function to find all indices of a number
    function AllIndexes(input, n, x)
    {
        let output = new Array(n);
        let size = AllIndexesRecursive(input, n, x, output);
        for (let i = 0; i < size; i++) {
            document.write(output[i] + " ");
        }
    }

    let arr = [ 1, 2, 3, 2, 2, 5 ];
    let x = 2;

    let n = arr.length;

    // Function call
    AllIndexes(arr, n, x);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output**

```
1 3 4 
```