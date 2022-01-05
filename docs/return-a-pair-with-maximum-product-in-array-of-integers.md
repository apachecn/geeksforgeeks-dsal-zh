# 在整数数组中找到乘积最大的一对

> 原文:[https://www . geesforgeks . org/return-一对整数数组中的最大乘积/](https://www.geeksforgeeks.org/return-a-pair-with-maximum-product-in-array-of-integers/)

给定一个同时包含+ive 和-ive 整数的数组，返回一个乘积最高的对。

**示例:**

```
Input: arr[] = {1, 4, 3, 6, 7, 0}  
Output: {6,7}  

Input: arr[] = {-1, -3, -4, 2, 0, -5} 
Output: {-4,-5}
```

一个**简单的解决方案**就是考虑每一对，跟踪最大乘积。下面是这个简单解决方案的实现。

## C++

```
// A simple C++ program to find max product pair in
// an array of integers
#include<bits/stdc++.h>
using namespace std;

// Function to find maximum product pair in arr[0..n-1]
void maxProduct(int arr[], int n)
{
    if (n < 2)
    {
        cout << "No pairs exists\n";
        return;
    }

    // Initialize max product pair
    int a = arr[0], b = arr[1];

    // Traverse through every possible pair
    // and keep track of max product
    for (int i=0; i<n; i++)
      for (int j=i+1; j<n; j++)
         if (arr[i]*arr[j] > a*b)
            a = arr[i], b = arr[j];

    cout << "Max product pair is {" << a << ", "
         << b << "}";
}

// Driver program to test
int main()
{
    int arr[] = {1, 4, 3, 6, 7, 0};
    int n = sizeof(arr)/sizeof(arr[0]);
    maxProduct(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code to Find a pair with maximum
// product in array of Integers
import java.util.*;

class GFG {

    // Function to find maximum product pair
    // in arr[0..n-1]
    static void maxProduct(int arr[], int n)
    {
        if (n < 2)
        {
            System.out.println("No pairs exists");
            return;
        }

        // Initialize max product pair
        int a = arr[0], b = arr[1];

        // Traverse through every possible pair
        // and keep track of max product
        for (int i = 0; i < n; i++)
          for (int j = i + 1; j < n; j++)
             if (arr[i] * arr[j] > a * b){
                a = arr[i];
                b = arr[j];
             }

        System.out.println("Max product pair is {" +
                           a + ", " + b + "}");
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {1, 4, 3, 6, 7, 0};
        int n = arr.length;
        maxProduct(arr, n);

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# A simple Python3 program to find max
# product pair in an array of integers

# Function to find maximum
# product pair in arr[0..n-1]
def maxProduct(arr, n):

    if (n < 2):
        print("No pairs exists")
        return

    # Initialize max product pair
    a = arr[0]; b = arr[1]

    # Traverse through every possible pair
    # and keep track of max product
    for i in range(0, n):

        for j in range(i + 1, n):
            if (arr[i] * arr[j] > a * b):
                a = arr[i]; b = arr[j]

    print("Max product pair is {", a, ",", b, "}",
                                          sep = "")

# Driver Code
arr = [1, 4, 3, 6, 7, 0]
n = len(arr)
maxProduct(arr, n)

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# Code to Find a pair with maximum
// product in array of Integers
using System;

class GFG
{

    // Function to find maximum
    // product pair in arr[0..n-1]
    static void maxProduct(int []arr, int n)
    {
        if (n < 2)
        {
            Console.Write("No pairs exists");
            return;
        }

        // Initialize max product pair
        int a = arr[0], b = arr[1];

        // Traverse through every possible pair
        // and keep track of max product
        for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            if (arr[i] * arr[j] > a * b)
            {
                a = arr[i];
                b = arr[j];
            }

    Console.Write("Max product pair is {" +
                       a + ", " + b + "}");
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, 4, 3, 6, 7, 0};
        int n = arr.Length;
        maxProduct(arr, n);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP program to
// find max product pair in
// an array of integers

// Function to find maximum
// product pair in arr[0..n-1]
function maxProduct( $arr, $n)
{
    if ($n < 2)
    {
        echo "No pairs exists\n";
        return;
    }

    // Initialize max product pair
    $a = $arr[0];
    $b = $arr[1];

    // Traverse through every possible pair
    // and keep track of max product
    for ($i = 0; $i < $n; $i++)
    for ($j = $i + 1; $j < $n; $j++)
    {
        if ($arr[$i] * $arr[$j] > $a * $b)
        {
            $a = $arr[$i];
            $b = $arr[$j];
        }
    }

    echo "Max product pair is {" , $a , ", ";
    echo $b , "}";
}

    // Driver Code
    $arr = array(1, 4, 3, 6, 7, 0);
    $n = count($arr);
    maxProduct($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// A simple Javascript program to find max product pair in
// an array of integers

// Function to find maximum product pair in arr[0..n-1]
function maxProduct(arr, n)
{
    if (n < 2)
    {
        document.write("No pairs exists" + "<br>");
        return;
    }

    // Initialize max product pair
    let a = arr[0], b = arr[1];

    // Traverse through every possible pair
    // and keep track of max product
    for (let i=0; i<n; i++)
    for (let j=i+1; j<n; j++)
        if (arr[i]*arr[j] > a*b)
            a = arr[i], b = arr[j];

    document.write("Max product pair is {" + a + ", "
        + b + "}");
}

// Driver program to test

    let arr = [1, 4, 3, 6, 7, 0];
    let n = arr.length;
    maxProduct(arr, n);

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
Max product pair is {6, 7}
```

**时间复杂度:** O(n <sup>2</sup>

**更好的方法:**

一个**更好的解决方案**是使用排序。下面是详细的步骤。
1)按升序排列输入数组。
2)如果所有元素都是正数，那么返回最后两个数的乘积。
3)否则最多返回前两个和后两个数字的乘积。

