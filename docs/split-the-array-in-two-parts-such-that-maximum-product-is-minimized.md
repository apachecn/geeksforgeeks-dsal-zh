# 将阵列分成两部分，使最大乘积最小化

> 原文:[https://www . geeksforgeeks . org/将阵列分成两部分，以使最大产品最小化/](https://www.geeksforgeeks.org/split-the-array-in-two-parts-such-that-maximum-product-is-minimized/)

给定一个整数[数组](https://www.geeksforgeeks.org/array-data-structure/)，大小为**N(<= 16)**的**arr【】**，任务是将数组划分为 2 个部分，使得 2 个半部分的最大乘积最小。求一半的最小最大乘积。如果数组为空，打印 **-1。**

**示例:**

> **输入:** arr[] = {3，5，7}
> **输出:** 15
> **解释:**可能的分区是–
> ->{ 5，7}，{ 3 }–这里的产品是 35 和 3，最大产品是 35
> - > {3，7}，{ 5 }–这里的产品是 21 和 5，最大产品是 21【T11 { 7 }–这里的产品是 15 和 7，最大产品是 15
> - > {5，7，3}，{ }–这里的产品是 105 和 0，最大产品是 105
> 
> 在获得的最大乘积中，即从 105、35、21 和 15，最小值是 15，因此我们需要的答案是 15。
> 
> **输入:** arr[] = { 10 }
> **输出:** 10
> **说明:**由于数组包含单个元素，数组无法进一步划分。因此，前半部分包含 10，另一半不包含任何元素。因此，答案是 10。

**方法:**由于 **N** 的值小于 **16** 这个问题可以通过使用[位屏蔽](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)来解决，即将位于设定位位置的所有数字相乘并将其放入一侧，类似地，将所有未设定位位置相乘并将其存储在另一半中，找到最大值并将其存储在[集合](http://www.geeksforgeeks.org/multiset-in-cpp-stl/)中，最后返回[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)的第一个元素。

按照以下步骤解决问题:

*   [初始化一个集合](https://www.geeksforgeeks.org/set-in-cpp-stl/) **st[]** 来按顺序存储可能的答案。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，2 <sup>N</sup> )** ，并执行以下任务:
    *   将变量 **product1** 和 **product2** 初始化为 **1** 。
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下任务:
        *   如果 **i & (1 < < j)** 为**真，**则将值**arr【j】**乘以变量 **product1** 否则乘以变量 **product2。**
    *   [将**产品 1** 或**产品 2** 的最大值插入](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/) **st[]。**
*   执行上述步骤后，打印集合的第一个值作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum of the
// maximum product of the 2 halves
void findMinimum(vector<int>& arr, int N)
{

    // Set to store the possible answers
    // in ascending order.
    set<int> st;

    // Traverse over the all possible
    for (int i = 0; i < (1 << N); i++) {

        // Variables to find the product
        // of set bits at set positions
        // and unset bits at unset positions
        int product1 = 1, product2 = 1;

        // Traverse over the array
        for (int j = 0; j < N; j++) {

            // Check the condition
            if (i & (1 << j)) {
                product1 = product1 * arr[j];
            }
            else {
                product2 = product2 * arr[j];
            }
        }

        // Insert the maximum one
        st.insert(max(product1, product2));
    }

    cout << *st.begin() << "\n";
}

// Driver Code
int main()
{
    vector<int> arr = { 3, 5, 7 };
    int N = arr.size();

    findMinimum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class GFG
{
// Function to find the minimum of the
// maximum product of the 2 halves
static void findMinimum(int []arr, int N)
{

    // Set to store the possible answers
    // in ascending order.
    HashSet<Integer> st = new HashSet<Integer>();

    // Traverse over the all possible
    for (int i = 0; i < (1 << N); i++) {

        // Variables to find the product
        // of set bits at set positions
        // and unset bits at unset positions
        int product1 = 1, product2 = 1;

        // Traverse over the array
        for (int j = 0; j < N; j++) {

            // Check the condition
            if ((i & (1 << j)) == 0) {
                product1 = product1 * arr[j];
            }
            else {
                product2 = product2 * arr[j];
            }
        }

        // Insert the maximum one
        st.add(Math.max(product1, product2));
    }
    int ans = 0;
    for (int x : st) {
        ans = x;
    }
    System.out.print(ans);
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 3, 5, 7 };
    int N = arr.length;

    findMinimum(arr, N);

}
}
// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum of the
# maximum product of the 2 halves
def findMinimum(arr, N):

    # Set to store the possible answers
    # in ascending order.
    st = set([])

    # Traverse over the all possible
    for i in range((1 << N)):

        # Variables to find the product
        # of set bits at set positions
        # and unset bits at unset positions
        product1 = 1
        product2 = 1

        # Traverse over the array
        for j in range(N):

            # Check the condition
            if (i & (1 << j)):
                product1 = product1 * arr[j]
            else:
                product2 = product2 * arr[j]

        # Insert the maximum one
        st.add(max(product1, product2))

    print(list(st)[-1])

# Driver Code
if __name__ == "__main__":

    arr = [ 3, 5, 7 ]
    N = len(arr)

    findMinimum(arr, N)

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// Function to find the minimum of the
// maximum product of the 2 halves
static void findMinimum(int []arr, int N)
{

    // Set to store the possible answers
    // in ascending order.
    HashSet<int> st = new HashSet<int>();

    // Traverse over the all possible
    for (int i = 0; i < (1 << N); i++) {

        // Variables to find the product
        // of set bits at set positions
        // and unset bits at unset positions
        int product1 = 1, product2 = 1;

        // Traverse over the array
        for (int j = 0; j < N; j++) {

            // Check the condition
            if ((i & (1 << j)) == 0) {
                product1 = product1 * arr[j];
            }
            else {
                product2 = product2 * arr[j];
            }
        }

        // Insert the maximum one
        st.Add(Math.Max(product1, product2));
    }
    int ans = 0;
    foreach (int x in st) {
        ans = x;
    }
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    int []arr = { 3, 5, 7 };
    int N = arr.Length;

    findMinimum(arr, N);

}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum of the
        // maximum product of the 2 halves
        function findMinimum(arr, N) {

            // Set to store the possible answers
            // in ascending order.
            let st = new Set();

            // Traverse over the all possible
            for (let i = 0; i < (1 << N); i++) {

                // Variables to find the product
                // of set bits at set positions
                // and unset bits at unset positions
                let product1 = 1;
                let product2 = 1;

                // Traverse over the array
                for (let j = 0; j < N; j++) {

                    // Check the condition
                    if (i & (1 << j)) {
                        product1 = product1 * arr[j];
                    }
                    else {
                        product2 = product2 * arr[j];
                    }
                }

                // Insert the maximum one
                st.add(Math.max(product1, product2));
            }
            const last = [...st][st.size - 1];
            document.write(last);
        }

        // Driver Code
        let arr = [3, 5, 7];
        let N = arr.length;

        findMinimum(arr, N);

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
15
```

***时间复杂度:**(o((2^n)*(n*log(n))*
***辅助空间:** O(N)*