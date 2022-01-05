# 两个大数的 LCM

> 原文:[https://www.geeksforgeeks.org/lcm-of-two-large-numbers/](https://www.geeksforgeeks.org/lcm-of-two-large-numbers/)

给出两个大数字‘a’和‘b’这样的 that(10^20 <=a, b<=10^300). Find the LCM of two large numbers given.
**的例子:**

```
 Input: a = 234516789234023485693020129
        b = 176892058718950472893785940
 Output: 41484157651764614525905399263631111992263435437186260

 Input: a = 36594652830916364940473625749407
        b = 448507083624364748494746353648484939
 Output: 443593541011902763984944550799004089258248037004507648321189937329

```

**解决方案:**在给定的问题中，我们可以看到数量非常大，超出了所有可用的原语数据类型的限制，因此我们不得不在 Java 中使用 BigInteger Class 的概念。因此，我们将给定的字符串转换为 biginteger，然后使用 Java . math . big integer . gcd(big integer val)方法计算大数的 gcd，然后使用以下公式计算 LCM:
LCM * HCF = x * y，其中 x 和 y 是两个数字

下面是上述想法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find LCM of two large numbers
import java.math.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // function to calculate LCM of two large numbers
    public static BigInteger lcm(String a, String b)
    {
        // convert string 'a' and 'b' into BigInteger
        BigInteger s = new BigInteger(a);
        BigInteger s1 = new BigInteger(b);

        // calculate multiplication of two bigintegers
        BigInteger mul = s.multiply(s1);

        // calculate gcd of two bigintegers
        BigInteger gcd = s.gcd(s1);

        // calculate lcm using formula: lcm * gcd = x * y
        BigInteger lcm = mul.divide(gcd);
        return lcm;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Input 'a' and 'b' are in the form of strings because
        // they can not be handled by integer data type
        String a = "36594652830916364940473625749407";
        String b = "448507083624364748494746353648484939";

        System.out.print(lcm(a, b));
    }
}
// Code contributed by Saurav Jain
```

## 蟒蛇 3

```
# Python3 program to find LCM of two 
# large numbers
import math

# Function to calculate LCM of two
# large numbers
def lcm (a, b):

    # Convert string 'a' and 'b' 
    # into Integer
    s = int(a)
    s1 = int(b)

    # Calculate multiplication of 
    # both integers
    mul = s * s1

    # Calculate gcd of two integers
    gcd = math.gcd(s, s1)

    # Calculate lcm using 
    # formula: lcm * gcd = x * y
    lcm = mul // gcd

    return lcm

# Driver Code
if __name__ == '__main__':

    # Input 'a' and 'b' are in the
    # form of strings
    a = "36594652830916364940473625749407"
    b = "448507083624364748494746353648484939"

    print(lcm(a, b))

# This code is contributed by himanshu77
```

**输出:**

```
443593541011902763984944550799004089258248037004507648321189937329

```