# 找到排序后形成一个 AP 且具有最小最大值的数组

> 原文:[https://www . geesforgeks . org/find-the-array-what-what-sorted-form-a-AP-and-has-minimum-maximum/](https://www.geeksforgeeks.org/find-the-array-which-when-sorted-forms-an-ap-and-has-minimum-maximum/)

给定三个正整数 **N** 、 **X** 和 **Y(X < Y)** 。任务是找到一个包含 **X** 和 **Y** 的长度为 **N** 的数组，当按照**递增**的顺序排序时，该数组必须形成一个**等差数列**

**示例:**

> ***输入:*** N = 5，X = 20，Y = 50
> ***输出:*** 20 30 40 50 10
> ***说明:*** 数组按递增顺序排序时形成一个等差数列 10 *。*
> 
> ***输入:*** N = 17，X = 23445，Y = 1000000
> ***输出:***23445 218756 414067 609378 804689 1000000 1195311 1390622 1585933 1781244 1976555 2171866

**逼近:**在这个问题中，可以观察到如果**最大**元素要**最小化**，那么可以假设 **Y** 应该是最大的元素。如果 **Y** 最大，那么剩余的每个元素都将小于或等于 **Y** 。如果 **Y** 不是数组中最大的元素，那么可以考虑大于 **Y** 的元素。

按照以下步骤解决给定的问题:

*   检查 **X** 和 **Y** 之间是否存在一些相同的差异元素。为此，检查( **Y-X** )是否可被( **N** -1)整除。如果可以整除，则减少 **N** ，公差 d 由下式给出:

> d = (Y-X)/(N-1)

*   如果它不能被整除，则减少(n-1)并循环重复上述步骤，直到分母不为零。
*   如果 X 和 Y 之间不存在任何这样的元素，那么公共差 d 由下式给出:

> d = (Y-X)

*   让结果数组存储在向量**和**中。将向量**和**中的 **X** 和 **Y** 之间的元素推送到 for 循环中。
*   如果 **N** 不等于零，则从( **X-d** )开始插入**和**中具有共同差异的元素 **d** 。
*   如果 **N** 等于零，输出 **ans** 。否则，从( **Y+d** 开始，将元素插入 **ans** 中，直到获得所需的数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the array which when
// sorted forms an arithmetic progression
// and has the minimum possible maximum element
void findArray(int N, int X, int Y)
{
    // Stores the difference of Y and X
    int r = Y - X;

    // To indicate the absence of required
    // elements between X and Y
    int d = -1;

    // Stores the number of required elements
    // present between X and Y
    int num = 0;

    // Loop to find the number of required
    // elements between X and Y
    for (int i = (N - 1); i > 0; i--) {

        // If r is divisible by i
        if (r % i == 0) {

            // Stores the common difference
            // of the elements
            d = r / i;

            // Decrease num by 1
            num = i - 1;

            // Break from the loop
            break;
        }
    }

    // If the number of elements present
    // between X and Y is zero
    if (d == -1) {

        // Update common difference
        d = Y - X;
    }

    // Update N
    N = N - 2 - num;

    // Stores the resultant array
    vector<int> ans;

    // Loop to insert the found elements
    // in the resultant vector
    for (int i = X; i <= Y; i += d) {
        ans.push_back(i);
    }

    // Stores the element to be inserted in
    // the resultant vector
    int i = X;

    // Loop to insert elements less than X
    // in the resultant vector
    while (N > 0 && i > 0) {
        i = i - d;

        // i must be positive
        if (i > 0) {
            ans.push_back(i);

            // Update N
            N--;
        }
    }

    // Stores the element to be inserted in
    // the resultant vector
    i = Y;

    // Loop to insert elements greater than Y
    // in the resultant vector
    while (N > 0) {
        i = i + d;
        ans.push_back(i);

        // Update N
        N--;
    }

    // Output the required array
    for (int i = 0; i < ans.size(); ++i) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given N, X and Y
    int N = 5, X = 20, Y = 50;

    // Function Call
    findArray(N, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;

class GFG {

    // Function to find the array which when
    // sorted forms an arithmetic progression
    // and has the minimum possible maximum element
    static void findArray(int N, int X, int Y) {

        // Stores the difference of Y and X
        int r = Y - X;

        // To indicate the absence of required
        // elements between X and Y
        int d = -1;

        // Stores the number of required elements
        // present between X and Y
        int num = 0;

        // Loop to find the number of required
        // elements between X and Y
        for (int i = (N - 1); i > 0; i--) {

            // If r is divisible by i
            if (r % i == 0) {

                // Stores the common difference
                // of the elements
                d = r / i;

                // Decrease num by 1
                num = i - 1;

                // Break from the loop
                break;
            }
        }

        // If the number of elements present
        // between X and Y is zero
        if (d == -1) {

            // Update common difference
            d = Y - X;
        }

        // Update N
        N = N - 2 - num;

        // Stores the resultant array
        ArrayList<Integer> ans = new ArrayList<Integer>();

        // Loop to insert the found elements
        // in the resultant vector
        for (int i = X; i <= Y; i += d) {
            ans.add(i);
        }

        // Stores the element to be inserted in
        // the resultant vector
        int j = X;

        // Loop to insert elements less than X
        // in the resultant vector
        while (N > 0 && j > 0) {
            j = j - d;

            // i must be positive
            if (j > 0) {
                ans.add(j);

                // Update N
                N--;
            }
        }

        // Stores the element to be inserted in
        // the resultant vector
        j = Y;

        // Loop to insert elements greater than Y
        // in the resultant vector
        while (N > 0) {
            j = j + d;
            ans.add(j);

            // Update N
            N--;
        }

        // Output the required array
        for (int i = 0; i < ans.size(); ++i) {
            System.out.print(ans.get(i) + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given N, X and Y
        int N = 5, X = 20, Y = 50;

        // Function Call
        findArray(N, X, Y);
    }
}

 // This code is contributed by gfgking.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the array which when
# sorted forms an arithmetic progression
# and has the minimum possible maximum element
def findArray(N, X, Y):

    # Stores the difference of Y and X
    r = Y - X

    # To indicate the absence of required
    # elements between X and Y
    d = -1

    # Stores the number of required elements
    # present between X and Y
    num = 0

    # Loop to find the number of required
    # elements between X and Y
    for i in range(N - 1, 0, -1):

        # If r is divisible by i
        if (r % i == 0):

            # Stores the common difference
            # of the elements
            d = r // i

            # Decrease num by 1
            num = i - 1

            # Break from the loop
            break

    # If the number of elements present
    # between X and Y is zero
    if (d == -1):

        # Update common difference
        d = Y - X

    # Update N
    N = N - 2 - num

    # Stores the resultant array
    ans = []

    # Loop to insert the found elements
    # in the resultant vector
    for i in range(X, Y + 1, d):
        ans.append(i)

    # Stores the element to be inserted in
    # the resultant vector
    i = X

    # Loop to insert elements less than X
    # in the resultant vector
    while (N > 0 and i > 0):
        i = i - d

        # i must be positive
        if (i > 0):
            ans.append(i)

            # Update N
            N -= 1

    # Stores the element to be inserted in
    # the resultant vector
    i = Y

    # Loop to insert elements greater than Y
    # in the resultant vector
    while (N > 0):
        i = i + d
        ans.append(i)

        # Update N
        N -= 1

    # Output the required array
    for i in range(0, len(ans)):
        print(ans[i], end=" ")

# Driver Code
if __name__ == "__main__":

    # Given N, X and Y
    N = 5
    X = 20
    Y = 50

    # Function Call
    findArray(N, X, Y)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function to find the array which when
// sorted forms an arithmetic progression
// and has the minimum possible maximum element
static void findArray(int N, int X, int Y)
{

    // Stores the difference of Y and X
    int r = Y - X;

    // To indicate the absence of required
    // elements between X and Y
    int d = -1;

    // Stores the number of required elements
    // present between X and Y
    int num = 0;

    // Loop to find the number of required
    // elements between X and Y
    for (int i = (N - 1); i > 0; i--) {

        // If r is divisible by i
        if (r % i == 0) {

            // Stores the common difference
            // of the elements
            d = r / i;

            // Decrease num by 1
            num = i - 1;

            // Break from the loop
            break;
        }
    }

    // If the number of elements present
    // between X and Y is zero
    if (d == -1) {

        // Update common difference
        d = Y - X;
    }

    // Update N
    N = N - 2 - num;

    // Stores the resultant array
    List<int> ans = new List<int>();

    // Loop to insert the found elements
    // in the resultant vector
    for (int i = X; i <= Y; i += d) {
        ans.Add(i);
    }

    // Stores the element to be inserted in
    // the resultant vector
    int j = X;

    // Loop to insert elements less than X
    // in the resultant vector
    while (N > 0 && j > 0) {
        j = j - d;

        // i must be positive
        if (j > 0) {
            ans.Add(j);

            // Update N
            N--;
        }
    }

    // Stores the element to be inserted in
    // the resultant vector
    j = Y;

    // Loop to insert elements greater than Y
    // in the resultant vector
    while (N > 0) {
        j = j + d;
        ans.Add(j);

        // Update N
        N--;
    }

    // Output the required array
    for (int i = 0; i < ans.Count; ++i) {
        Console.Write( ans[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    // Given N, X and Y
    int N = 5, X = 20, Y = 50;

    // Function Call
    findArray(N, X, Y);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function to find the array which when
       // sorted forms an arithmetic progression
       // and has the minimum possible maximum element
       function findArray(N, X, Y)
       {

           // Stores the difference of Y and X
           let r = Y - X;

           // To indicate the absence of required
           // elements between X and Y
           let d = -1;

           // Stores the number of required elements
           // present between X and Y
           let num = 0;

           // Loop to find the number of required
           // elements between X and Y
           for (let i = (N - 1); i > 0; i--) {

               // If r is divisible by i
               if (r % i == 0) {

                   // Stores the common difference
                   // of the elements
                   d = r / i;

                   // Decrease num by 1
                   num = i - 1;

                   // Break from the loop
                   break;
               }
           }

           // If the number of elements present
           // between X and Y is zero
           if (d == -1) {

               // Update common difference
               d = Y - X;
           }

           // Update N
           N = N - 2 - num;

           // Stores the resultant array
           let ans = [];

           // Loop to insert the found elements
           // in the resultant vector
           for (let i = X; i <= Y; i += d) {
               ans.push(i);
           }

           // Stores the element to be inserted in
           // the resultant vector
           let i = X;

           // Loop to insert elements less than X
           // in the resultant vector
           while (N > 0 && i > 0) {
               i = i - d;

               // i must be positive
               if (i > 0) {
                   ans.push(i);

                   // Update N
                   N--;
               }
           }

           // Stores the element to be inserted in
           // the resultant vector
           i = Y;

           // Loop to insert elements greater than Y
           // in the resultant vector
           while (N > 0) {
               i = i + d;
               ans.push(i);

               // Update N
               N--;
           }

           // Output the required array
           for (let i = 0; i < ans.length; ++i) {
               document.write(ans[i] + " ");
           }
       }

       // Driver Code

       // Given N, X and Y
       let N = 5, X = 20, Y = 50;

       // Function Call
       findArray(N, X, Y);

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
20 30 40 50 10 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)