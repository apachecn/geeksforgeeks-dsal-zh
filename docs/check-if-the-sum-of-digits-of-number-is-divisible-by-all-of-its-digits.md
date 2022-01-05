# 检查数字的位数总和是否能被其所有位数整除

> 原文:[https://www . geeksforgeeks . org/check-如果数字总和被其所有数字整除/](https://www.geeksforgeeks.org/check-if-the-sum-of-digits-of-number-is-divisible-by-all-of-its-digits/)

给定一个整数 **N** ，任务是检查给定数的位数之和是否能被其所有位数整除。如果可分，则打印**是**否则打印**否**。

**示例:**

> **输入:** N = 12
> **输出:**否
> 位数之和= 1 + 2 = 3
> 3 可被 1 整除但不能被 2 整除。
> 
> **输入:**N = 123
> T3】输出:是

**方法:**先求数字的位数之和，然后逐一检查，计算出的和是否能被数字的所有位数整除。如果某个数字不能被整除，则打印**否**否则打印**是**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if all the digits
// of n divide the sum of the digits of n
bool isDivisible(long long int n)
{

    // Store a copy of the original number
    long long int temp = n;

    // Find the sum of the digits of n
    int sum = 0;
    while (n) {
        int digit = n % 10;
        sum += digit;
        n /= 10;
    }

    // Restore the original value
    n = temp;

    // Check if all the digits divide
    // the calculated sum
    while (n) {
        int digit = n % 10;

        // If current digit doesn't
        // divide the sum
        if (sum % digit != 0)
            return false;

        n /= 10;
    }

    return true;
}

// Driver code
int main()
{
    long long int n = 123;

    if (isDivisible(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns true if all the digits
    // of n divide the sum of the digits of n
    static boolean isDivisible(long n)
    {

        // Store a copy of the original number
        long temp = n;

        // Find the sum of the digits of n
        int sum = 0;
        while (n != 0)
        {
            int digit = (int) n % 10;
            sum += digit;
            n /= 10;
        }

        // Restore the original value
        n = temp;

        // Check if all the digits divide
        // the calculated sum
        while (n != 0)
        {
            int digit = (int)n % 10;

            // If current digit doesn't
            // divide the sum
            if (sum % digit != 0)
                return false;

            n /= 10;
        }
        return true;
    }

    // Driver code
    public static void main (String[] args)
    {
        long n = 123;

        if (isDivisible(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python implementation of the approach

# Function that returns true if all the digits
# of n divide the sum of the digits of n
def isDivisible(n):

    # Store a copy of the original number
    temp = n

    # Find the sum of the digits of n
    sum = 0
    while (n):
        digit = n % 10
        sum += digit
        n //= 10

    # Restore the original value
    n = temp

    # Check if all the digits divide
    # the calculated sum
    while(n):
        digit = n % 10

        # If current digit doesn't
        # divide the sum
        if(sum % digit != 0):
            return False

        n //= 10;

    return True

# Driver code
n = 123
if(isDivisible(n)):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if all the digits
    // of n divide the sum of the digits of n
    static bool isDivisible(long n)
    {

        // Store a copy of the original number
        long temp = n;

        // Find the sum of the digits of n
        int sum = 0;
        while (n != 0)
        {
            int digit = (int) n % 10;
            sum += digit;
            n /= 10;
        }

        // Restore the original value
        n = temp;

        // Check if all the digits divide
        // the calculated sum
        while (n != 0)
        {
            int digit = (int)n % 10;

            // If current digit doesn't
            // divide the sum
            if (sum % digit != 0)
                return false;

            n /= 10;
        }
        return true;
    }

    // Driver code
    static public void Main ()
    {
        long n = 123;

        if (isDivisible(n))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by @tushil.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach    

// Function that returns true if all the
// digits of n divide the sum of the digits
// of n
function isDivisible(n)
{

    // Store a copy of the original number
    var temp = n;

    // Find the sum of the digits of n
    var sum = 0;

    while (n != 0)
    {
        var digit = parseInt(n % 10);
        sum += digit;
        n = parseInt(n / 10);
    }

    // Restore the original value
    n = temp;

    // Check if all the digits divide
    // the calculated sum
    while (n != 0)
    {
        var digit = parseInt(n % 10);

        // If current digit doesn't
        // divide the sum
        if (sum % digit != 0)
            return false;

        n = parseInt(n/10);
    }
    return true;
}

// Driver code
var n = 123;

if (isDivisible(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by todaysgaurav

</script>
```

**Output**

```
Yes
```

**时间复杂度:** O(log(N))
**辅助空间:** O(1)

#### 方法 2:使用字符串:

*   我们必须通过取一个新的变量把给定的数字转换成字符串。
*   遍历字符串，将每个元素转换为整数，并将其相加。
*   再次遍历字符串
*   检查总和是否不能被任何一个数字整除
*   如果是真的，则返回假的
*   否则返回真

下面是上述方法的实现:

## 蟒蛇 3

```
# Python implementation of above approach
def getResult(n):

    # Converting integer to string
    st = str(n)

    # Initialising sum to 0
    sum = 0
    length = len(st)

    # Traversing through the string
    for i in st:

        # Converting character to int
        sum = sum + int(i)

    # Comparing number and sum
    # Traversing again
    for i in st:

        # Check if any digit is
        # not dividing the sum
        if(sum % int(i) != 0):

            # Return false
            return 'No'

    # If any value is not returned
    # then all the digits are dividing the sum
    # SO return true
    return 'Yes'

# Driver Code
n = 123

# passing this number to get result function
print(getResult(n))

# this code is contributed by vikkycirus
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

function getResult(n){

    // Converting integer to string
    var st = n.toString();

    // Initialising sum to 0
    var sum = 0
    var length = st.length;

    // Traversing through the string
    for (var i= 0 ;i<st.length ; i++){

        // Converting character to int
        sum = sum + Number(st[i])
    }

    // Comparing number and sum
    // Traversing again
    for( var i = 0 ; i < st.length ; i++){

        // Check if any digit is
        // not dividing the sum
        if(sum % Number(st[i]) != 0){

            // Return false
            return 'No'
        }

    // If any value is not returned
    // then all the digits are dividing the sum
    // SO return true
        else{
            return 'Yes';
          }
    }

}

// Driver Code
var n = 123;

// passing this number to get result function
document.write(getResult(n));

</script>
```

**Output**

```
Yes
```