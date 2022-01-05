# 找出排序数组中每个元素的频率

> 原文:[https://www . geeksforgeeks . org/find-排序数组中每个元素的频率/](https://www.geeksforgeeks.org/find-the-frequency-of-each-element-in-a-sorted-array/)

给定一个由 **N** 个整数组成的排序的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，任务是找到[每个数组元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)[的](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)频率。

**示例:**

> **输入:** arr[] = {1，1，1，2，3，3，5，5，8，8，8，9，9，10}
> **输出:**频率 1 为:3
> 频率 2 为:1
> 频率 3 为:2
> 频率 5 为:2
> 频率 8 为:3
> 频率 9 为:2
> 频率 10 为:1
> 
> **输入:** arr[] = {2，2，6，6，7，7，11}
> **输出:**2 的频率为:2
> 6 的频率为:2
> 7 的频率为:3
> 11 的频率为:1

**天真法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并保留在 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 中遇到的每个元素的计数，最后通过[遍历 HashMap 打印每个元素的频率。](https://www.geeksforgeeks.org/traverse-through-a-hashmap-in-java/)这个办法已经在[这里](https://www.geeksforgeeks.org/find-frequency-of-each-element-in-a-limited-range-array-in-less-than-on-time/)实行了。

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**高效方法:**上述方法可以根据使用的空间进行优化，这是基于这样一个事实，即在排序的数组中，相同的元素连续出现，因此想法是在遍历数组时维护一个变量来跟踪元素的频率。按照以下步骤解决问题:

*   初始化一个变量，说 **freq** 为 **1** 存储元素的频率。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N-1】**中迭代，并执行以下步骤:
    *   如果 **arr[i]** 的值等于 **arr[i-1]** ，则将 **freq** 增加 **1** 。
    *   否则打印在**频率**中获得的**arr【I-1】**的频率值，然后将**频率**更新为 **1** 。
*   最后，在上述步骤之后，将数组最后一个不同元素的频率打印为 **freq** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

    // Function to print the frequency
    // of each element of the sorted array
     void printFreq(vector<int> &arr, int N)
    {

        // Stores the frequency of an element
        int freq = 1;

       // Traverse the array arr[]
        for (int i = 1; i < N; i++)
        {

            // If the current element is equal
            // to the previous element
            if (arr[i] == arr[i - 1])
            {

                // Increment the freq by 1
                freq++;
            }

        // Otherwise,
            else {
                cout<<"Frequency of "<<arr[i - 1]<< " is: " << freq<<endl;
                // Update freq
                freq = 1;
            }
        }

        // Print the frequency of the last element
       cout<<"Frequency of "<<arr[N - 1]<< " is: " << freq<<endl;
       }

    // Driver Code
    int main()
    {

        // Given Input
        vector<int> arr
            = { 1, 1, 1, 2, 3, 3, 5, 5,
                8, 8, 8, 9, 9, 10 };
        int N = arr.size();

        // Function Call
        printFreq(arr, N);
    return 0;
    }   

// This code is contributed by codersaty
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

    // Function to print the frequency
    // of each element of the sorted array
    static void printFreq(int arr[], int N)
    {

        // Stores the frequency of an element
        int freq = 1;

        // Traverse the array arr[]
        for (int i = 1; i < N; i++) {
            // If the current element is equal
            // to the previous element
            if (arr[i] == arr[i - 1]) {
                // Increment the freq by 1
                freq++;
            }

            // Otherwise,
            else {
                System.out.println("Frequency of "
                                   + arr[i - 1]
                                   + " is: " + freq);
                // Update freq
                freq = 1;
            }
        }

        // Print the frequency of the last element
        System.out.println("Frequency of "
                           + arr[N - 1]
                           + " is: " + freq);
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given Input
        int arr[]
            = { 1, 1, 1, 2, 3, 3, 5, 5,
                8, 8, 8, 9, 9, 10 };
        int N = arr.length;

        // Function Call
        printFreq(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the frequency
# of each element of the sorted array
def printFreq(arr, N):

    # Stores the frequency of an element
    freq = 1

    # Traverse the array arr[]
    for i in range(1, N, 1):

        # If the current element is equal
        # to the previous element
        if (arr[i] == arr[i - 1]):

            # Increment the freq by 1
            freq += 1

        # Otherwise,
        else:
            print("Frequency of",arr[i - 1],"is:",freq)
                # Update freq
            freq = 1

    # Print the frequency of the last element
    print("Frequency of",arr[N - 1],"is:",freq)

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [1, 1, 1, 2, 3, 3, 5, 5,8, 8, 8, 9, 9, 10]
    N = len(arr)

    # Function Call
    printFreq(arr, N)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

// Function to print the frequency
// of each element of the sorted array
static void printFreq(int[] arr, int N)
{

    // Stores the frequency of an element
    int freq = 1;

    // Traverse the array arr[]
    for (int i = 1; i < N; i++)
    {

      // If the current element is equal
      // to the previous element
      if (arr[i] == arr[i - 1])
      {

        // Increment the freq by 1
        freq++;
      }

      // Otherwise,
      else {
        Console.WriteLine("Frequency of " + arr[i - 1] + " is: " + freq);
        // Update freq
        freq = 1;
      }
    }

    // Print the frequency of the last element
    Console.WriteLine("Frequency of " + arr[N - 1] + " is: " + freq);
}

// Driver Code
static public void Main (){

    // Given Input
    int[] arr = { 1, 1, 1, 2, 3, 3, 5, 5,
                  8, 8, 8, 9, 9, 10 };
    int N = arr.Length;

    // Function Call
    printFreq(arr, N);
}
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print the frequency
// of each element of the sorted array
function printFreq(arr, N)
{

    // Stores the frequency of an element
    let freq = 1;

    // Traverse the array arr[]
    for(let i = 1; i < N; i++)
    {

        // If the current element is equal
        // to the previous element
        if (arr[i] == arr[i - 1])
        {

            // Increment the freq by 1
            freq++;
        }

        // Otherwise,
        else
        {
            document.write("Frequency of " +
                           parseInt(arr[i - 1]) + " is: " +
                           parseInt(freq) + "<br>");

            // Update freq
            freq = 1;
        }
    }

    // Print the frequency of the last element
    document.write("Frequency of " +
                   parseInt(arr[N - 1]) + " is: " +
                   parseInt(freq) + "<br>");
}

// Driver Code

// Given Input
let arr = [ 1, 1, 1, 2, 3, 3, 5, 5,
            8, 8, 8, 9, 9, 10 ];
let N = arr.length;

// Function Call
printFreq(arr, N);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
Frequency of 1 is: 3
Frequency of 2 is: 1
Frequency of 3 is: 2
Frequency of 5 is: 2
Frequency of 8 is: 3
Frequency of 9 is: 2
Frequency of 10 is: 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)