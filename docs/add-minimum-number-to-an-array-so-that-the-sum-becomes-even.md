# 将最小数加到一个数组中，使和变成偶数

> 原文:[https://www . geeksforgeeks . org/add-最小数对数组，使和变成偶数/](https://www.geeksforgeeks.org/add-minimum-number-to-an-array-so-that-the-sum-becomes-even/)

给定一个数组，编写一个程序将最小数(**应该大于 0** )加到数组中，使数组的和变成偶数。
示例:

```
Input : 1 2 3 4 5 6 7 8
Output : 2
Explanation : Sum of array is 36, so we 
add minimum number 2 to make the sum even.

Input : 1 2 3 4 5 6 7 8 9
Output : 1
```

**方法 1(计算和)。**我们计算数组所有元素的和，然后可以检查和是否为偶数最小数为 2，否则最小数为 1。如果总和超过允许的限制，此方法会导致溢出。
**方法二。**我们不计算数字的和，而是保留数组中奇数元素的**计数。如果奇数计数为偶数，我们返回 2，否则返回 1。
例如–数组包含:1 2 3 4 5 6 7
奇数计数为 4。而且我们知道奇数的偶数的**和是偶数**。偶数的和总是偶数(这就是为什么我们不计算偶数)。** 

## C++

```
// CPP program to add minimum number
// so that the sum of array becomes even
#include <iostream>
using namespace std;

// Function to find out minimum number
int minNum(int arr[], int n)
{
    // Count odd number of terms in array
    int odd = 0;
    for (int i = 0; i < n; i++)
        if (arr[i] % 2)
            odd += 1;

   return (odd % 2)? 1 : 2;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minNum(arr, n) << "n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to add minimum number
// so that the sum of array becomes even

class GFG
{
    // Function to find out minimum number
    static int minNum(int arr[], int n)
    {
        // Count odd number of terms in array
        int odd = 0;
        for (int i = 0; i < n; i++)
            if (arr[i] % 2 != 0)
                odd += 1;

        return ((odd % 2) != 0)? 1 : 2;
    }

    // Driver method to test above function
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
        int n = arr.length;

        System.out.println(minNum(arr, n));
    }
}
```

## 计算机编程语言

```
# Python program to add minimum number
# so that the sum of array becomes even

# Function to find out minimum number
def minNum(arr, n):

    # Count odd number of terms in array
    odd = 0
    for i in range(n):
        if (arr[i] % 2):
            odd += 1

    if (odd % 2):
        return 1
    return 2

# Driver code
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
n = len(arr)
print minNum(arr, n)
```

## C#

```
// C# program to add minimum number
// so that the sum of array becomes even
using System;

class GFG
{
    // Function to find out minimum number
    static int minNum(int []arr, int n)
    {
        // Count odd number of terms in array
        int odd = 0;
        for (int i = 0; i < n; i++)
            if (arr[i] % 2 != 0)
                odd += 1;

        return ((odd % 2) != 0)? 1 : 2;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, 2, 3, 4, 5, 6, 7, 8, 9};
        int n = arr.Length;

        Console.Write(minNum(arr, n));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to add minimum number
// so that the sum of array becomes even

// Function to find out minimum number
function minNum( $arr, $n)
{

    // Count odd number of
    // terms in array
    $odd = 0;
    for ($i = 0; $i < $n; $i++)
        if ($arr[$i] % 2)
            $odd += 1;

    return ($odd % 2)? 1 : 2;
}

    // Driver code
    $arr = array(1, 2, 3, 4, 5,
                 6, 7, 8, 9);
    $n = count($arr);
    echo minNum($arr, $n) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript  program to add minimum number
// so that the sum of array becomes even

    // Function to find out minimum number
    function minNum(arr, n)
    {
        // Count odd number of terms in array
        let odd = 0;
        for (let i = 0; i < n; i++)
            if (arr[i] % 2 != 0)
                odd += 1;

        return ((odd % 2) != 0)? 1 : 2;
    }

// driver program

        let arr = [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ];
        let n = arr.length;

        document.write(minNum(arr, n));

// This code is contributed by code_hunt.
</script>
```

输出:

```
1
```

**方法三。**我们也可以改进 2 方法，我们不需要保持奇数元素存在的计数。我们可以**取一个布尔变量**(初始化为 0)。每当我们**找到数组中的奇数元素时，我们就执行 NOT(！)布尔变量上的操作**。这个逻辑运算符反转布尔变量的值(意味着如果它是 0，它将变量转换为 1，反之亦然)。
例如–数组包含:1 2 3 4 5
解释:变量初始化为 0。
**遍历数组**
1 是奇数，在变量中应用 NOT 运算，现在变量变成 1。
2 为偶数，无操作。
3 为奇数，在变量中应用 NOT 运算，现在变量变为 0。
4 为偶数，无操作。
5 是奇数，在变量中应用 NOT 运算，现在变量变成 1。
如果**变量值为 1，则表示存在奇数个奇数元素**，使元素之和为偶数的最小数量是加 1。
否则最小数量为 2。

## C++

```
// CPP program to add minimum number
// so that the sum of array becomes even

#include <iostream>
using namespace std;

// Function to find out minimum number
int minNum(int arr[], int n)
{
    // Count odd number of terms in array
    bool odd = 0;
    for (int i = 0; i < n; i++)
        if (arr[i] % 2)
            odd = !odd;

    if (odd)
        return 1;
    return 2;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minNum(arr, n) << "n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to add minimum number
// so that the sum of array becomes even

class GFG
{
    // Function to find out minimum number
    static int minNum(int arr[], int n)
    {
        // Count odd number of terms in array
        Boolean odd = false;
        for (int i = 0; i < n; i++)
            if (arr[i] % 2 != 0)
                odd = !odd;

        if (odd)
            return 1;
        return 2;
    }

    //Driver method to test above function
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
        int n = arr.length;

        System.out.println(minNum(arr, n));
    }
}
```

## 计算机编程语言

```
# Python program to add minimum number
# so that the sum of array becomes even

# Function to find out minimum number
def minNum(arr, n):

    # Count odd number of terms in array
    odd = False
    for i in range(n):
        if (arr[i] % 2):
            odd = not odd
    if (odd):
        return 1
    return 2

# Driver code
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
n = len(arr)
print minNum(arr, n)
```

## C#

```
// C# program to add minimum number
// so that the sum of array becomes even
using System;

class GFG
{

    // Function to find out minimum number
    static int minNum(int []arr, int n)
    {
        // Count odd number of terms in array
        bool odd = false;
        for (int i = 0; i < n; i++)
            if (arr[i] % 2 != 0)
                odd = !odd;

        if (odd)
            return 1;
        return 2;
    }

    //Driver Code
    public static void Main()
    {
        int []arr = {1, 2, 3, 4, 5, 6, 7, 8, 9};
        int n = arr.Length;

        Console.Write(minNum(arr, n));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to add minimum number
// so that the sum of array becomes even

// Function to find out minimum number
function minNum($arr, $n)
{

    // Count odd number of
    // terms in array
    $odd = 0;
    for($i = 0; $i < $n; $i++)
        if ($arr[$i] % 2)
            $odd = !$odd;

    if ($odd)
        return 1;
    return 2;
}

    // Driver code
    $arr = array(1, 2, 3, 4, 5, 6, 7, 8, 9);
    $n = sizeof($arr);
    echo minNum($arr, $n) ,"\n";

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
    // Javascript program to add minimum number
    // so that the sum of array becomes even

    // Function to find out minimum number
    function minNum(arr, n)
    {
        // Count odd number of terms in array
        let odd = false;
        for (let i = 0; i < n; i++)
            if (arr[i] % 2 != 0)
                odd = !odd;

        if (odd)
            return 1;
        return 2;
    }

    let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
    let n = arr.length;

    document.write(minNum(arr, n));

 // This code is contributed by divyesh072019.
</script>
```

输出:

```
1
```

**练习:**
求使元素之和为奇数所需的最小数。
本文由 [**沙钦毕斯特**](https://www.linkedin.com/in/sachin-bisht-984b5013a/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。