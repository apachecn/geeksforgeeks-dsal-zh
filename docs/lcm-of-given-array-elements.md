# 给定数组元素的 LCM

> 原文:[https://www.geeksforgeeks.org/lcm-of-given-array-elements/](https://www.geeksforgeeks.org/lcm-of-given-array-elements/)

给定一个 n 个数的数组，求它的 LCM。

```
Input : {1, 2, 8, 3}
Output : 24

Input : {2, 7, 3, 9, 4}
Output : 252
```

我们知道，
![LCM(a, b)=\frac{a*b}{gcd(a, b)}            ](img/1d0dd08541b27107b2180787eac5222c.png "Rendered by QuickLaTeX.com")
上面的关系只适用于两个数字，
![LCM(a, b, c)\neq \frac{a*b*c}{gcd(a, b, c)}            ](img/1e04df22fd899ff92859a0edc9943b20.png "Rendered by QuickLaTeX.com")
这里的想法是将我们的关系扩展到 2 个以上的数字。假设我们有一个数组 arr[]包含 n 个元素，需要计算它们的 LCM。
我们算法的主要步骤是:

1.  初始化 ans = arr[0]。
2.  迭代数组的所有元素，即从 i = 1 到 i = n-1
    在第 I 次迭代中 ans = LCM(arr[0]，arr[1]，…)..，arr[i-1])。这可以通过 **LCM(arr[0]，arr[1]，…)轻松完成。，arr[i]) = LCM(ans，arr[i])** 。因此在第 I 次迭代中，我们只需要做 **ans = LCM(ans，arr[i]) = ans x arr[i] / gcd(ans，arr[i])**

以下是上述算法的实现:

## C++

```
// C++ program to find LCM of n elements
#include <bits/stdc++.h>
using namespace std;

typedef long long int ll;

// Utility function to find
// GCD of 'a' and 'b'
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Returns LCM of array elements
ll findlcm(int arr[], int n)
{
    // Initialize result
    ll ans = arr[0];

    // ans contains LCM of arr[0], ..arr[i]
    // after i'th iteration,
    for (int i = 1; i < n; i++)
        ans = (((arr[i] * ans)) /
                (gcd(arr[i], ans)));

    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 2, 7, 3, 9, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printf("%lld", findlcm(arr, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find LCM of n elements
public class GFG {

    public static long lcm_of_array_elements(int[] element_array)
    {
        long lcm_of_array_elements = 1;
        int divisor = 2;

        while (true) {
            int counter = 0;
            boolean divisible = false;

            for (int i = 0; i < element_array.length; i++) {

                // lcm_of_array_elements (n1, n2, ... 0) = 0.
                // For negative number we convert into
                // positive and calculate lcm_of_array_elements.

                if (element_array[i] == 0) {
                    return 0;
                }
                else if (element_array[i] < 0) {
                    element_array[i] = element_array[i] * (-1);
                }
                if (element_array[i] == 1) {
                    counter++;
                }

                // Divide element_array by devisor if complete
                // division i.e. without remainder then replace
                // number with quotient; used for find next factor
                if (element_array[i] % divisor == 0) {
                    divisible = true;
                    element_array[i] = element_array[i] / divisor;
                }
            }

            // If divisor able to completely divide any number
            // from array multiply with lcm_of_array_elements
            // and store into lcm_of_array_elements and continue
            // to same divisor for next factor finding.
            // else increment divisor
            if (divisible) {
                lcm_of_array_elements = lcm_of_array_elements * divisor;
            }
            else {
                divisor++;
            }

            // Check if all element_array is 1 indicate
            // we found all factors and terminate while loop.
            if (counter == element_array.length) {
                return lcm_of_array_elements;
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] element_array = { 2, 7, 3, 9, 4 };
        System.out.println(lcm_of_array_elements(element_array));
    }
}

// Code contributed by Mohit Gupta_OMG
```

## 计算机编程语言

```
# Python Program to find LCM of n elements

def find_lcm(num1, num2):
    if(num1>num2):
        num = num1
        den = num2
    else:
        num = num2
        den = num1
    rem = num % den
    while(rem != 0):
        num = den
        den = rem
        rem = num % den
    gcd = den
    lcm = int(int(num1 * num2)/int(gcd))
    return lcm

l = [2, 7, 3, 9, 4]

num1 = l[0]
num2 = l[1]
lcm = find_lcm(num1, num2)

for i in range(2, len(l)):
    lcm = find_lcm(lcm, l[i])

print(lcm)

# Code contributed by Mohit Gupta_OMG
```

## C#