感谢 Rahul Jain 提出这个方法。

## C++14

```
// C++ code to find a pair with maximum
// product in array of Integers
#include<bits/stdc++.h>
using namespace std; 

void maxProduct(vector<int>arr, int n)
{

    // Sort the array
    sort(arr.begin(), arr.end());
    int num1, num2;

    // Calculate product of two smallest numbers
    int sum1 = arr[0] * arr[1];

    // Calculate product of two largest numbers
    int sum2 = arr[n - 1] * arr[n - 2];

    // Print the pairs whose product is greater
    if (sum1 > sum2)
    {
        num1 = arr[0];
        num2 = arr[1];
    }
    else
    {
        num1 = arr[n - 2];
        num2 = arr[n - 1];
    }
    cout << ("Max product pair = ")
         << num1 << "," << num2;
}

// Driver Code
int  main()
{
    vector<int>arr = { 1, 4, 3, 6, 7, 0 };
    int n = arr.size();

    maxProduct(arr, n);
}

// This code is contributed by Stream_Cipher
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code to Find a pair with maximum
// product in array of Integers
import java.util.*;

public class GFG {

    static void maxProduct(int arr[], int n)
    {

        // Sort the array
        Arrays.sort(arr);
        int num1, num2;

          // Calculate product of two smallest numbers
        int sum1 = arr[0] * arr[1];

          // Calculate product of two largest numbers
        int sum2 = arr[n - 1] * arr[n - 2];

          // print the pairs whose product is greater
        if (sum1 > sum2) {
            num1 = arr[0];
            num2 = arr[1];
        }
        else {
            num1 = arr[n - 2];
            num2 = arr[n - 1];
        }
        System.out.println("Max product pair = " +
                           "{" + num1 + "," + num2 + "}");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 4, 3, 6, 7, 0 };
        int n = arr.length;
        maxProduct(arr, n);
    }
}
// Contributed by Navtika Kumar
```

## 蟒蛇 3

