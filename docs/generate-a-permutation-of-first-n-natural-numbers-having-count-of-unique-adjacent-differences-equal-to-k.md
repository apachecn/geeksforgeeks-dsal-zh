# 生成前 N 个自然数的排列，其唯一相邻差的计数等于 K

> 原文:[https://www . geesforgeks . org/generate-a-排列第一个 n 个自然数-有-计数-唯一-相邻-差异-等于-k/](https://www.geeksforgeeks.org/generate-a-permutation-of-first-n-natural-numbers-having-count-of-unique-adjacent-differences-equal-to-k/)

给定两个正整数 **N** 和 **K** ，任务是构造第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)的[排列](https://www.geeksforgeeks.org/permutation-and-combination/)，使得相邻元素之间所有可能的绝对差都是 **K** 。

**示例:**

> **输入:** N = 3，K = 1
> **输出:** 1 2 3
> **说明:**考虑排列{1，2，3}，所有可能的相邻元素唯一绝对差为{1}。由于计数为 1(= K)，打印序列{1，2，3}作为结果排列。
> 
> **输入:** N = 3，K = 2
> T3】输出: 1 3 2

**天真方法:**解决给定问题的最简单方法是创建一个数组，其中元素从 **1** 到 **N** 按升序排列，然后[遍历数组的前 K 个元素](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[反转子数组](https://www.geeksforgeeks.org/reverse-an-array-upto-a-given-position/)从当前索引开始，到最后一个索引结束。完成上述步骤后，打印得到的结果数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to reverse the given list
void reverse(int list[], int start, int end)
{

    // Iterate until start < end
    while (start < end)
    {

        // Swap operation
        int temp = list[start];
        list[start] = list[end];
        list[end] = temp;

        start++;
        end--;
    }
}

// Function to construct a list with
// exactly K unique adjacent element
// differences
void makeList(int N, int K)
{

    // Stores the resultant array
    int list[N];

    // Add initial value to array
    for(int i = 1; i <= N; i++)
    {
        list[i - 1] = i;
    }

    // Reverse the list k-1 times
    // from index i to n-1
    for(int i = 1; i < K; i++)
    {
        reverse(list, i, N - 1);
    }

    // Print the resultant array
    for(int i = 0; i < N; i++)
    {
        cout << list[i] << " ";
    }
}

// Driver code
int main()
{
    int N = 6, K = 3;
    makeList(N, K);

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to construct a list with
    // exactly K unique adjacent element
    // differences
    public static void makeList(int N, int K)
    {
        // Stores the resultant array
        int[] list = new int[N];

        // Add initial value to array
        for (int i = 1; i <= N; i++) {
            list[i - 1] = i;
        }

        // Reverse the list k-1 times
        // from index i to n-1
        for (int i = 1; i < K; i++) {
            reverse(list, i, N - 1);
        }

        // Print the resultant array
        for (int i = 0;
             i < list.length; i++) {
            System.out.print(list[i] + " ");
        }
    }

    // Function to reverse the given list
    public static void reverse(
        int[] list, int start, int end)
    {
        // Iterate until start < end
        while (start < end) {

            // Swap operation
            int temp = list[start];
            list[start] = list[end];
            list[end] = temp;

            start++;
            end--;
        }
    }

    // Driver Code
    public static void main(
        String[] args)
    {
        int N = 6, K = 3;
        makeList(N, K);
    }
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to reverse the given lst
def reverse(lst, start,  end):

    # Iterate until start < end
    while (start < end):

        # Swap operation
        temp = lst[start]
        lst[start] = lst[end]
        lst[end] = temp

        start += 1
        end -= 1

# Function to construct a lst with
# exactly K unique adjacent element
# differences
def makelst(N, K):

    # Stores the resultant array
    lst = [0 for i in range(N)]

    # Add initial value to array
    for i in range(1, N + 1, 1):
        lst[i - 1] = i

    # Reverse the lst k-1 times
    # from index i to n-1
    for i in range(1, K, 1):
        reverse(lst, i, N - 1)

    # Print the resultant array
    for i in range(N):
        print(lst[i], end = " ")

# Driver code
if __name__ == '__main__':
    N = 6
    K = 3
    makelst(N, K)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to construct a list with
// exactly K unique adjacent element
// differences
public static void makeList(int N, int K)
{

    // Stores the resultant array
    int[] list = new int[N];

    // Add initial value to array
    for(int i = 1; i <= N; i++)
    {
        list[i - 1] = i;
    }

    // Reverse the list k-1 times
    // from index i to n-1
    for(int i = 1; i < K; i++)
    {
        reverse(list, i, N - 1);
    }

    // Print the resultant array
    for(int i = 0; i < list.Length; i++)
    {
        Console.Write(list[i] + " ");
    }
}

// Function to reverse the given list
public static void reverse(int[] list, int start,
                           int end)
{

    // Iterate until start < end
    while (start < end)
    {

        // Swap operation
        int temp = list[start];
        list[start] = list[end];
        list[end] = temp;

        start++;
        end--;
    }
}

// Driver Code
static public void Main()
{
    int N = 6, K = 3;

    makeList(N, K);
}
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to construct a list with
    // exactly K unique adjacent element
    // differences
    function makeList(N, K)
    {
        // Stores the resultant array
        let list = Array.from(Array(N), ()=>Array(0));

        // Add initial value to array
        for (let i = 1; i <= N; i++) {
            list[i - 1] = i;
        }

        // Reverse the list k-1 times
        // from index i to n-1
        for (let i = 1; i < K; i++) {
            reverse(list, i, N - 1);
        }

        // Print the resultant array
        for (let i = 0;
             i < list.length; i++) {
            document.write(list[i] + " ");
        }
    }

    // Function to reverse the given list
    function reverse(
        list, start, end)
    {
        // Iterate until start < end
        while (start < end) {

            // Swap operation
            let temp = list[start];
            list[start] = list[end];
            list[end] = temp;

            start++;
            end--;
        }
    }

// Driver Code

    let N = 6, K = 3;
    makeList(N, K);

 // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
1 6 2 3 4 5
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法也可以使用[双指针方法](https://www.geeksforgeeks.org/two-pointers-technique/)进行优化。按照以下步骤解决问题:

*   初始化一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **ans[]** ，该数组存储结果排列。
*   创建两个变量，分别称**左**和**右**为 **1** 和**N***。*
*   [遍历给定数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并执行以下步骤:
    *   如果 **K** 的值为偶数，则将**左**的值推至数组**ans【】**并将**左**的值增加 **1** 。
    *   如果 **K** 的值为奇数，则将**右***T5】的值推至数组**ans【】**，将**右**的值递减 **1** *。**
    *   如果***K**的值大于 1，则 **K** 的值递减 **1** 。*
*   *完成以上步骤后，[打印阵列](https://www.geeksforgeeks.org/java-program-to-print-the-elements-of-an-array/) **ans[]** 。*

*下面是上述方法的实现:*

## *C++*

```
*// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;
// Function to construct the list
// with exactly K unique adjacent
// element differences
void makeList(int N, int K)
{
    // Stores the resultant array
    int list[N];

    // Stores the left and the right
    // most element of the range
    int left = 1;
    int right = N;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If k is even, the add
        // left to array and
        // increment the left
        if (K % 2 == 0) {
            list[i] = left;
            left = left + 1;
        }

        // If k is odd, the add
        // right to array and
        // decrement the right
        else {
            list[i] = right;
            right = right - 1;
        }

        // Repeat the steps for
        // k-1 times
        if (K > 1)
            K--;
    }

    // Print the resultant list
    for (int i = 0; i < N; i++) {
            cout<<list[i]<< " ";
}
}

// Driver Code
int main()
{
    int N = 6;
    int K = 3;
    makeList(N, K);
}

// This code is contributed by ukasp.*
```

## *Java 语言(一种计算机语言，尤用于创建网站)*

```
*// Java program for the above approach

class GFG {

    // Function to construct the list
    // with exactly K unique adjacent
    // element differences
    public static void makeList(int N,
                                int K)
    {
        // Stores the resultant array
        int[] list = new int[N];

        // Stores the left and the right
        // most element of the range
        int left = 1;
        int right = N;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // If k is even, the add
            // left to array and
            // increment the left
            if (K % 2 == 0) {
                list[i] = left;
                left = left + 1;
            }

            // If k is odd, the add
            // right to array and
            // decrement the right
            else {
                list[i] = right;
                right = right - 1;
            }

            // Repeat the steps for
            // k-1 times
            if (K > 1)
                K--;
        }

        // Print the resultant list
        for (int i = 0;
             i < list.length; i++) {
            System.out.print(
                list[i] + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 6;
        int K = 3;
        makeList(N, K);
    }
}*
```

## *蟒蛇 3*

```
*# Python3 program for the above approach

# Function to construct the lst
# with exactly K unique adjacent
# element differences
def makelst(N, K):

    # Stores the resultant array
    lst = [0 for i in range(N)]

    # Stores the left and the right
    # most element of the range
    left = 1
    right = N

    # Traverse the array
    for i in range(N):

        # If k is even, the add
        # left to array and
        # increment the left
        if (K % 2 == 0):
            lst[i] = left
            left = left + 1

        # If k is odd, the add
        # right to array and
        # decrement the right
        else:
            lst[i] = right
            right = right - 1

        # Repeat the steps for
        # k-1 times
        if (K > 1):
            K -= 1

    # Print the resultant lst
    for i in range(N):
        print(lst[i], end = " ")

# Driver Code
if __name__ == '__main__':

    N = 6
    K = 3

    makelst(N, K)

# This code is contributed by bgangwar59*
```

## *C#*

```
*// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to construct the list
// with exactly K unique adjacent
// element differences
public static void makeList(int N, int K)
{

    // Stores the resultant array
    int[] list = new int[N];

    // Stores the left and the right
    // most element of the range
    int left = 1;
    int right = N;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If k is even, the add
        // left to array and
        // increment the left
        if (K % 2 == 0)
        {
            list[i] = left;
            left = left + 1;
        }

        // If k is odd, the add
        // right to array and
        // decrement the right
        else
        {
            list[i] = right;
            right = right - 1;
        }

        // Repeat the steps for
        // k-1 times
        if (K > 1)
            K--;
    }

    // Print the resultant list
    for(int i = 0; i < list.Length; i++)
    {
        Console.Write(list[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 6;
    int K = 3;

    makeList(N, K);
}
}

// This code is contributed by 29AjayKumar*
```

## *java 描述语言*

```
*<script>

// Javascript program for the above approach

// Function to construct the list
// with exactly K unique adjacent
// element differences
function makeList(N, K)
{

    // Stores the resultant array
    var list= new Array(N);

    // Stores the left and the right
    // most element of the range
    var left = 1;
    var right = N;

    // Traverse the array
    for(var i = 0; i < N; i++)
    {

        // If k is even, the add
        // left to array and
        // increment the left
        if (K % 2 == 0)
        {
            list[i] = left;
            left = left + 1;
        }

        // If k is odd, the add
        // right to array and
        // decrement the right
        else
        {
            list[i] = right;
            right = right - 1;
        }

        // Repeat the steps for
        // k-1 times
        if (K > 1)
            K--;
    }

    // Print the resultant list
    for(var i = 0; i < N; i++)
    {
        document.write(list[i] + " ");
    }
}

// Driver code
var  N = 6;
var K = 3;

makeList(N, K);

// This code is contributed by SoumikMondal

</script>*
```

***Output:** 

```
6 1 5 4 3 2
```* 

****时间复杂度:**O(N)*
T5**辅助空间:** O(N)*