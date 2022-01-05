# 计算给定数组中元素总和的程序

> 原文:[https://www . geesforgeks . org/program-find-sum-elements-given-array/](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

给定一个整数数组，求其元素的和。
**例:**

```
Input : arr[] = {1, 2, 3}
Output : 6
1 + 2 + 3 = 6

Input : arr[] = {15, 12, 13, 10}
Output : 50
```

## C++

```
/* C++ Program to find sum of elements
in a given array */
#include <bits/stdc++.h>
using namespace std;

// function to return sum of elements
// in an array of size n
int sum(int arr[], int n)
{
    int sum = 0; // initialize sum

    // Iterate through all elements
    // and add them to sum
    for (int i = 0; i < n; i++)
    sum += arr[i];

    return sum;
}

// Driver code
int main()
{
    int arr[] = {12, 3, 4, 15};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Sum of given array is " << sum(arr, n);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
/* C Program to find sum of elements
 in a given array */
#include <bits/stdc++.h>

// function to return sum of elements
// in an array of size n
int sum(int arr[], int n)
{
    int sum = 0; // initialize sum

    // Iterate through all elements
    // and add them to sum
    for (int i = 0; i < n; i++)
    sum += arr[i];

    return sum;
}

int main()
{
    int arr[] = {12, 3, 4, 15};
    int n = sizeof(arr) / sizeof(arr[0]);
    printf("Sum of given array is %d", sum(arr, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java Program to find sum of elements in a given array  */
class Test
{
     static int arr[] = {12,3,4,15};

     // method for sum of elements in an array
     static int sum()
     {
         int sum = 0; // initialize sum
         int i;

         // Iterate through all elements and add them to sum
         for (i = 0; i < arr.length; i++)
            sum +=  arr[i];

         return sum;
     }

     // Driver method
     public static void main(String[] args)
     {
         System.out.println("Sum of given array is " + sum());
        }
 }
```

## 蟒蛇 3

```
# Python 3 code to find sum
# of elements in given array
def _sum(arr,n):

    # return sum using sum
    # inbuilt sum() function
    return(sum(arr))

# driver function
arr=[]
# input values to list
arr = [12, 3, 4, 15]

# calculating length of array
n = len(arr)

ans = _sum(arr,n)

# display sum
print ('Sum of the array is ',ans)

# This code is contributed by Himanshu Ranjan
```

## C#

```
// C# Program to find sum of elements in a
// given array
using System;

class GFG {

    // method for sum of elements in an array
    static int sum(int []arr, int n)
    {

        int sum = 0; // initialize sum

        // Iterate through all elements and
        // add them to sum
        for (int i = 0; i < n; i++)
            sum += arr[i];

        return sum;
    }

    // Driver method
    public static void Main()
    {

        int []arr = {12,3,4,15};
        int n = arr.Length;

        Console.Write("Sum of given array is "
                               + sum(arr, n));
    }

}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum of
// elements in a given array

// function to return sum
// of elements in an array
// of size n
function sum( $arr, $n)
{
    // initialize sum
    $sum = 0;

    // Iterate through all elements
    // and add them to sum
    for ($i = 0; $i < $n; $i++)
    $sum += $arr[$i];

    return $sum;
}

// Driver Code
$arr =array(12, 3, 4, 15);
$n = sizeof($arr);
echo "Sum of given array is ",
                sum($arr, $n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
//JavaScript Program to find
//sum of elements in a given array

    // function to return sum of elements 
    // in an array of size n 
    function sum(arr) { 
        let sum = 0; // initialize sum 

        // Iterate through all elements 
        // and add them to sum 
        for (let i = 0; i < arr.length; i++) 
            sum += arr[i]; 

        return sum; 
    } 

    // Driver code
    let arr = [12, 3, 4, 15];
    document.write("Sum of given array is " + sum(arr));

 // This code is contributed by Surbhi Tyagi 
</script>
```

**输出:**

```
Sum of given array is 34
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

**另一种方法:**使用 STL
调用 STL 中数组元素和的内置函数。
*累加(第一、最后、总和)；*
*第一个、最后一个:要添加元素的范围*
*的第一个和最后一个元素*
*总和:总和的初始值*

***该函数返回数组的和。**T3】*

## C++

```
/* C++ Program to find sum of elements
in a given array */
#include <bits/stdc++.h>
using namespace std;

// Driver code
int main()
{
    int arr[] = {12, 3, 4, 15};
    int n = sizeof(arr) / sizeof(arr[0]);
      // calling accumulate function, passing first, last element and
    // initial sum, which is 0 in this case.
    cout << "Sum of given array is " << accumulate(arr, arr + n, 0);
    return 0;
}

// This code is contributed by pranoy_coder
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java Program to find sum of elements
in a given array */
import java.util.*;

class GFG{

    static int accumulate(int []arr)
        {
            int sum = 0;
            for(int i = 0; i < arr.length; i++)
            {
                sum = sum + arr[i];
            }
            return sum;
        }

// Driver code
public static void main(String[] args)
{
    int arr[] = {12, 3, 4, 15};
    int n = arr.length;

      // calling accumulate function, passing first, last element and
    // initial sum, which is 0 in this case.
    System.out.print("Sum of given array is " +  accumulate(arr));
}
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# Python3 program to find sum of elements
# in a given array

# Driver code
if __name__ == "__main__":

    arr = [ 12, 3, 4, 15 ]
    n = len(arr)

    # Calling accumulate function, passing
    # first, last element and initial sum,
    # which is 0 in this case.
    print("Sum of given array is ", sum(arr));

# This code is contributed by ukasp
```

## C#

```
/* C# Program to find sum of elements
in a given array */
using System;
public class GFG {

    static int accumulate(int[] arr) {
        int sum = 0;
        for (int i = 0; i < arr.Length; i++) {
            sum = sum + arr[i];
        }
        return sum;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 12, 3, 4, 15 };
        int n = arr.Length;

        // calling accumulate function, passing first, last element and
        // initial sum, which is 0 in this case.
        Console.Write("Sum of given array is " + accumulate(arr));
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
     /* javascript Program to find sum of elements
    in a given array */

    function accumulate(arr)
    {
        let sum = 0;
        for(let i = 0; i < arr.length; i++)
        {
            sum = sum + arr[i];
        }
        return sum;
    }

    // Driver code

    let arr = [12, 3, 4, 15];
    let n = arr.length;

    // calling accumulate function, passing first, last element and
    // initial sum, which is 0 in this case
    document.write("Sum of given array is " + accumulate(arr));

    // This code is contributed by vaibhavrabadiya3.
</script>
```

**Output**

```
Sum of given array is 34
```