```
# Python code to find a pair with maximum
# product in array of Integers
def maxProduct(arr, n):

    # Sort the array
    arr.sort()
    num1 = num2 = 0

    # Calculate product of two smallest numbers
    sum1 = arr[0] * arr[1]

    # Calculate product of two largest numbers
    sum2 = arr[n - 1] * arr[n - 2]

    # Print the pairs whose product is greater
    if (sum1 > sum2):
        num1 = arr[0]
        num2 = arr[1]
    else:
        num1 = arr[n - 2]
        num2 = arr[n - 1]
    print("Max product pair = {", num1, ",", num2, "}", sep="")

# Driver Code
arr = [1, 4, 3, 6, 7, 0]
n = len(arr)

maxProduct(arr, n)

# This code is contributed by subhammahato348.
```

## C#

```
// C# code to Find a pair with maximum
// product in array of Integers
using System;

class GFG{

static void maxProduct(int []arr, int n)
{

    // Sort the array
    Array.Sort(arr);
    int num1, num2;

    // Calculate product of two
    // smallest numbers
    int sum1 = arr[0] * arr[1];

    // Calculate product of two
    // largest numbers
    int sum2 = arr[n - 1] * arr[n - 2];

    // Print the pairs whose
    // product is greater
    if (sum1 > sum2)
    {
        num1 = arr[0];
        num2 = arr[1];
    }
    else
    {
        num1 = arr[n - 2];
        num2 = arr[n - 1];
    }
    Console.Write("Max product pair = " +
                  "{" + num1 + "," + num2 + "}");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 4, 3, 6, 7, 0 };
    int n = arr.Length;

    maxProduct(arr, n);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript code to Find a pair with maximum
// product in array of Integers
function maxProduct(arr, n)
{

    // Sort the array
    arr.sort(function(a, b){return a - b});

    let  num1, num2;

    // Calculate product of two smallest numbers
    let sum1 = arr[0] * arr[1];

    // Calculate product of two largest numbers
    let sum2 = arr[n - 1] * arr[n - 2];

    // print the pairs whose product is greater
    if (sum1 > sum2)
    {
        num1 = arr[0];
        num2 = arr[1];
    }
    else
    {
        num1 = arr[n - 2];
        num2 = arr[n - 1];
    }
    document.write("Max product pair = " +
                 "{" + num1 + "," + num2 + "}");
}

// Driver Code
let arr = [ 1, 4, 3, 6, 7, 0 ];
let n = arr.length;

maxProduct(arr, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
Max product pair = {6,7}
```

**时间复杂度:**O(nlog n)
T3】辅助空间: O(1)

**有效方法:**

一个**有效解**可以在输入数组的单次遍历中解决上述问题。其思想是遍历输入数组并跟踪以下四个值。
a)最大正值
b)第二大正值
c)最大负值，即绝对值最大的负值
d)第二大负值。
循环结束时，比较前两个和后两个的产品，打印两个产品的最大值。下面是这个想法的实现。

## C++

