# 通过仅交换 GCD 为 1 的对来对给定数组进行排序

> 原文:[https://www . geeksforgeeks . org/sort-a-给定数组-仅通过交换-pairs-with-gcd-as-1/](https://www.geeksforgeeks.org/sort-a-given-array-by-swapping-only-pairs-with-gcd-as-1/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是检查是否有可能[使用任意数量的操作对给定数组](https://www.geeksforgeeks.org/sorting-algorithms/)进行排序，其中在每个操作中，如果 **arr[i]** 和 **arr[j]** 的 [GCD](http://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 为 **1** ，则两个元素 **arr[i]** 可以交换。

**示例:**

> **输入:** a = {3，2，1}
> **输出:**可能
> **解释:**给定数组可以通过交换 arr[0]和 arr[2]进行排序，即 3 和 1 作为 gcd(3，1) = 1。
> 
> **输入:** arr[] = {10，15，6，2，9}
> **输出:**不可能
> **解释:**不可能使用任何有效操作序列对给定数组进行排序。
> 
> **输入:** arr[] = {1，9，3，7，2，4}
> **输出:**可能

**逼近:**借助[递归](http://www.geeksforgeeks.org/recursion/)和[回溯](http://www.geeksforgeeks.org/backtracking-algorithms/)可以解决给定的问题。创建一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)迭代给定数组的所有[求逆，如果它们的](https://www.geeksforgeeks.org/counting-inversions/) [*GCD*](http://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) *为 1* 则一次交换一个求逆元素，并递归调用剩余的数组。在任何时候，如果数组已经排序，可以使用 [is_sorted()函数](https://www.geeksforgeeks.org/stdis_sorted-in-cpp/)进行检查，则返回 **true** 否则返回 **false** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to check if it is
// possible to sort the given array by
// swapping elements with their GCD = 1
bool isPossible(vector<int> arr)
{
    // If the given array is sorted
    if (is_sorted(arr.begin(), arr.end())) {
        return true;
    }

    // Stores if it is possible to sort
    // the given array
    bool res = false;

    // Iterate for all possible pairs of
    // Inversions
    for (int i = 0; i < arr.size(); i++) {
        for (int j = i + 1; j < arr.size(); j++) {

            // If for current inversion,
            // GCD of both elements is 1,
            // GCD of both the indices
            if (arr[i] > arr[j]
                && __gcd(arr[i], arr[j]) == 1) {
                swap(arr[i], arr[j]);

                // Recursive Call for the
                // remaining array
                res = (res | isPossible(arr));

                // Backtrack
                swap(arr[i], arr[j]);
            }
        }
    }

    // Return Answer
    return res;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 9, 3, 7, 2, 4 };

    if (isPossible(arr))
        cout << "Possible";
    else
        cout << "Not Possible";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Recursive function to check if it is
// possible to sort the given array by
// swapping elements with their GCD = 1
static boolean isPossible(int[] arr)
{

    // If the given array is sorted
    if (is_sorted(arr)) {
        return true;
    }

    // Stores if it is possible to sort
    // the given array
    boolean res = false;

    // Iterate for all possible pairs of
    // Inversions
    for (int i = 0; i < arr.length; i++) {
        for (int j = i + 1; j < arr.length; j++) {

            // If for current inversion,
            // GCD of both elements is 1,
            // GCD of both the indices
            if (arr[i] > arr[j]
                && __gcd(arr[i], arr[j]) == 1) {
                arr = swap(arr,i,j);

                // Recursive Call for the
                // remaining array
                res = (res | isPossible(arr));

                // Backtrack
                arr = swap(arr,i,j);
            }
        }
    }

    // Return Answer
    return res;
}
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}
static int[] swap(int []arr, int i, int j){
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}
private static boolean is_sorted(int[] a) {
    int i;
    for(i = 0; i < a.length - 1 && a[i] < a[i+1]; i++){}
    return (i == a.length - 1);
}

public static void main(String[] args)
{
    int[] arr = { 1, 9, 3, 7, 2, 4 };

    if (isPossible(arr))
        System.out.print("Possible");
    else
        System.out.print("Not Possible");

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python code for the above approach

# Recursive function to return gcd of a and b
def __gcd(a, b):

    # Everything divides 0
    if (a == 0):
        return b
    if (b == 0):
        return a

    # base case
    if (a == b):
        return a

    # a is greater
    if (a > b):
        return __gcd(a - b, b)
    return __gcd(a, b - a)

# Recursive function to check if it is
# possible to sort the given array by
# swapping elements with their GCD = 1
def isPossible(arr):

    # If the given array is sorted
    brr = sorted(arr)
    if (arr == brr):
        return True

    # Stores if it is possible to sort
    # the given array
    res = False

    # Iterate for all possible pairs of
    # Inversions
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):

            # If for current inversion,
            # GCD of both elements is 1,
            # GCD of both the indices
            if (arr[i] > arr[j] and __gcd(arr[i], arr[j]) == 1):
                temp = arr[i]
                arr[i] = arr[j]
                arr[j] = temp

                # Recursive Call for the
                # remaining array
                res = (res | isPossible(arr))

                # Backtrack
                temp = arr[i]
                arr[i] = arr[j]
                arr[j] = temp

    # Return Answer
    return res

# Driver Code
arr = [1, 9, 3, 7, 2, 4]
if (isPossible(arr)):
    print("Possible")
else:
    print("Not Possible")

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

// Recursive function to check if it is
// possible to sort the given array by
// swapping elements with their GCD = 1
static bool isPossible(int[] arr)
{

    // If the given array is sorted
    if (is_sorted(arr)) {
        return true;
    }

    // Stores if it is possible to sort
    // the given array
    bool res = false;

    // Iterate for all possible pairs of
    // Inversions
    for (int i = 0; i < arr.Length; i++) {
        for (int j = i + 1; j < arr.Length; j++) {

            // If for current inversion,
            // GCD of both elements is 1,
            // GCD of both the indices
            if (arr[i] > arr[j]
                && __gcd(arr[i], arr[j]) == 1) {
                arr = swap(arr,i,j);

                // Recursive Call for the
                // remaining array
                res = (res | isPossible(arr));

                // Backtrack
                arr = swap(arr,i,j);
            }
        }
    }

    // Return Answer
    return res;
}
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}
static int[] swap(int []arr, int i, int j){
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}
private static bool is_sorted(int[] a) {
    int i;
    for(i = 0; i < a.Length - 1 && a[i] < a[i+1]; i++){}
    return (i == a.Length - 1);
}

