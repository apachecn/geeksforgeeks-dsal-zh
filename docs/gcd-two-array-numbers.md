# 两个以上(或数组)数的 GCD

> 原文:[https://www.geeksforgeeks.org/gcd-two-array-numbers/](https://www.geeksforgeeks.org/gcd-two-array-numbers/)

给定一个数字数组，求数组元素的 GCD。在之前的帖子中，我们[找到了两个数字](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)的 GCD。
**例:**

```
Input  : arr[] = {1, 2, 3}
Output : 1

Input  : arr[] = {2, 4, 6, 8}
Output : 2
```

三个或三个以上数的 GCD 等于所有数共有的质因数的乘积，但也可以通过重复取数对的 GCD 来计算。

```
gcd(a, b, c) = gcd(a, gcd(b, c)) 
             = gcd(gcd(a, b), c) 
             = gcd(gcd(a, c), b)
```

对于元素数组，我们执行以下操作。我们还将检查结果，如果任何一步的结果变成 1，我们将返回 1 作为 gcd(1，x)=1。

```
result = arr[0]
For i = 1 to n-1
   result = GCD(result, arr[i])
```

以下是上述想法的实现。

## C++

```
// C++ program to find GCD of two or
// more numbers
#include <bits/stdc++.h>
using namespace std;

// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to find gcd of array of
// numbers
int findGCD(int arr[], int n)
{
    int result = arr[0];
    for (int i = 1; i < n; i++)
    {
        result = gcd(arr[i], result);

        if(result == 1)
        {
           return 1;
        }
    }
    return result;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 6, 8, 16 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findGCD(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find GCD of two or
// more numbers

public class GCD {
    // Function to return gcd of a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to find gcd of array of
    // numbers
    static int findGCD(int arr[], int n)
    {
        int result = 0;
        for (int element: arr){
            result = gcd(result, element);

            if(result == 1)
            {
               return 1;
            }
        }

        return result;
    }

    public static void main(String[] args)
    {
        int arr[] = { 2, 4, 6, 8, 16 };
        int n = arr.length;
        System.out.println(findGCD(arr, n));
    }
}

// This code is contributed by Saket Kumar
```

## 计算机编程语言

```
# GCD of more than two (or array) numbers

# Function implements the Euclidian
# algorithm to find H.C.F. of two number
def find_gcd(x, y):

    while(y):
        x, y = y, x % y

    return x

# Driver Code       
l = [2, 4, 6, 8, 16]

num1 = l[0]
num2 = l[1]
gcd = find_gcd(num1, num2)

for i in range(2, len(l)):
    gcd = find_gcd(gcd, l[i])

print(gcd)

# Code contributed by Mohit Gupta_OMG
```

## C#

```
// C# program to find GCD of
// two or more numbers
using System;

public class GCD {

    // Function to return gcd of a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to find gcd of
    // array of numbers
    static int findGCD(int[] arr, int n)
    {
        int result = arr[0];
        for (int i = 1; i < n; i++){
            result = gcd(arr[i], result);

            if(result == 1)
            {
               return 1;
            }
        }

        return result;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 2, 4, 6, 8, 16 };
        int n = arr.Length;
        Console.Write(findGCD(arr, n));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find GCD of two or
// more numbers

// Function to return gcd of a and b
function gcd( $a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Function to find gcd of array of
// numbers
function findGCD($arr, $n)
{
    $result = $arr[0];

    for ($i = 1; $i < $n; $i++){
        $result = gcd($arr[$i], $result);

        if($result == 1)
        {
           return 1;
        }
    }
    return $result;
}

// Driver code
$arr = array( 2, 4, 6, 8, 16 );
$n = sizeof($arr);
echo (findGCD($arr, $n));

// This code is contributed by
// Prasad Kshirsagar.
?>
```

## java 描述语言

```
<script>

// Javascript program to find GCD of two or
// more numbers

// Function to return gcd of a and b
function gcd(a, b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to find gcd of array of
// numbers
function findGCD(arr, n)
{
    let result = arr[0];
    for (let i = 1; i < n; i++)
    {
        result = gcd(arr[i], result);

        if(result == 1)
        {
        return 1;
        }
    }
    return result;
}

// Driver code

    let arr = [ 2, 4, 6, 8, 16 ];
    let n = arr.length;
    document.write(findGCD(arr, n) + "<br>");

// This is code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
2
```

***时间复杂度:** O(N * log(N))，其中 N 是数组中最大的元素*
***辅助空间:** O(1)*

**递归方法:**递归实现算法:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// recursive implementation
int GcdOfArray(vector<int>& arr, int idx)
{
    if (idx == arr.size() - 1) {
        return arr[idx];
    }
    int a = arr[idx];
    int b = GcdOfArray(arr, idx + 1);
    return __gcd(
        a, b); // __gcd(a,b) is inbuilt library function
}

int main()
{
    vector<int> arr = { 1, 2, 3 };
    cout << GcdOfArray(arr, 0) << "\n";

    arr = { 2, 4, 6, 8 };
    cout << GcdOfArray(arr, 0) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
class GFG
{

    // Recursive function to return gcd of a and b 
    static int __gcd(int a, int b) 
    { 
        return b == 0? a:__gcd(b, a % b);    
    }

// recursive implementation
static int GcdOfArray(int[] arr, int idx)
{
    if (idx == arr.length - 1) {
        return arr[idx];
    }
    int a = arr[idx];
    int b = GcdOfArray(arr, idx + 1);
    return __gcd(
        a, b); // __gcd(a,b) is inbuilt library function
}

public static void main(String[] args)
{
   int[] arr = { 1, 2, 3 };
    System.out.print(GcdOfArray(arr, 0)+ "\n");

    int[] arr1 = { 2, 4, 6, 8 };
    System.out.print(GcdOfArray(arr1, 0)+ "\n");
}
}

// This code is contributed by gauravrajput1
```

**Output**

```
1
2
```

**时间复杂度:** O(N * log(N))，其中 N 是数组中最大的元素

**辅助空间** : O(N)

本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。