```
// A O(n) C++ program to find maximum product pair in an array
#include<bits/stdc++.h>
using namespace std;

// Function to find maximum product pair in arr[0..n-1]
void maxProduct(int arr[], int n)
{
    if (n < 2)
    {
        cout << "No pairs exists\n";
        return;
    }

    if (n == 2)
    {
        cout << arr[0] << " " << arr[1] << endl;
        return;
    }

    // Initialize maximum and second maximum
    int posa = INT_MIN, posb = INT_MIN;

    // Initialize minimum and second minimum
    int nega = INT_MIN, negb = INT_MIN;

    // Traverse given array
    for (int i = 0; i < n; i++)
    {
        // Update maximum and second maximum if needed
        if (arr[i] > posa)
        {
            posb = posa;
            posa = arr[i];
        }
        else if (arr[i] > posb)
            posb = arr[i];

        // Update minimum and second minimum if needed
        if (arr[i] < 0 && abs(arr[i]) > abs(nega))
        {
            negb = nega;
            nega = arr[i];
        }
        else if(arr[i] < 0 && abs(arr[i]) > abs(negb))
            negb = arr[i];
    }

    if (nega*negb > posa*posb)
        cout << "Max product pair is {" << nega << ", "
             << negb << "}";
    else
        cout << "Max product pair is {" << posa << ", "
             << posb << "}";
}

// Driver program to test above function
int main()
{
    int arr[] = {1, 4, 3, 6, 7, 0};
    int n = sizeof(arr)/sizeof(arr[0]);
    maxProduct(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code to Find a pair with maximum
// product in array of Integers
import java.util.*;

class GFG {

    // Function to find maximum product pair
    // in arr[0..n-1]
    static void maxProduct(int arr[], int n)
    {
        if (n < 2)
        {
            System.out.println("No pairs exists");
            return;
        }

        if (n == 2)
        {
            System.out.println(arr[0] + " " + arr[1]);
            return;
        }

        // Initialize maximum and second maximum
        int posa = Integer.MIN_VALUE,
            posb = Integer.MIN_VALUE;

        // Initialize minimum and second minimum
        int nega = Integer.MIN_VALUE,
            negb = Integer.MIN_VALUE;

        // Traverse given array
        for (int i = 0; i < n; i++)
        {
            // Update maximum and second maximum
            // if needed
            if (arr[i] > posa)
            {
                posb = posa;
                posa = arr[i];
            }
            else if (arr[i] > posb)
                posb = arr[i];

            // Update minimum and second minimum
            // if needed
            if (arr[i] < 0 && Math.abs(arr[i]) >
                       Math.abs(nega))
            {
                negb = nega;
                nega = arr[i];
            }
            else if(arr[i] < 0 && Math.abs(arr[i])
                       > Math.abs(negb))
                negb = arr[i];
        }

        if (nega * negb > posa * posb)
            System.out.println("Max product pair is {"
                          + nega + ", " + negb + "}");
        else
            System.out.println("Max product pair is {"
                          + posa + ", " + posb + "}");
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {1, 4, 3, 6, 7, 0};
        int n = arr.length;
        maxProduct(arr, n);

    }
}

// This code is contributed by Arnav Kr. Mandal.   
```

## 蟒蛇 3

