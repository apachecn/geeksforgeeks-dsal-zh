# 求数组前半部分和后半部分元素的异或

> 原文:[https://www . geeksforgeeks . org/查找数组的前半部分和后半部分元素的异或运算/](https://www.geeksforgeeks.org/find-the-xor-of-first-half-and-second-half-elements-of-an-array/)

给定一个大小为 **N** 的数组 **arr** 。任务是求一个数组的前半部分( **N/2** )元素和后半部分元素(**N–N/2**)的异或。
**举例:**

> **输入:** arr[]={20，30，50，10，55，15，42}
> **输出:** 56，24
> T6】解释:
> 前半元素 20 ^ 30 ^ 50 是 56
> 后半元素 10 ^ 55 ^ 15 ^ 42 是 24
> **输入:** arr[]={50，45，36

**进场:**

1.  将第一个半异或和第二个半异或初始化为 0。

2.  遍历第一个半异或中的数组和异或元素，直到当前索引小于 N/2。

3.  否则，第二个半异或中的异或元素。

以下是上述方法的实现:

## C++

```
// C++ program to find the xor of
// the first half elements and
// second half elements of an array
#include <iostream>
using namespace std;

// Function to find the xor of
// the first half elements and
// second half elements of an array
void XOROfElements(int arr[], int n){

    int FirstHalfXOR = 0;
    int SecondHalfXOR = 0;

    for(int i=0; i < n; i++){

        // xor of elements in FirstHalfXOR
        if (i < n / 2)
            FirstHalfXOR ^= arr[i];

        // xor of elements in SecondHalfXOR
        else
            SecondHalfXOR ^= arr[i];
    }   
    cout << FirstHalfXOR << "," << SecondHalfXOR << endl;

}

// Driver Code
int main() {
    int arr[] = {20, 30, 50, 10, 55, 15, 42};

    int N = sizeof(arr)/sizeof(arr[0]);

    // Function call
    XOROfElements(arr, N);

    return 0;
}

// This code is contributed by AnkitRai01
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the xor of
// the first half elements and
// second half elements of an array

class GFG{

// Function to find the xor of
// the first half elements and
// second half elements of an array
static void XOROfElements(int arr[], int n){

    int FirstHalfXOR = 0;
    int SecondHalfXOR = 0;

    for(int i = 0; i < n; i++){

        // xor of elements in FirstHalfXOR
        if (i < n / 2)
            FirstHalfXOR ^= arr[i];

        // xor of elements in SecondHalfXOR
        else
            SecondHalfXOR ^= arr[i];
    }
    System.out.print(FirstHalfXOR + ","
                     + SecondHalfXOR + "\n");

}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 20, 30, 50, 10, 55, 15, 42 };

    int N = arr.length;

    // Function call
    XOROfElements(arr, N);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the xor of
# the first half elements and
# second half elements of an array

# Function to find the xor of
# the first half elements and
# second half elements of an array
def XOROfElements(arr, n):

    FirstHalfXOR = 0;
    SecondHalfXOR = 0;

    for i in range(n):

        # xor of elements in FirstHalfXOR
        if (i < n // 2):
            FirstHalfXOR ^= arr[i];

        # xor of elements in SecondHalfXOR
        else:
            SecondHalfXOR  ^= arr[i];

    print(FirstHalfXOR,",",SecondHalfXOR);

# Driver Code
arr = [20, 30, 50, 10, 55, 15, 42];

N = len(arr);

# Function call
XOROfElements(arr, N);
```

## C#

```
// C# program to find the xor of
// the first half elements and
// second half elements of an array
using System;

class GFG{

// Function to find the xor of
// the first half elements and
// second half elements of an array
static void XOROfElements(int []arr, int n)
{
    int FirstHalfXOR = 0;
    int SecondHalfXOR = 0;

    for(int i = 0; i < n; i++)
    {

       // xor of elements in FirstHalfXOR
       if (i < n / 2)
           FirstHalfXOR ^= arr[i];

       // xor of elements in SecondHalfXOR
       else
           SecondHalfXOR ^= arr[i];
    }

    Console.Write(FirstHalfXOR + "," +
                  SecondHalfXOR + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 20, 30, 50, 10, 55, 15, 42 };
    int N = arr.Length;

    // Function call
    XOROfElements(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the xor of
// the first half elements and
// second half elements of an array

    // Function to find the xor of
    // the first half elements and
    // second half elements of an array
    function XOROfElements(arr , n)
    {

        var FirstHalfXOR = 0;
        var SecondHalfXOR = 0;

        for (i = 0; i < n; i++) {

            // xor of elements in FirstHalfXOR
            if (i < parseInt(n / 2))
                FirstHalfXOR ^= arr[i];

            // xor of elements in SecondHalfXOR
            else
                SecondHalfXOR ^= arr[i];
        }
        document.write(
        FirstHalfXOR + ", " + SecondHalfXOR + "\n"
        );

    }

    // Driver Code

        var arr = [ 20, 30, 50, 10, 55, 15, 42 ];

        var N = arr.length;

        // Function call
        XOROfElements(arr, N);

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
56, 24
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)