public static void Main(String[] args)
{
    int[] arr = { 1, 9, 3, 7, 2, 4 };

    if (isPossible(arr))
        Console.Write("Possible");
    else
        Console.Write("Not Possible");

}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
  <script>
        // JavaScript code for the above approach

        // Recursive function to return gcd of a and b
        function __gcd(a, b)
        {

            // Everything divides 0
            if (a == 0)
                return b;
            if (b == 0)
                return a;

            // base case
            if (a == b)
                return a;

            // a is greater
            if (a > b)
                return __gcd(a - b, b);
            return __gcd(a, b - a);
        }

        // Recursive function to check if it is
        // possible to sort the given array by
        // swapping elements with their GCD = 1
        function isPossible(arr)
        {

            // If the given array is sorted
            brr = arr.sort(function (a, b) { return a - b })
            if (arr == brr) {
                return true;
            }

            // Stores if it is possible to sort
            // the given array
            let res = false;

            // Iterate for all possible pairs of
            // Inversions
            for (let i = 0; i < arr.length; i++)
            {
                for (let j = i + 1; j < arr.length; j++)
                {

                    // If for current inversion,
                    // GCD of both elements is 1,
                    // GCD of both the indices
                    if (arr[i] > arr[j]
                        && __gcd(arr[i], arr[j]) == 1) {
                        let temp = arr[i];
                        arr[i] = arr[j];
                        arr[j] = temp;

                        // Recursive Call for the
                        // remaining array
                        res = (res | isPossible(arr));

                        // Backtrack
                        temp = arr[i];
                        arr[i] = arr[j];
                        arr[j] = temp;
                    }
                }
            }

            // Return Answer
            return res;
        }

        // Driver Code
        let arr = [1, 9, 3, 7, 2, 4];
        if (isPossible(arr))
            document.write("Possible")
        else
            document.write("Not Possible");

// This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
Possible
```

***时间复杂度:** O(N <sup>2</sup> N！)*
***辅助空间:** O(1)*