```
# A O(n) Python 3 program to find
# maximum product pair in an array

# Function to find maximum product
# pair in arr[0..n-1]
def maxProduct(arr, n):

    if (n < 2):
        print("No pairs exists")
        return

    if (n == 2):
        print(arr[0] ," " , arr[1])
        return

    # Initialize maximum and
    # second maximum
    posa = 0
    posb = 0

    # Initialize minimum and
    # second minimum
    nega = 0
    negb = 0

    # Traverse given array
    for i in range(n):

        # Update maximum and second
        # maximum if needed
        if (arr[i] > posa):
            posb = posa
            posa = arr[i]

        elif (arr[i] > posb):
            posb = arr[i]

        # Update minimum and second
        # minimum if needed
        if (arr[i] < 0 and abs(arr[i]) > abs(nega)):
            negb = nega
            nega = arr[i]

        elif(arr[i] < 0 and abs(arr[i]) > abs(negb)):
            negb = arr[i]

    if (nega * negb > posa * posb):
        print("Max product pair is {" ,
                nega ,", ", negb , "}")
    else:
        print( "Max product pair is {" ,
                 posa ,", " ,posb , "}")

# Driver Code
if __name__ =="__main__":
    arr = [1, 4, 3, 6, 7, 0]
    n = len(arr)
    maxProduct(arr, n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# Code to Find a pair with maximum
// product in array of Integers
using System;
class GFG {

    // Function to find maximum
    // product pair in arr[0..n-1]
    static void maxProduct(int []arr, int n)
    {
        if (n < 2)
        {
            Console.WriteLine("No pairs exists");
            return;
        }

        if (n == 2)
        {
            Console.WriteLine(arr[0] + " " + arr[1]);
            return;
        }

        // Initialize maximum and
        // second maximum
        int posa = int.MinValue;
        int posb = int.MaxValue;

        // Initialize minimum and
        // second minimum
        int nega = int.MinValue;
        int negb = int.MaxValue;

        // Traverse given array
        for (int i = 0; i < n; i++)
        {

            // Update maximum and
            // second maximum
            // if needed
            if (arr[i] > posa)
            {
                posb = posa;
                posa = arr[i];
            }
            else if (arr[i] > posb)
                posb = arr[i];

            // Update minimum and
            // second minimum if
            // needed
            if (arr[i] < 0 && Math.Abs(arr[i]) >
                              Math.Abs(nega))
            {
                negb = nega;
                nega = arr[i];
            }
            else if(arr[i] < 0 &&
                    Math.Abs(arr[i]) >
                    Math.Abs(negb))
                negb = arr[i];
        }

        if (nega * negb > posa * posb)
            Console.WriteLine("Max product pair is {"
                        + nega + ", " + negb + "}");
        else
            Console.WriteLine("Max product pair is {"
                        + posa + ", " + posb + "}");
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, 4, 3, 6, 7, 0};
        int n = arr.Length;
        maxProduct(arr, n);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A O(n) PHP program to find maximum
// product pair in an array

// Function to find maximum product
// pair in arr[0..n-1]
function maxProduct(&$arr, $n)
{
    if ($n < 2)
    {
        echo("No pairs exists\n");
        return;
    }

    if ($n == 2)
    {
        echo ($arr[0]);
        echo (" ");
        echo($arr[1]);
        echo("\n");
        return;
    }

    // Initialize maximum and
    // second maximum
    $posa = 0;
    $posb = 0;

    // Initialize minimum and
    // second minimum
    $nega = 0;
    $negb = 0;

    // Traverse given array
    for ($i = 0; $i < $n; $i++)
    {
        // Update maximum and second
        // maximum if needed
        if ($arr[$i] > $posa)
        {
            $posb = $posa;
            $posa = $arr[$i];
        }
        else if ($arr[$i] > $posb)
            $posb = $arr[$i];

        // Update minimum and second
        // minimum if needed
        if ($arr[$i] < 0 &&
            abs($arr[$i]) > abs($nega))
        {
            $negb = $nega;
            $nega = $arr[$i];
        }
        else if($arr[$i] < 0 &&
            abs($arr[$i]) > abs($negb))
            $negb = $arr[$i];
    }

    if ($nega * $negb > $posa * $posb)
    {
        echo("Max product pair is {");
        echo $nega;
        echo(", ");
        echo ($negb);
        echo ("}");
    }
    else
    {
        echo("Max product pair is {");
        echo $posa;
        echo(", ");
        echo ($posb);
        echo ("}");
    }
}

// Driver Code
$arr = array(1, 4, 3, 6, 7, 0);
$n = sizeof($arr);
maxProduct($arr, $n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// JAVAscript Code to Find a pair with maximum
// product in array of Integers

    // Function to find maximum product pair
    // in arr[0..n-1]
    function maxProduct(arr,n)
    {
        if (n < 2)
        {
            document.write("No pairs exists");
            return;
        }

        if (n == 2)
        {
            document.write(arr[0] + " " + arr[1]);
            return;
        }

        // Initialize maximum and second maximum
        let posa = Number.MIN_VALUE,
            posb = Number.MIN_VALUE;

        // Initialize minimum and second minimum
        let nega = Number.MIN_VALUE,
            negb = Number.MIN_VALUE;

        // Traverse given array
        for (let i = 0; i < n; i++)
        {
            // Update maximum and second maximum
            // if needed
            if (arr[i] > posa)
            {
                posb = posa;
                posa = arr[i];
            }
            else if (arr[i] > posb)
                posb = arr[i];

            // Update minimum and second minimum
            // if needed
            if (arr[i] < 0 && Math.abs(arr[i]) >
                       Math.abs(nega))
            {
                negb = nega;
                nega = arr[i];
            }
            else if(arr[i] < 0 && Math.abs(arr[i])
                       > Math.abs(negb))
                negb = arr[i];
        }

        if (nega * negb > posa * posb)
            document.write("Max product pair is {"
                          + nega + ", " + negb + "}");
        else
            document.write("Max product pair is {"
                          + posa + ", " + posb + "}");
    }

    /* Driver program to test above function */
    let arr=[1, 4, 3, 6, 7, 0];
    let n = arr.length;
    maxProduct(arr, n);

    //  This code is contributed by rag2127
</script>
```

**输出:**

```
Max product pair is {7, 6}
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

感谢 Gaurav Ahirwar 提出这个方法。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息