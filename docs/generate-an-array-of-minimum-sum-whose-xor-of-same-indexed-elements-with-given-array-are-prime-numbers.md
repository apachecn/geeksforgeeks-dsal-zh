# 生成一个最小和数组，其给定数组的同索引元素的异或是素数

> 原文:[https://www . geeksforgeeks . org/生成具有给定数组的相同索引元素的最小和异或数组是素数/](https://www.geeksforgeeks.org/generate-an-array-of-minimum-sum-whose-xor-of-same-indexed-elements-with-given-array-are-prime-numbers/)

给定一个由**n**(*1≤n≤10<sup>5</sup>*)整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是生成一个由 **N 个非零元素**组成的数组**b【**，使得**a<sub>I</sub>t19】^**b<sub>I</sub>****

***注:**应尽量减少得到的 xor 之和。*

**示例:**

> ***输入:** arr[] = {5，4，7，6}*
> ***输出:** {7，6，5，4}*
> ***说明:***
> ***2** 是最小素数。因此，**将 A[i]** 与(A[i] ^ 2)*
> *进行异或运算，给出了最小的素数。*
> ***a[I]^(a[I]^ 2)=(a[I]^ a[I])^ 2 = 0 ^ 2 = 2***
> *因为*
> *1。5 的异或^ 7 = 2，即素数*
> *2。4 ^ 6 = 2 的异或，它是素数。*
> *3。7 ^ 5 = 2 的异或，它是素数。*
> *4。6 ^ 4 = 2 的异或，它是素数。*
> *结果总和为–2+2+2+2 = 8，这是最小可能值*
> 
> ***输入:** arr[] = {10，16}*
> ***输出:** {8，18}*

**方法:**这个问题可以用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。按照以下步骤解决问题:

1.  因为 2 是可能的最小素数，所以 **Arr[i]** 与 **B[i] = (Arr[i] ^ 2)** 的 **XOR** 将给出一个[素数](https://www.geeksforgeeks.org/prime-numbers/) **2** 。
2.  当任何数组元素本身为 **Arr[i] = 2** 时，矛盾就产生了。在这种情况下， **B[i] = 2 ^ 2** 导致 **0** 。
3.  因此，如果 **Arr[i] = 2** ，设置 **B[i] = (2 ^ 3) = 1** ，使得 **Arr[i] ^ K = 3** ，下一个最小素数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to generate an array whose XOR
// with same-indexed elements of the given
// array is always a prime
void minXOR(vector<int>& Arr, int N)
{
    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If current array element is 2
        if (Arr[i] == 2) {

            // Print its XOR with 3
            cout << (Arr[i] ^ 3) << " ";
        }
        // Otherwise
        else {

            // Print its XOR with 2
            cout << (Arr[i] ^ 2) << " ";
        }
    }
}

// Driver Code
int main()
{
    // Given array
    vector<int> Arr = { 5, 4, 7, 6 };

    // Size of the array
    int N = Arr.size();

    // Prints the required array
    minXOR(Arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to generate an array whose XOR
// with same-indexed elements of the given
// array is always a prime
private static void minXOR(int Arr[], int N)
{

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If current array element is 2
        if (Arr[i] == 2)
        {

            // Print its XOR with 3
            System.out.print((Arr[i] ^ 3) + " ");
        }

        // Otherwise
        else
        {

            // Print its XOR with 2
            System.out.print((Arr[i] ^ 2) + " ");
        }
    }
}

// Driver code
public static void main(String[] args)
{

    // Given array
    int Arr[] = { 5, 4, 7, 6 };

    // Size of the array
    int N = Arr.length;

    // Prints the required array
    minXOR(Arr, N);
}
}

// This code is contributed by MuskanKalra1
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to generate an array whose XOR
# with same-indexed elements of the given
# array is always a prime
def minXOR(Arr, N):

    # Traverse the array
    for i in range(N):

        # If current array element is 2
        if (Arr[i] == 2):

            # Print its XOR with 3
            print(Arr[i] ^ 3,end=" ")
        # Otherwise
        else:

            # Print its XOR with 2
            print(Arr[i] ^ 2,end=" ")

# Driver Code
if __name__ == '__main__':

    # Given array
    Arr = [5, 4, 7, 6 ]

    # Size of the array
    N = len(Arr)

    # Prints the required array
    minXOR(Arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to generate an array whose XOR
// with same-indexed elements of the given
// array is always a prime
private static void minXOR(int[] Arr, int N)
{

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If current array element is 2
        if (Arr[i] == 2)
        {

            // Print its XOR with 3
            Console.Write((Arr[i] ^ 3) + " ");
        }

        // Otherwise
        else
        {

            // Print its XOR with 2
            Console.Write((Arr[i] ^ 2) + " ");
        }
    }
}

// Driver code
public static void Main()
{

    // Given array
    int[] Arr = { 5, 4, 7, 6 };

    // Size of the array
    int N = Arr.Length;

    // Prints the required array
    minXOR(Arr, N);
}
}
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to generate an array whose XOR
// with same-indexed elements of the given
// array is always a prime
function minXOR(Arr, N)
{

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // If current array element is 2
        if (Arr[i] == 2)
        {

            // Print its XOR with 3
            document.write((Arr[i] ^ 3) + " ");
        }

        // Otherwise
        else
        {

            // Print its XOR with 2
            document.write((Arr[i] ^ 2) + " ");
        }
    }
}

// Driver code

    // Given array
    let Arr = [ 5, 4, 7, 6 ];

    // Size of the array
    let N = Arr.length;

    // Prints the required array
    minXOR(Arr, N);

</script>
```

**Output:** 

```
7 6 5 4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)