# 切换一个数字除第 k 位以外的所有位。

> 原文:[https://www . geesforgeks . org/toggle-bits-number-except-k-th-bit/](https://www.geeksforgeeks.org/toggle-bits-number-except-k-th-bit/)

给定一个正(或无符号)整数 **n** ，编写一个函数来切换除第 k 位以外的所有位。这里 k 的值从 0(零)开始，从右开始。

**示例**:

```
Input : n = 4294967295, k = 0
Output : 1
The number 4294967295 in 32 bits has all bits
set.  When we toggle all bits except last bit,
we get 1.

Input  :  n = 1, k = 1
Output : 4294967292
4294967262 has all bits toggled except second
bit from right.
```

1.  在第 k 个位置切换位。我们通过找到一个只有第 k 位集的数字(使用 1 << k)，然后对这个数字 n 进行按位异或运算来实现。
2.  使用~ ( [逐位求反](https://www.geeksforgeeks.org/interesting-facts-bitwise-operators-c/))切换上面获得的所有位数

## C++

```
// C++ program to toggle all bits except kth bit
#include <iostream>
using namespace std;

// Returns a number with all bit toggled in n
// except k-th bit
unsigned int toggleAllExceptK(unsigned int n,
                              unsigned int k)
{

    /* 1) Toggle k-th bit by doing n ^ (1 << k)
       2) Toggle all bits of the modified number */
    return ~(n ^ (1 << k));
}

// Driver code
int main()
{
    unsigned int n = 4294967295;
    unsigned int k = 0;

    cout << toggleAllExceptK(n, k);

    return 0;
}

// This code is contributed by khushboogoyal499
```

## C

```
// C program to toggle all bits except kth bit
#include<stdio.h>

// Returns a number with all bit toggled in n
// except k-th bit
unsigned int toggleAllExceptK(unsigned int n,
                            unsigned int k)
{
   /* 1) Toggle k-th bit by doing n ^ (1 << k)
      2) Toggle all bits of the modified number */
    return ~(n ^ (1 << k));
}

// Driver code
int main()
{
    unsigned int n = 4294967295;
    unsigned int k = 0;
    printf("%u", toggleAllExceptK( n, k));
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to toggle all bits
# except kth bit

# Returns a number with all bit toggled
# in n except k-th bit
def toggleAllExceptK(n, k):

    # 1) Toggle k-th bit by doing n ^ (1 << k)
    # 2) Toggle all bits of the modified number
    temp = bin(n ^ (1 << k))[2:]

    ans = ""

    for i in temp:
        if i == '1':
            ans += '0'
        else:
            ans += '1'

    return int(ans, 2)

# Driver code
if __name__ == '__main__':

    n = 4294967295
    k = 0

    print(toggleAllExceptK(n, k))

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>
// javascript program to toggle all bits except kth bit

    // Returns a number with all bit toggled in n
    // except k-th bit
    function toggleAllExceptK(n,k)
    {
        /* 1) Toggle k-th bit by doing n ^ (1 << k)
           2) Toggle all bits of the modified number */
        return ~(n ^ (1 << k));
    }

    // Driver code
    let n = 4294967295;
    let k = 0;
    document.write(toggleAllExceptK(n, k));

    //This code is contributed by unknown2108

</script>
```

**输出:**

```
1
```