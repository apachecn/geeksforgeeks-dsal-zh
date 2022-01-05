# 在代码的任何地方不使用减号“-”来反转数组

> 原文:[https://www . geesforgeks . org/reverse-array-not-use-减法-sign-anywhere-code/](https://www.geeksforgeeks.org/reverse-array-without-using-subtract-sign-anywhere-code/)

给定一个数组，任务是[反转数组](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)，而不在代码中的任何地方使用减号“-”。反转数组并不难，但最主要的是不要使用“-”运算符。

问于:[月蛙访谈](https://www.geeksforgeeks.org/moonfrog-labs-interview-experience-set-4/)
下面是不同的方法:
**方法 1:**
1-在 C++ 中将数组元素存储成[向量。
2-然后使用预定义的函数反转矢量。
3-然后将反转的元素存储到数组中。
**方法 2:**
1-将数组元素存储到](https://www.geeksforgeeks.org/vector-sequence-containers-the-c-standard-template-library-stl-set-1/)[堆栈](https://www.geeksforgeeks.org/stack-container-adaptors-the-c-standard-template-library-stl/)中。
2-由于堆栈遵循后进先出，因此我们可以将堆栈顶部的元素存储到数组中，该数组本身将以相反的方式存在。
**方法 3:**
1-在这种方法中，想法是使用负号，但将其存储到变量中。
2-通过使用这个语句 x = (INT_MIN/INT_MAX)，我们在变量 x 中得到-1。
3-由于 INT_MIN 和 INT_MAX 具有相同的值，只是符号相反，所以在划分它们时，它将给出-1。
4-那么“x”可以用于从最后一个开始递减索引。

## C++

```
// C++ program to reverse an array without
// using "-" sign
#include <bits/stdc++.h>
using namespace std;

// Function to reverse array
void reverseArray(int arr[], int n)
{
    // Trick to assign -1 to a variable
    int x = (INT_MIN / INT_MAX);

    // Reverse array in simple manner
    for (int i = 0; i < n / 2; i++)

        // Swap ith index value with (n-i-1)th
        // index value
        swap(arr[i], arr[n + (x * i) + x]);
}

// Drivers code
int main()
{
    int arr[] = { 5, 3, 7, 2, 1, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    reverseArray(arr, n);

    // print the reversed array
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse an array without
// using "-" sign
class GFG {

    // Function to reverse array
    static void reverseArray(int arr[], int n)
    {
        // Trick to assign -1 to a variable
        int x = (Integer.MIN_VALUE / Integer.MAX_VALUE);

        // Reverse array in simple manner
        for (int i = 0; i < n / 2; i++)

            // Swap ith index value with (n-i-1)th
            // index value
            swap(arr, i, n + (x * i) + x);
    }
    static int[] swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Drivers code
    public static void main(String[] args)
    {
        int arr[] = { 5, 3, 7, 2, 1, 6 };
        int n = arr.length;

        reverseArray(arr, n);

        // print the reversed array
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to reverse an array without
# using "-" sign

# Function to reverse array
def reverseArray(arr, n):

    import sys

    # Trick to assign - 1 to a variable
    x = -sys.maxsize // sys.maxsize

    # Reverse array in simple manner
    for i in range(n//2):

        # Swap ith index value with (n-i-1)th
        # index value
        arr[i], arr[n + (x*i) + x] = arr[n + (x*i) + x], arr[i]

# Driver code
if __name__ == "__main__":
    arr = [5, 3, 7, 2, 1, 6]
    n = len(arr)

    reverseArray(arr, n)

    # print the reversed array
    for i in range(n):
        print(arr[i], end=" ")

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to reverse an array without
// using "-" sign
using System;

class GFG {

    // Function to reverse array
    static void reverseArray(int[] arr, int n)
    {
        // Trick to assign -1 to a variable
        int x = (int.MinValue / int.MaxValue);

        // Reverse array in simple manner
        for (int i = 0; i < n / 2; i++)

            // Swap ith index value with (n-i-1)th
            // index value
            swap(arr, i, n + (x * i) + x);
    }

    static int[] swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Drivers code
    public static void Main()
    {
        int[] arr = { 5, 3, 7, 2, 1, 6 };
        int n = arr.Length;

        reverseArray(arr, n);

        // print the reversed array
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?PHP
// PHP program to reverse an array without
// using "-" sign

// Function to reverse array
function reverseArray(&$arr, $n)
{
    // Trick to assign -1 to a variable
    $x = (PHP_INT_MIN / PHP_INT_MAX);

    // Reverse array in simple manner
    for ($i = 0; $i < $n / 2; $i++)

        // Swap ith index value with (n-i-1)th
        // index value
        swap($arr, $i, $n + ($x * $i) + $x);
}

function swap(&$arr, $i, $j)
{
    $temp = $arr[$i];
    $arr[$i] = $arr[$j];
    $arr[$j] = $temp;
    return $arr;
}

// Drivers code
$arr = array( 5, 3, 7, 2, 1, 6 );
$n = sizeof($arr);

reverseArray($arr, $n);

// print the reversed array
for ($i = 0; $i < $n; $i++)
    echo($arr[$i] . " ");

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
    //javascript program to reverse an array without
    // using "-" sign

    // Function to reverse array
    function reversearray(arr,n)
    {
        // Trick to assign -1 to a variable
        let x = parseInt(-2147483648 / 2147483647, 10);

        // Reverse array in simple manner
        for (let i = 0; i < parseInt(n / 2, 10); i++)
        {

            // Swap ith index value with (n-i-1)th
            // index value
            let temp = arr[i];
            arr[i] = arr[n + (x * i) + x];
            arr[n + (x * i) + x] = temp;
        }
    }

    let arr = [ 5, 3, 7, 2, 1, 6 ];
    let n = arr.length;

    reversearray(arr, n);

    // print the reversed array
    for (let i = 0; i < n; i++)
        document.write(arr[i] +" ");

// This code is contributed by vaibhavrabadiya117.
</script>
```

**输出:**

```
6 1 2 7 3 5
```

**方法 4:**
在这个方法 4 中，思路是用按位运算符实现减法即
A–B = A+~ b+ 1
所以，I–可以写成 i = i +~1 +1

## C++

```
// C++ program to reverse an array without
// using "-" sign
#include <bits/stdc++.h>
using namespace std;

// Function to reverse array
void reverseArray(int arr[], int n)
{

    // Reverse array in simple manner
    for (int i = 0; i < n / 2; i++)

        // Swap ith index value with (n-i-1)th
        // index value
        // Note : A - B = A + ~B + 1
        // So n - i = n + ~i + 1 then
        // n - i - 1 = (n + ~i + 1) + ~1 + 1
        swap(arr[i], arr[(n + ~i + 1) + ~1 + 1]);
}

// Driver code
int main()
{
    int arr[] = { 5, 3, 7, 2, 1, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    reverseArray(arr, n);

    // print the reversed array
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse an array without
// using "-" sign
import java.util.Arrays;

class GFG {

    // Function to reverse array
    static void reverseArray(int arr[], int n)
    {

        // Reverse array in simple manner
        for (int i = 0; i < n / 2; i++)

        // Swap ith index value with (n-i-1)th
        // index value
        // Note : A - B = A + ~B + 1
        // So n - i = n + ~i + 1 then
        // n - i - 1 = (n + ~i + 1) + ~1 + 1
        {
            swap(arr, i, (n + ~i + 1) + ~1 + 1);
        }
    }

    static int[] swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 5, 3, 7, 2, 1, 6 };
        int n = arr.length;

        reverseArray(arr, n);

        // print the reversed array
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to reverse an array without
# using "-" sign

# Function to reverse array
def reverseArray(arr, n):

    # Reverse array in simple manner
    for i in range(n//2):

        # Swap ith index value with (n-i-1)th
        # index value
        # Note : A - B = A + ~B + 1
        # So n - i = n + ~i + 1 then
        # n - i - 1 = (n + ~i + 1) + ~1 + 1
        arr[i], arr[(n + ~i + 1) + ~1 + 1] = arr[(n + ~i + 1) + ~1 + 1],arr[i]

# Driver code

arr = [ 5, 3, 7, 2, 1, 6 ]
n = len(arr)

reverseArray(arr, n)

# print the reversed array
for i in range(n):
    print(arr[i],end=" ")

# This code is contributed by ankush_953
```

## C#

```
// C# program to reverse an array without
// using "-" sign
using System;

class GFG {

    // Function to reverse array
    static void reverseArray(int[] arr, int n)
    {

        // Reverse array in simple manner
        for (int i = 0; i < n / 2; i++)

        // Swap ith index value with (n-i-1)th
        // index value
        // Note : A - B = A + ~B + 1
        // So n - i = n + ~i + 1 then
        // n - i - 1 = (n + ~i + 1) + ~1 + 1
        {
            swap(arr, i, (n + ~i + 1) + ~1 + 1);
        }
    }

    static int[] swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 5, 3, 7, 2, 1, 6 };
        int n = arr.Length;

        reverseArray(arr, n);

        // print the reversed array
        for (int i = 0; i < n; i++) {
            Console.Write(arr[i] + " ");
        }
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?PHP
    // PHP program to reverse an array without
    // using "-" sign

    // Function to reverse array
    function reverseArray(&$arr, $n)
    {

        // Reverse array in simple manner
        for ($i = 0; $i < $n / 2; $i++)

        // Swap ith index value with (n-i-1)th
        // index value
        // Note : A - B = A + ~B + 1
        // So n - i = n + ~i + 1 then
        // n - i - 1 = (n + ~i + 1) + 1 + 1
        {
            swap($arr, $i, ($n + ~$i + 1) + ~1 + 1);
        }
    }

    function swap(&$arr, $i, $j)
    {
        $temp = $arr[$i];
        $arr[$i] = $arr[$j];
        $arr[$j] = $temp;
        return $arr;
    }

    // Driver code
    {
        $arr = array( 5, 3, 7, 2, 1, 6 );
        $n = sizeof($arr);

        reverseArray($arr, $n);

        // print the reversed array
        for ($i = 0; $i < $n; $i++)
        {
            echo($arr[$i] . " ");
        }
    }

// This code contributed by Code_Mech
```

## java 描述语言

```
<script>
    // Javascript program to reverse an array without using "-" sign

    // Function to reverse array
    function reverseArray(arr, n)
    {

        // Reverse array in simple manner
        for (let i = 0; i < parseInt(n / 2, 10); i++)

        // Swap ith index value with (n-i-1)th
        // index value
        // Note : A - B = A + ~B + 1
        // So n - i = n + ~i + 1 then
        // n - i - 1 = (n + ~i + 1) + ~1 + 1
        {
            swap(arr, i, (n + ~i + 1) + ~1 + 1);
        }
    }

    function swap(arr, i, j)
    {
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    let arr = [ 5, 3, 7, 2, 1, 6 ];
    let n = arr.length;

    reverseArray(arr, n);

    // print the reversed array
    for (let i = 0; i < n; i++) {
      document.write(arr[i] + " ");
    }

 // This code is contributed by mukesh07.
</script>
```

**输出:**

```
6 1 2 7 3 5
```

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。