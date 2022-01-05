# 检查一个数字的偶数位数字的乘积是否能被奇数位数字的和整除

> 原文:[https://www . geesforgeks . org/check-偶数位置的位数乘积是否可被奇数位置的位数和除尽/](https://www.geeksforgeeks.org/check-whether-product-of-digits-at-even-places-is-divisible-by-sum-of-digits-at-odd-place-of-a-number/)

给定一个数 N 和 N 中的位数，任务是检查一个数的偶数位的位数乘积是否能被奇数位的位数之和整除。如果它是可分的，输出“真”，否则输出“假”。

**示例:**

```
Input: N = 2157 
Output: TRUE
Since, 1 * 7 = 7, which is divisible by 2+5=7

Input: N = 1234
Output: TRUE
Since, 2 * 4 = 8, which is divisible by 1 + 3 = 4   
```

**进场:**

1.  在从右到左的偶数位置寻找数字的乘积。
2.  从右到左找出奇数位的数字总和。
3.  然后用和取模来检验乘积的可除性
4.  如果模为 0，输出真，否则输出假

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// below function checks whether
// product of digits at even places
// is divisible by sum of digits at odd places
bool productSumDivisible(int n, int size)
{
    int sum = 0, product = 1;
    while (n > 0) {

        // if size is even
        if (size % 2 == 0) {
            product *= n % 10;
        }

        // if size is odd
        else {
            sum += n % 10;
        }
        n = n / 10;
        size--;
    }

    if (product % sum == 0)
        return true;
    return false;
}

// Driver code
int main()
{
    int n = 1234;
    int len = 4;

    if (productSumDivisible(n, len))
        cout << "TRUE";
    else
        cout << "FALSE";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation of the above approach

class GFG {

    // below function checks whether
    // product of digits at even places
    // is divisible by sum of digits at odd places
    static boolean productSumDivisible(int n, int size)
    {
        int sum = 0, product = 1;
        while (n > 0) {

            // if size is even
            if (size % 2 == 0) {
                product *= n % 10;
            }

            // if size is odd
            else {
                sum += n % 10;
            }
            n = n / 10;
            size--;
        }

        if (product % sum == 0) {
            return true;
        }
        return false;
    }
    // Driver code

    public static void main(String[] args)
    {
        int n = 1234;
        int len = 4;

        if (productSumDivisible(n, len)) {
            System.out.println("TRUE");
        }
        else {
            System.out.println("FALSE");
        }
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

# Below function checks whether product
# of digits at even places is divisible
# by sum of digits at odd places
def productSumDivisible(n, size):
    sum = 0
    product = 1
    while (n > 0) :

        # if size is even
        if (size % 2 == 0) :
            product *= n % 10

        # if size is odd
        else :
            sum += n % 10

        n = n // 10
        size -= 1

    if (product % sum == 0):
        return True
    return False

# Driver code
if __name__ == "__main__":
    n = 1234
    len = 4

    if (productSumDivisible(n, len)):
        print("TRUE")
    else :
        print("FALSE")

# This code is contributed by ChitraNayal
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

    // below function checks whether
    // product of digits at even places
    // is divisible by K
    static bool productSumDivisible(int n, int size)
    {
        int sum = 0, product = 1;
        while (n > 0) {

            // if size is even
            if (size % 2 == 0) {
                product *= n % 10;
            }

            // if size is odd
            else {
                sum += n % 10;
            }
            n = n / 10;
            size--;
        }

        if (product % sum == 0) {
            return true;
        }
        return false;
    }

    // Driver code
    public static void Main()
    {
        int n = 1234;
        int len = 4;

        if (productSumDivisible(n, len))
            Console.WriteLine("TRUE");
        else
            Console.WriteLine("FALSE");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Below function checks whether
// product of digits at even
// places is divisible by sum of
// digits at odd places
function productSumDivisible($n, $size)
{
    $sum = 0; $product = 1;
    while ($n > 0)
    {

        // if size is even
        if ($size % 2 == 0)
        {
            $product *= $n % 10;
        }

        // if size is odd
        else
        {
            $sum += $n % 10;
        }
        $n = $n / 10;
        $size--;
    }

    if ($product % $sum == 0)
        return true;
    return false;
}

// Driver code
$n = 1234;
$len = 4;

if (productSumDivisible($n, $len))
    echo "TRUE";
else
    echo "FALSE";

// This code is contributed by anuj_67..
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// below function checks whether
// product of digits at even places
// is divisible by sum of digits at odd places
function productSumDivisible(n, size)
{
    var sum = 0, product = 1;
    while (n > 0) {

        // if size is even
        if (size % 2 == 0) {
            product *= n % 10;
        }

        // if size is odd
        else {
            sum += n % 10;
        }
        n = parseInt(n / 10);
        size--;
    }

    if (product % sum == 0)
        return true;
    return false;
}

// Driver code
var n = 1234;
var len = 4;
if (productSumDivisible(n, len))
    document.write("TRUE");
else
    document.write("FALSE");

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
TRUE
```

### 方法 2:使用 string()方法

将整数转换为字符串，然后遍历字符串并执行两个操作

*   将所有奇数索引相乘并存储在乘积中
*   将所有偶数索引相加并存储在一起
*   如果乘积能被和整除，则返回真，否则返回假

下面是实现:

## C++

```
// C++ implementation of the above approach
#include <iostream>

using namespace std;
#include<string>

  // Below function checks whether product
  // of digits at even places is divisible
  // by sum of digits at odd places
bool  productSumDivisible(int n)
  {
    int sum = 0;
    int product = 1;

    // Converting integer to string
    string num = to_string(n);

    // Traveersing the string
    for(int i = 0 ; i < num.length() ; i++ ) {
      if(i % 2 != 0){
        product = product*(num[i]);
      }
      else{
        sum = sum+int(num[i]);
      }
    }

    if (product % sum == 0){
      return true ;
    }
    else{
      return false;
    }       
  }

  // Driver code
 int main()
 {

    int n = 1234;

    if (productSumDivisible(n))
    {
      cout<<"true";
    }
    else{
     cout<<"false";
    }

}

// This code is contributed by akshitsaxena07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG {

  // Below function checks whether product
  // of digits at even places is divisible
  // by sum of digits at odd places
  static boolean productSumDivisible(int n)
  {
    int sum = 0;
    int product = 1;

    // Converting integer to string
    String num = String.valueOf(n);

    // Traveersing the string
    for(int i = 0 ; i < num.length() ; i++ ) {
      if(i % 2 != 0){
        product = product*Character.getNumericValue(num.charAt(i));
      }
      else{
        sum = sum+Character.getNumericValue(num.charAt(i));
      }
    }

    if (product % sum == 0){
      return true ;
    }
    else{
      return false;
    }       
  }

  // Driver code
  public static void main (String[] args) {

    int n = 1234;

    if (productSumDivisible(n))
    {
      System.out.println("TRUE");
    }
    else{
      System.out.println("FALSE");
    }
  }
}

// This code is contributed by rag2127.
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

# Below function checks whether product
# of digits at even places is divisible
# by sum of digits at odd places
def productSumDivisible(n):
    sum = 0
    product = 1

    # Converting integer to string
    num = str(n)

    # Traveersing the string
    for i in range(len(num)):
        if(i % 2 != 0):
            product = product*int(num[i])
        else:
            sum = sum+int(num[i])

    if (product % sum == 0):
        return True
    return False

# Driver code
if __name__ == "__main__":
    n = 1234

    if (productSumDivisible(n)):
        print("TRUE")
    else:
        print("FALSE")

# This code is contributed by vikkycirus
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Below function checks whether product
// of digits at even places is divisible
// by sum of digits at odd places
static bool productSumDivisible(int n)
{
    int sum = 0;
    int product = 1;

    // Converting integer to string
    string num = n.ToString();

    // Traveersing the string
    for(int i = 0; i < num.Length; i++ )
    {
        if (i % 2 != 0)
        {
            product = product*(int)Char.GetNumericValue(num[i]);
        }
        else
        {
            sum = sum+(int)Char.GetNumericValue(num[i]);
        }
    }

    if (product % sum == 0)
    {
        return true;
    }
    else
    {
        return false;
    }      
}

// Driver code
static public void Main()
{
    int n = 1234;

    if (productSumDivisible(n))
    {
        Console.WriteLine("TRUE");
    }
    else
    {
        Console.WriteLine("FALSE");
    }
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Below function checks whether product
// of digits at even places is divisible
// by sum of digits at odd places
function productSumDivisible(n){
    var sum = 0
    var product = 1

    // Converting integer to string
    var num = n.toString();

    // Traveersing the string
    for(i = 0 ; i < num.length ; i++ ) {
        if(i % 2 != 0){
            product = product*Number(num[i])
        }
        else{
            sum = sum+Number(num[i])
        }
    }

    if (product % sum == 0){
        return true ;
     }
    else{
    return false;
    }
}

// Driver code
   var  n = 1234

    if (productSumDivisible(n)){
        document.write("TRUE")
    }
    else{
        document.write("FALSE")
    }

</script>
```

**输出:**

```
TRUE
```