```
// C# Program to find LCM of n elements
using System;

public class GFG {

    public static long lcm_of_array_elements(int[] element_array)
    {
        long lcm_of_array_elements = 1;
        int divisor = 2;

        while (true) {

            int counter = 0;
            bool divisible = false;
            for (int i = 0; i < element_array.Length; i++) {

                // lcm_of_array_elements (n1, n2, ... 0) = 0.
                // For negative number we convert into
                // positive and calculate lcm_of_array_elements.
                if (element_array[i] == 0) {
                    return 0;
                }
                else if (element_array[i] < 0) {
                    element_array[i] = element_array[i] * (-1);
                }
                if (element_array[i] == 1) {
                    counter++;
                }

                // Divide element_array by devisor if complete
                // division i.e. without remainder then replace
                // number with quotient; used for find next factor
                if (element_array[i] % divisor == 0) {
                    divisible = true;
                    element_array[i] = element_array[i] / divisor;
                }
            }

            // If divisor able to completely divide any number
            // from array multiply with lcm_of_array_elements
            // and store into lcm_of_array_elements and continue
            // to same divisor for next factor finding.
            // else increment divisor
            if (divisible) {
                lcm_of_array_elements = lcm_of_array_elements * divisor;
            }
            else {
                divisor++;
            }

            // Check if all element_array is 1 indicate
            // we found all factors and terminate while loop.
            if (counter == element_array.Length) {
                return lcm_of_array_elements;
            }
        }
    }

    // Driver Code
    public static void Main()
    {
        int[] element_array = { 2, 7, 3, 9, 4 };
        Console.Write(lcm_of_array_elements(element_array));
    }
}

// This Code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find LCM of n elements

// Utility function to find
// GCD of 'a' and 'b'
function gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return gcd($b, $a % $b);
}

// Returns LCM of array elements
function findlcm($arr, $n)
{

    // Initialize result
    $ans = $arr[0];

    // ans contains LCM of
    // arr[0], ..arr[i]
    // after i'th iteration,
    for ($i = 1; $i < $n; $i++)
        $ans = ((($arr[$i] * $ans)) /
                (gcd($arr[$i], $ans)));

    return $ans;
}

// Driver Code
$arr = array(2, 7, 3, 9, 4 );
$n = sizeof($arr);
echo findlcm($arr, $n);

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find LCM of n elements

// Utility function to find
// GCD of 'a' and 'b'
function gcd(a, b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Returns LCM of array elements
function findlcm(arr, n)
{
    // Initialize result
    let ans = arr[0];

    // ans contains LCM of arr[0], ..arr[i]
    // after i'th iteration,
    for (let i = 1; i < n; i++)
        ans = (((arr[i] * ans)) /
                (gcd(arr[i], ans)));

    return ans;
}

// Driver Code

    let arr = [ 2, 7, 3, 9, 4 ];
    let n = arr.length;
    document.write(findlcm(arr, n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
252
```

下面是上述算法的递归实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

//recursive implementation
int LcmOfArray(vector<int> arr, int idx){
    // lcm(a,b) = (a*b/gcd(a,b))
    if (idx == arr.size()-1){
        return arr[idx];
    }
    int a = arr[idx];
    int b = LcmOfArray(arr, idx+1);
    return (a*b/__gcd(a,b)); // __gcd(a,b) is inbuilt library function
}

int main() {

    vector<int> arr = {1,2,8,3};
    cout << LcmOfArray(arr, 0) << "\n";
      arr = {2,7,3,9,4};
      cout << LcmOfArray(arr,0) << "\n";
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
  static int LcmOfArray(int[] arr, int idx)
  {

    // lcm(a,b) = (a*b/gcd(a,b))
    if (idx == arr.length - 1){
      return arr[idx];
    }
    int a = arr[idx];
    int b = LcmOfArray(arr, idx+1);
    return (a*b/__gcd(a,b)); //
  }

  public static void main(String[] args)
  {

    int[] arr = {1,2,8,3};
    System.out.print(LcmOfArray(arr, 0)+ "\n");
    int[]  arr1 = {2,7,3,9,4};
    System.out.print(LcmOfArray(arr1,0)+ "\n");
  }
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
def __gcd(a, b):
    if (a == 0):
        return b
    return __gcd(b % a, a)

# recursive implementation
def LcmOfArray(arr, idx):

    # lcm(a,b) = (a*b/gcd(a,b))
    if (idx == len(arr)-1):
        return arr[idx]
    a = arr[idx]
    b = LcmOfArray(arr, idx+1)
    return int(a*b/__gcd(a,b)) # __gcd(a,b) is inbuilt library function

arr = [1,2,8,3]
print(LcmOfArray(arr, 0))
arr = [2,7,3,9,4]
print(LcmOfArray(arr,0))

# This code is contributed by divyeshrabadiya07.
```

## C#

```
using System;
class GFG {

    // Function to return
    // gcd of a and b
    static int __gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return __gcd(b % a, a);
    }

    //recursive implementation
    static int LcmOfArray(int[] arr, int idx){
        // lcm(a,b) = (a*b/gcd(a,b))
        if (idx == arr.Length-1){
            return arr[idx];
        }
        int a = arr[idx];
        int b = LcmOfArray(arr, idx+1);
        return (a*b/__gcd(a,b)); // __gcd(a,b) is inbuilt library function
    }

  static void Main() {
    int[] arr = {1,2,8,3};
    Console.WriteLine(LcmOfArray(arr, 0));
    int[] arr1 = {2,7,3,9,4};
    Console.WriteLine(LcmOfArray(arr1,0));
  }
}
```

## java 描述语言

```
<script>

    // Function to return
    // gcd of a and b
    function __gcd(a, b)
    {
        if (a == 0)
            return b;
        return __gcd(b % a, a);
    }

    //recursive implementation
    function LcmOfArray(arr, idx){
        // lcm(a,b) = (a*b/gcd(a,b))
        if (idx == arr.length-1){
            return arr[idx];
        }
        let a = arr[idx];
        let b = LcmOfArray(arr, idx+1);
        return (a*b/__gcd(a,b)); // __gcd(a,b) is inbuilt library function
    }

    let arr = [1,2,8,3];
    document.write(LcmOfArray(arr, 0) + "</br>");
    arr = [2,7,3,9,4];
    document.write(LcmOfArray(arr,0));

// This code is contributed by decode2207.
</script>
```

**Output**

```
24
252
```

**相关文章:**

*   [不使用 GCD 查找两个以上(或数组)数的 LCM](https://www.geeksforgeeks.org/finding-lcm-two-array-numbers-without-using-gcd/)
*   [c++中计算 LCM 的内置函数](https://www.geeksforgeeks.org/inbuilt-function-calculating-lcm-cpp/)

本文由**马达尔·莫迪**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息