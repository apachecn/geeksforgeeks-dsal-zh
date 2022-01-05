# 奇数和的子阵列数量

> 原文:[https://www . geeksforgeeks . org/带奇数和的子阵数量/](https://www.geeksforgeeks.org/number-of-subarrays-with-odd-sum/)

给定一个数组，求其和为奇数的子数组的个数。

**示例:**

```
Input : arr[] = {5, 4, 4, 5, 1, 3} 
Output : 12

There are possible subarrays with odd
sum. The subarrays are 
1) {5} Sum = 5 (At index 0)
2) {5, 4}  Sum = 9
3) {5, 4, 4}  Sum = 13 
4) {5, 4, 4, 5, 1} Sum = 19
5) {4, 4, 5}  Sum = 13
6) {4, 4, 5, 1, 3}  Sum = 17
7) {4, 5}  Sum = 9 
8) {4, 5, 1, 3} Sum = 13
9) {5}  Sum = 5 (At index 3)
10) {5, 1, 3}  Sum = 9
11)  {1} Sum = 1
12) {3} Sum = 3
```

**O(n <sup>2</sup> )时间和 O(1)空间方法【蛮力】**
我们可以简单地生成所有可能的子数组，并找出其中所有元素的和是否为奇数。如果它是奇数，那么我们将计算该子阵列，否则忽略它。

## C++

```
// C++ code to find count of sub-arrays
// with odd sum
#include <bits/stdc++.h>
using namespace std;

int countOddSum(int ar[], int n)
{
    int result = 0;

    // Find sum of all subarrays and increment
    // result if sum is odd
    for (int i = 0; i <= n - 1; i++) {
        int val = 0;
        for (int j = i; j <= n - 1; j++) {
            val = val + ar[j];
            if (val % 2 != 0)
                result++;
        }
    }

    return (result);
}

// Driver code
int main()
{
    int ar[] = { 5, 4, 4, 5, 1, 3 };
    int n = sizeof(ar) / sizeof(ar[0]);

    cout << "The Number of Subarrays with odd"
            " sum is "
         << countOddSum(ar, n);

    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find count of sub-arrays
// with odd sum
import java.io.*;

class GFG {
    static int countOddSum(int ar[],
                           int n)
    {
        int result = 0;

        // Find sum of all subarrays
        // and increment result if
        // sum is odd
        for (int i = 0; i <= n - 1; i++) {
            int val = 0;
            for (int j = i; j <= n - 1; j++) {
                val = val + ar[j];
                if (val % 2 != 0)
                    result++;
            }
        }

        return (result);
    }

    // Driver code
    public static void main(String[] args)
    {
        int ar[] = { 5, 4, 4, 5, 1, 3 };
        int n = ar.length;

        System.out.print("The Number of Subarrays"
                         + " with odd sum is ");

        System.out.println(countOddSum(ar, n));
    }
}
```

## 蟒蛇 3

```
# Python 3 code to find count
# of sub-arrays with odd sum

def countOddSum(ar, n):
    result = 0

    # Find sum of all subarrays and
    # increment result if sum is odd
    for i in range(n):
        val = 0
        for j in range(i, n ):
            val = val + ar[j]
            if (val % 2 != 0):
                result +=1

    return (result)

# Driver code
ar = [ 5, 4, 4, 5, 1, 3 ]

print("The Number of Subarrays" ,
            "with odd", end = "")

print(" sum is "+ str(countOddSum(ar, 6)))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# code to find count
// of sub-arrays with odd sum
using System;

class GFG
{
static int countOddSum(int []ar,
                       int n)
{
    int result = 0;

    // Find sum of all subarrays
    // and increment result if
    // sum is odd
    for (int i = 0;
             i <= n - 1; i++)
    {
        int val = 0;
        for (int j = i;
                 j <= n - 1; j++)
        {
            val = val + ar[j];
            if (val % 2 != 0)
                result++;
        }
    }

    return (result);
}

// Driver code
public static void Main()
{
    int []ar = {5, 4, 4, 5, 1, 3};
    int n = ar.Length;

    Console.Write("The Number of Subarrays" +
                        " with odd sum is ");

    Console.WriteLine(countOddSum(ar, n));
}
}

// This code is contributed
// by chandan_jnu.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find count
// of sub-arrays with odd sum

function countOddSum(&$ar, $n)
{
    $result = 0;

    // Find sum of all subarrays and
    // increment result if sum is odd
    for ($i = 0; $i <= $n - 1; $i++)
    {
        $val = 0;
        for ($j = $i;
             $j <= $n - 1; $j++)
        {
            $val = $val + $ar[$j];
            if ($val % 2 != 0)
                $result++;
        }
    }

    return ($result);
}

// Driver code
$ar = array(5, 4, 4, 5, 1, 3);
$n = sizeof($ar);

echo "The Number of Subarrays with odd ";
echo "sum is ".countOddSum($ar, $n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript code to find count of
// sub-arrays with odd sum
function countOddSum(ar, n)
{
    let result = 0;

    // Find sum of all subarrays
    // and increment result if
    // sum is odd
    for(let i = 0; i <= n - 1; i++)
    {
        let val = 0;
        for(let j = i; j <= n - 1; j++)
        {
            val = val + ar[j];

            if (val % 2 != 0)
                result++;
        }
    }
    return (result);
}

// Driver code
let ar = [ 5, 4, 4, 5, 1, 3 ];
let n = ar.length;
document.write("The Number of Subarrays" +
               " with odd sum is ");

document.write(countOddSum(ar, n));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
The Number of Subarrays with odd sum is 12
```

**O(n)时间和 O(1)空间方法【高效】**
如果我们确实计算了输入数组 temp[]中的累积和数组，那么我们可以看到从 I 开始到 j 结束的子数组，如果 temp[]If(temp[j]–temp[I])% 2 = 0，则有一个偶和。因此，我们不是构建一个累积和数组，而是构建一个累积和模 2 数组。然后计算奇偶对将得到所需的结果，即 temp[0]*temp[1]。

## C++

```
// C++ program to find count of sub-arrays
// with odd sum
#include <bits/stdc++.h>
using namespace std;

int countOddSum(int ar[], int n)
{
    // A temporary array of size 2\. temp[0] is
    // going to store count of even subarrays
    // and temp[1] count of odd.
    // temp[0] is initialized as 1 because there
    // a single odd element is also counted as
    // a subarray
    int temp[2] = { 1, 0 };

    // Initialize count. sum is sum of elements
    // under modulo 2 and ending with arr[i].
    int result = 0, val = 0;

    // i'th iteration computes sum of arr[0..i]
    // under modulo 2 and increments even/odd count
    // according to sum's value
    for (int i = 0; i <= n - 1; i++) {
        // 2 is added to handle negative numbers
        val = ((val + ar[i]) % 2 + 2) % 2;

        // Increment even/odd count
        temp[val]++;
    }

    // An odd can be formed by even-odd pair
    result = (temp[0] * temp[1]);

    return (result);
}

// Driver code
int main()
{
    int ar[] = { 5, 4, 4, 5, 1, 3 };
    int n = sizeof(ar) / sizeof(ar[0]);

    cout << "The Number of Subarrays with odd"
            " sum is "
         << countOddSum(ar, n);

    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find count of sub-arrays
// with odd sum
import java.io.*;

class GFG {
    static int countOddSum(int ar[],
                           int n)
    {
        // A temporary array of size 2.
        // temp[0] is going to store
        // count of even subarrays
        // and temp[1] count of odd.
        // temp[0] is initialized as
        // 1 because there a single odd
        // element is also counted as
        // a subarray
        int temp[] = { 1, 0 };

        // Initialize count. sum is
        // sum of elements under modulo
        // 2 and ending with arr[i].
        int result = 0, val = 0;

        // i'th iteration computes sum
        // of arr[0..i] under modulo 2
        // and increments even/odd count
        // according to sum's value
        for (int i = 0; i <= n - 1; i++) {
            // 2 is added to handle
            // negative numbers
            val = ((val + ar[i]) % 2 + 2) % 2;

            // Increment even/odd count
            temp[val]++;
        }

        // An odd can be formed by an even-odd pair
        result = temp[0] * temp[1];

        return (result);
    }

    // Driver code
    public static void main(String[] args)
    {

        int ar[] = { 5, 4, 4, 5, 1, 3 };
        int n = ar.length;

        System.out.println("The Number of Subarrays"
                           + " with odd sum is " + countOddSum(ar, n));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to 
# find count of sub-arrays
# with odd sum
def countOddSum(ar, n):

    # A temporary array of size
    # 2\. temp[0] is going to
    # store count of even subarrays
    # and temp[1] count of odd.
    # temp[0] is initialized as 1
    # because there is a single odd
    # element is also counted as
    # a subarray
    temp = [ 1, 0 ]

    # Initialize count. sum is sum
    # of elements under modulo 2
    # and ending with arr[i].
    result = 0
    val = 0

    # i'th iteration computes
    # sum of arr[0..i] under
    # modulo 2 and increments
    # even/odd count according
    # to sum's value
    for i in range(n):

        # 2 is added to handle
        # negative numbers
        val = ((val + ar[i]) % 2 + 2) % 2

        # Increment even/odd count
        temp[val] += 1

    # An odd can be formed
    # by even-odd pair
    result = (temp[0] * temp[1])

    return (result)

# Driver code
ar = [ 5, 4, 4, 5, 1, 3 ]

print("The Number of Subarrays"
           " with odd sum is "+
       str(countOddSum(ar, 6)))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# code to find count of
// sub-arrays with odd sum
using System;

class GFG
{
static int countOddSum(int[] ar,
                       int n)
{
    // A temporary array of size 2.
    // temp[0] is going to store
    // count of even subarrays
    // and temp[1] count of odd.
    // temp[0] is initialized as
    // 1 because there a single odd
    // element is also counted as
    // a subarray
    int[] temp = { 1, 0 };

    // Initialize count. sum is
    // sum of elements under modulo
    // 2 and ending with arr[i].
    int result = 0, val = 0;

    // i'th iteration computes sum
    // of arr[0..i] under modulo 2
    // and increments even/odd count
    // according to sum's value
    for (int i = 0; i <= n - 1; i++)
    {
        // 2 is added to handle
        // negative numbers
        val = ((val + ar[i]) % 2 + 2) % 2;

        // Increment even/odd count
        temp[val]++;
    }

    // An odd can be formed
    // by an even-odd pair
    result = temp[0] * temp[1];

    return (result);
}

// Driver code
public static void Main()
{

    int[] ar = { 5, 4, 4, 5, 1, 3 };
    int n = ar.Length;

    Console.Write("The Number of Subarrays" +
                        " with odd sum is " +
                         countOddSum(ar, n));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find count
// of sub-arrays with odd sum

function countOddSum($ar, $n)
{
    // A temporary array of size
    // 2\. temp[0] is going to
    // store count of even subarrays
    // and temp[1] count of odd.
    // temp[0] is initialized as 1
    // because there is a single odd
    // element is also counted as
    // a subarray
    $temp = array(1, 0);

    // Initialize count. sum is
    // sum of elements under
    // modulo 2 and ending with arr[i].
    $result = 0;
    $val = 0;

    // i'th iteration computes sum
    // of arr[0..i] under modulo 2
    // and increments even/odd count
    // according to sum's value
    for ($i = 0; $i <= $n - 1; $i++)
    {
        // 2 is added to handle
        // negative numbers
        $val = (($val + $ar[$i]) %
                       2 + 2) % 2;

        // Increment even/odd count
        $temp[$val]++;
    }

    // An odd can be formed
    // by even-odd pair
    $result = ($temp[0] * $temp[1]);

    return ($result);
}

// Driver code
$ar = array(5, 4, 4, 5, 1, 3);
$n = sizeof($ar);

echo "The Number of Subarrays with odd".
        " sum is ".countOddSum($ar, $n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript code to find count of
// sub-arrays with odd sum
function countOddSum(ar, n)
{

    // A temporary array of size 2.
    // temp[0] is going to store
    // count of even subarrays
    // and temp[1] count of odd.
    // temp[0] is initialized as
    // 1 because there a single odd
    // element is also counted as
    // a subarray
    let temp = [1, 0];

    // Initialize count. sum is
    // sum of elements under modulo
    // 2 and ending with arr[i].
    let result = 0, val = 0;

    // i'th iteration computes sum
    // of arr[0..i] under modulo 2
    // and increments even/odd count
    // according to sum's value
    for(let i = 0; i <= n - 1; i++)
    {

        // 2 is added to handle
        // negative numbers
        val = ((val + ar[i]) % 2 + 2) % 2;

        // Increment even/odd count
        temp[val]++;
    }

    // An odd can be formed
    // by an even-odd pair
    result = temp[0] * temp[1];

    return (result);
}

// Driver code
let ar = [ 5, 4, 4, 5, 1, 3 ];
let n = ar.length;

document.write("The Number of Subarrays" +
               " with odd sum is " +
               countOddSum(ar, n));

// This code is contributed by rameshtravel07  

</script>
```

**输出:**

```
The Number of Subarrays with odd sum is 12
```

另一种有效的方法是首先找到从索引 0 开始并且具有奇数和的子阵列的数量。然后遍历数组并更新从索引 I 开始且具有奇数和的子数组的数量。

下面是上述方法的实现:

## C++

```
// C++ program to find number of subarrays with odd sum
#include <bits/stdc++.h>
using namespace std;

// Function to find number of subarrays with odd sum
int countOddSum(int a[], int n)
{
    // 'odd' stores number of odd numbers upto ith index
    // 'c_odd' stores number of odd sum subarrays starting at ith index
    // 'Result' stores the number of odd sum subarrays
    int odd = 0, c_odd=0, result = 0;

    // First find number of odd sum subarrays starting at 0th index
    for(int i=0;i <n;i++) {
        if(a[i]&1) {
            odd = !odd;
        }
        if(odd) {
            c_odd++;
        }
    }

    // Find number of odd sum subarrays starting at ith index
    // add to result
    for(int i=0; i<n; i++) {
        result += c_odd;
        if(a[i]&1) {
            c_odd = (n-i-c_odd);
        }
    }

    return result;
}

// Driver code
int main()
{
    int ar[] = { 5, 4, 4, 5, 1, 3 };
    int n = sizeof(ar) / sizeof(ar[0]);

    cout << "The Number of Subarrays with odd sum is "
        << countOddSum(ar, n);

    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of subarrays
// with odd sum
import java.util.*;

class GFG{

// Function to find number of
// subarrays with odd sum
static int countOddSum(int a[], int n)
{

    // 'odd' stores number of odd numbers
    // upto ith index
    // 'c_odd' stores number of odd sum
    // subarrays starting at ith index
    // 'Result' stores the number of
    // odd sum subarrays
    int  c_odd = 0, result = 0;
    boolean odd = false;

    // First find number of odd sum
    // subarrays starting at 0th index
    for(int i = 0; i < n; i++)
    {
        if (a[i] % 2 == 1)
        {
            odd = !odd;
        }
        if (odd)
        {
            c_odd++;
        }
    }

    // Find number of odd sum subarrays
    // starting at ith index add to result
    for(int i = 0; i < n; i++)
    {
        result += c_odd;
        if (a[i] % 2 == 1)
        {
            c_odd = (n - i - c_odd);
        }
    }
    return result;
}

// Driver code
public static void main(String[] args)
{
    int ar[] = { 5, 4, 4, 5, 1, 3 };
    int n = ar.length;

    System.out.print("The Number of Subarrays " +
                     "with odd sum is " +
                     countOddSum(ar, n));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to find
# number of subarrays with
# odd sum

# Function to find number
# of subarrays with odd sum

def countOddSum(a, n):

    # 'odd' stores number of
    # odd numbers upto ith index
    # 'c_odd' stores number of
    # odd sum subarrays starting
    # at ith index
    # 'Result' stores the number
    # of odd sum subarrays
    c_odd = 0;
    result = 0;
    odd = False;

    # First find number of odd
    # sum subarrays starting at
    # 0th index
    for i in range(n):
        if (a[i] % 2 == 1):
            if(odd == True):
                odd = False;
            else:
                odd = True;

        if (odd):
            c_odd += 1;

    # Find number of odd sum
    # subarrays starting at ith
    # index add to result
    for i in range(n):
        result += c_odd;
        if (a[i] % 2 == 1):
            c_odd = (n - i - c_odd);

    return result;

# Driver code
if __name__ == '__main__':

    ar = [5, 4, 4, 5, 1, 3];
    n = len(ar);
    print("The Number of Subarrays" +
          "with odd sum is " ,
          countOddSum(ar, n));

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program to find number of subarrays
// with odd sum
using System;

public class GFG{

// Function to find number of
// subarrays with odd sum
static int countOddSum(int []a, int n)
{

    // 'odd' stores number of odd numbers
    // upto ith index
    // 'c_odd' stores number of odd sum
    // subarrays starting at ith index
    // 'Result' stores the number of
    // odd sum subarrays
    int  c_odd = 0, result = 0;
    bool odd = false;

    // First find number of odd sum
    // subarrays starting at 0th index
    for(int i = 0; i < n; i++)
    {
        if (a[i] % 2 == 1)
        {
            odd = !odd;
        }
        if (odd)
        {
            c_odd++;
        }
    }

    // Find number of odd sum subarrays
    // starting at ith index add to result
    for(int i = 0; i < n; i++)
    {
        result += c_odd;
        if (a[i] % 2 == 1)
        {
            c_odd = (n - i - c_odd);
        }
    }
    return result;
}

// Driver code
public static void Main(String[] args)
{
    int []ar = { 5, 4, 4, 5, 1, 3 };
    int n = ar.Length;

    Console.Write("The Number of Subarrays " +
                     "with odd sum is " +
                     countOddSum(ar, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

  // JavaScript program to find number
  // of subarrays with odd sum

  // Function to find number of
  // subarrays with odd sum
  function countOddSum(a, n)
  {

      // 'odd' stores number of odd numbers
      // upto ith index
      // 'c_odd' stores number of odd sum
      // subarrays starting at ith index
      // 'Result' stores the number of
      // odd sum subarrays
      let  c_odd = 0, result = 0;
      let odd = false;

      // First find number of odd sum
      // subarrays starting at 0th index
      for(let i = 0; i < n; i++)
      {
          if (a[i] % 2 == 1)
          {
              odd = !odd;
          }
          if (odd)
          {
              c_odd++;
          }
      }

      // Find number of odd sum subarrays
      // starting at ith index add to result
      for(let i = 0; i < n; i++)
      {
          result += c_odd;
          if (a[i] % 2 == 1)
          {
              c_odd = (n - i - c_odd);
          }
      }
      return result;
  }

  let ar = [ 5, 4, 4, 5, 1, 3 ];
  let n = ar.length;

  document.write("The Number of Subarrays " +
                   "with odd sum is " +
                   countOddSum(ar, n));

</script>
```

**输出:**

```
The Number of Subarrays with odd sum is 12
```

**时间复杂度:**O(N)
T3】空间复杂度: O(1)