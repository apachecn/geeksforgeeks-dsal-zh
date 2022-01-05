# 在重复元素/唯一数字 2 的数组中找到两个非重复元素

> 原文:[https://www . geeksforgeeks . org/find-两个非重复元素数组中的重复元素/](https://www.geeksforgeeks.org/find-two-non-repeating-elements-in-an-array-of-repeating-elements/)

SG 询问
给定一个数组，其中除了两个数字之外的所有数字都重复一次。(即我们有 2n+2 个数字，n 个数字出现了两次，剩下的两个出现了一次)。用最有效的方法找到这两个数字。

**方法 1(使用排序)**
首先，对所有元素进行排序。在排序的数组中，通过比较相邻的元素，我们可以很容易地得到不重复的元素。该方法的时间复杂度为 0(nLogn)

**方法 2(使用异或)**
让 x 和 y 成为我们要寻找的非重复元素，arr[]成为输入数组。首先，计算所有数组元素的异或。

```
     xor = arr[0]^arr[1]^arr[2].....arr[n-1]
```

xor 中设置的所有位将被设置在一个非重复元素(x 或 y)中，而不是其他元素中。因此，如果我们取 xor 的任意一组位，将数组的元素分成两组——一组元素具有相同的位集，另一组元素具有未设置的位集。这样，我们将在一个集合中得到 x，在另一个集合中得到 y。现在，如果我们对第一个集合中的所有元素进行异或运算，我们将获得第一个非重复元素，通过在其他集合中进行相同的运算，我们将获得第二个非重复元素。

```
Let us see an example.
   arr[] = {2, 4, 7, 9, 2, 4}
1) Get the XOR of all the elements.
     xor = 2^4^7^9^2^4 = 14 (1110)
2) Get a number which has only one set bit of the xor.   
   Since we can easily get the rightmost set bit, let us use it.
     set_bit_no = xor & ~(xor-1) = (1110) & ~(1101) = 0010
   Now set_bit_no will have only set as rightmost set bit of xor.
3) Now divide the elements in two sets and do xor of         
   elements in each set and we get the non-repeating 
   elements 7 and 9\. Please see the implementation for this step.
```

**方法:**
**步骤 1:** 将数组中的所有元素异或为一个变量和，这样数组中出现两次的所有元素都将被移除，例如，4 =“100”，如果 4 异或 4 =>“100”异或“100”，则答案为“000”。
**步骤 2:** 因此，在和中，最终答案将是 3 异或 5，因为 2 和 4 都与自身异或，给出 0，因此 sum =“011”异或“101”，即 sum =“110”= 6。
**第三步:**现在我们取和的 2 的补码，即(-sum)=“010”。
**第四步:**现在将和的 2 与和进行按位 And 运算，即“110”&“010”给出答案“010”(按位&的目的是我们想要得到一个只包含和的最右边集合位的数字)。
**第五步:**按位&将数组的所有元素与这个得到的和相加，2 =“010”&“010”= 2，3 =“011”&“010”=“010”，4 =“100”&“010”=“000”，5 =“101”&“010”=“000”。
**步骤 6:** 我们可以看到，2，3 的按位&为 0，因此它们将与 sum1 异或，4，5 的按位&为 0，因此它们将与 sum2 异或。
**步骤 7:** 由于 2 出现两次，因此与 sum1 进行两次异或运算时，只有结果 3 存储在其中，而 As 4 也出现两次，因此与 sum2 进行异或运算将取消其值，因此只有 5 保留在其中。

**实施:**

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

/* This function sets the values of
*x and *y to non-repeating elements
in an array arr[] of size n*/
void get2NonRepeatingNos(int arr[], int n, int* x, int* y)
{
    /* Will hold Xor of all elements */
    int Xor = arr[0];

    /* Will have only single set bit of Xor */
    int set_bit_no;
    int i;
    *x = 0;
    *y = 0;

    /* Get the Xor of all elements */
    for (i = 1; i < n; i++)
        Xor ^= arr[i];

    /* Get the rightmost set bit in set_bit_no */
    set_bit_no = Xor & ~(Xor - 1);

    /* Now divide elements in two sets by
    comparing rightmost set bit of Xor with bit
    at same position in each element. */
    for (i = 0; i < n; i++) {

        /*Xor of first set */
        if (arr[i] & set_bit_no)
            *x = *x ^ arr[i];
        /*Xor of second set*/
        else {
            *y = *y ^ arr[i];
        }
    }
}

/* Driver code */
int main()
{
    int arr[] = { 2, 3, 7, 9, 11, 2, 3, 11 };
    int n = sizeof(arr) / sizeof(*arr);
    int* x = new int[(sizeof(int))];
    int* y = new int[(sizeof(int))];
    get2NonRepeatingNos(arr, n, x, y);
    cout << "The non-repeating elements are " << *x
         << " and " << *y;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program for above approach
#include <stdio.h>
#include <stdlib.h>

/* This function sets the values of
*x and *y to non-repeating elements
in an array arr[] of size n*/
void get2NonRepeatingNos(int arr[], int n, int* x, int* y)
{
    /* Will hold Xor of all elements */
    int Xor = arr[0];

    /* Will have only single set bit of Xor */
    int set_bit_no;
    int i;
    *x = 0;
    *y = 0;

    /* Get the Xor of all elements */
    for (i = 1; i < n; i++)
        Xor ^= arr[i];

    /* Get the rightmost set bit in set_bit_no */
    set_bit_no = Xor & ~(Xor - 1);

    /* Now divide elements in two sets by
    comparing rightmost set bit of Xor with bit
    at same position in each element. */
    for (i = 0; i < n; i++) {

        /*Xor of first set */
        if (arr[i] & set_bit_no)
            *x = *x ^ arr[i];
        /*Xor of second set*/
        else {
            *y = *y ^ arr[i];
        }
    }
}

/* Driver program to test above function */
int main()
{
    int arr[] = { 2, 3, 7, 9, 11, 2, 3, 11 };
    int* x = (int*)malloc(sizeof(int));
    int* y = (int*)malloc(sizeof(int));
    get2NonRepeatingNos(arr, 8, x, y);
    printf("The non-repeating elements are %d and %d", *x,
           *y);
    getchar();
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach

public class UniqueNumbers {

    // This function sets the values of
    // *x and *y to non-repeating elements
    // in an array arr[] of size n
    public static void UniqueNumbers2(int[] arr, int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++) {

            // Xor  all the elements of the array
            // all the elements occurring twice will
            // cancel out each other remaining
            // two unique numbers will be xored
            sum = (sum ^ arr[i]);
        }

        // Bitwise & the sum with it's 2's Complement
        // Bitwise & will give us the sum containing
        // only the rightmost set bit
        sum = (sum & -sum);

        // sum1 and sum2 will contains 2 unique
        // elements elements initialized with 0 box
        // number xored with 0 is number itself
        int sum1 = 0;
        int sum2 = 0;

        // traversing the array again
        for (int i = 0; i < arr.length; i++) {

            // Bitwise & the arr[i] with the sum
            // Two possibilities either result == 0
            // or result > 0
            if ((arr[i] & sum) > 0) {

                // if result > 0 then arr[i] xored
                // with the sum1
                sum1 = (sum1 ^ arr[i]);
            }
            else {
                // if result == 0 then arr[i]
                // xored with sum2
                sum2 = (sum2 ^ arr[i]);
            }
        }

        // print the the two unique numbers
        System.out.println("The non-repeating elements are "
                           + sum1 + " and " + sum2);
    }

    public static void main(String[] args)
    {
        int[] arr = new int[] { 2, 3, 7, 9, 11, 2, 3, 11 };
        int n = arr.length;
        UniqueNumbers2(arr, n);
    }
}
// This code is contributed by Parshav Nahta
```

## 蟒蛇 3

```
# Python3 program for above approach

# This function sets the values of
# *x and *y to non-repeating elements
# in an array arr[] of size n

def UniqueNumbers2(arr, n):

    sums = 0

    for i in range(0, n):

        # Xor  all the elements of the array
        # all the elements occurring twice will
        # cancel out each other remaining
        # two unique numbers will be xored
        sums = (sums ^ arr[i])

    # Bitwise & the sum with it's 2's Complement
    # Bitwise & will give us the sum containing
    # only the rightmost set bit
    sums = (sums & -sums)

    # sum1 and sum2 will contains 2 unique
    # elements elements initialized with 0 box
    # number xored with 0 is number itself
    sum1 = 0
    sum2 = 0

    # Traversing the array again
    for i in range(0, len(arr)):

        # Bitwise & the arr[i] with the sum
        # Two possibilities either result == 0
        # or result > 0
        if (arr[i] & sums) > 0:

            # If result > 0 then arr[i] xored
            # with the sum1
            sum1 = (sum1 ^ arr[i])

        else:

            # If result == 0 then arr[i]
            # xored with sum2
            sum2 = (sum2 ^ arr[i])

    # Print the the two unique numbers
    print("The non-repeating elements are ",
          sum1, " and ", sum2)

# Driver Code
if __name__ == "__main__":

    arr = [2, 3, 7, 9, 11, 2, 3, 11]
    n = len(arr)

    UniqueNumbers2(arr, n)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for above approach
using System;

class GFG {

    // This function sets the values of
    // *x and *y to non-repeating elements
    // in an array arr[] of size n
    static void UniqueNumbers2(int[] arr, int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++) {

            // Xor  all the elements of the array
            // all the elements occurring twice will
            // cancel out each other remaining
            // two unique numbers will be xored
            sum = (sum ^ arr[i]);
        }

        // Bitwise & the sum with it's 2's Complement
        // Bitwise & will give us the sum containing
        // only the rightmost set bit
        sum = (sum & -sum);

        // sum1 and sum2 will contains 2 unique
        // elements elements initialized with 0 box
        // number xored with 0 is number itself
        int sum1 = 0;
        int sum2 = 0;

        // Traversing the array again
        for (int i = 0; i < arr.Length; i++) {

            // Bitwise & the arr[i] with the sum
            // Two possibilities either result == 0
            // or result > 0
            if ((arr[i] & sum) > 0) {

                // If result > 0 then arr[i] xored
                // with the sum1
                sum1 = (sum1 ^ arr[i]);
            }
            else {

                // If result == 0 then arr[i]
                // xored with sum2
                sum2 = (sum2 ^ arr[i]);
            }
        }

        // Print the the two unique numbers
        Console.WriteLine("The non-repeating "
                          + "elements are " + sum1 + " and "
                          + sum2);
    }

    // Driver Code
    static public void Main()
    {
        int[] arr = { 2, 3, 7, 9, 11, 2, 3, 11 };
        int n = arr.Length;

        UniqueNumbers2(arr, n);
    }
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
    // Javascript program for above approach

    // This function sets the values of
    // *x and *y to non-repeating elements
    // in an array arr[] of size n
    function UniqueNumbers2(arr, n)
    {
        let sum = 0;
        for(let i = 0; i < n; i++)
        {

            // Xor  all the elements of the array
            // all the elements occurring twice will
            // cancel out each other remaining
            // two unique numbers will be xored
            sum = (sum ^ arr[i]);
        }

        // Bitwise & the sum with it's 2's Complement
        // Bitwise & will give us the sum containing
        // only the rightmost set bit
        sum = (sum & -sum);

        // sum1 and sum2 will contains 2 unique
        // elements elements initialized with 0 box
        // number xored with 0 is number itself
        let sum1 = 0;
        let sum2 = 0;

        // Traversing the array again
        for(let i = 0; i < arr.length; i++)
        {

            // Bitwise & the arr[i] with the sum
            // Two possibilities either result == 0
            // or result > 0
            if ((arr[i] & sum) > 0)
            {

                // If result > 0 then arr[i] xored
                // with the sum1
                sum1 = (sum1 ^ arr[i]);
            }
            else
            {

                // If result == 0 then arr[i]
                // xored with sum2
                sum2 = (sum2 ^ arr[i]);
            }
        }

        // Print the the two unique numbers
        document.write("The non-repeating " +
                          "elements are " + sum1 +
                          " and " + sum2);
    }

    let arr = [ 2, 3, 7, 9, 11, 2, 3, 11 ];
    let n = arr.length;

    UniqueNumbers2(arr, n);

// This code is contributed by vaibhavrabadiya117.
</script>
```

**Output**

```
The non-repeating elements are 7 and 9
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

详细说明请参考下面的帖子:
[在一个未排序的数组中找到出现次数为奇数的两个数字](https://www.geeksforgeeks.org/find-the-two-numbers-with-odd-occurences-in-an-unsorted-array/)

**方法 3(使用地图)**

在这种方法中，我们简单地计算每个元素的频率。频率等于 1 的元素是不重复的数。下面的代码解释了解决方案-

## C++

```
// C++ program for Find the two non-repeating elements in
// an array of repeating elements/ Unique Numbers 2

#include <bits/stdc++.h>
using namespace std;

/* This function prints the two non-repeating elements in an
 * array of repeating elements*/

void get2NonRepeatingNos(int arr[], int n)
{
    /*Create map and calculate frequency of array
       elements.*/

    map<int, int> m;
    for (int i = 0; i < n; i++) {
        m[arr[i]]++;
    }

    /*Traverse through the map and check if its second
      element that is the frequency is 1 or not. If this is
      1 than it is the non-repeating element print it.It is
      clearly mentioned in problem that all numbers except
      two are repeated once. So they will be printed*/

    cout << "The non-repeating elements are ";
    for (auto& x : m) {
        if (x.second == 1) {
            cout << x.first << " ";
        }
    }
}

/* Driver code */
int main()
{
    int arr[] = { 2, 3, 7, 9, 11, 2, 3, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);
    get2NonRepeatingNos(arr, n);
}

// This code is contributed by Abhishek
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

//Java program to find 2 non repeating elements
//in array that has pairs of numbers

import java.util.*;
import java.io.*;

class GFG {

      //Method to print the 2 non repeating elements in an array
      public static void print2SingleNumbers(int[] nums){

          /*We use a TreeMap to store the elements
          in the sorted order*/
         TreeMap<Integer, Integer> map = new TreeMap<>();

          int n = nums.length;

          /*Iterate through the array and check if each
          element is present or not in the map. If the
        element is present, remove it from the array
        otherwise add it to the map*/

          for(int i = 0; i<n; i++){
            if(map.containsKey(nums[i]))
                  map.remove(nums[i]);
            else
                map.put(nums[i],1);
        }

          System.out.println("The non-repeating integers are " + map.firstKey() + " " + map.lastKey());
    }
      //Driver code
    public static void main (String[] args) {
        int[] nums = new int[]{2,11,3,11,7,3,9,2};
          print2SingleNumbers(nums);
    }
      //This code is contributed by Satya Anvesh R
}
```

**Output**

```
The non-repeating elements are 7 9 
```