# 设置最右边的关闭位

> 原文:[https://www.geeksforgeeks.org/set-the-rightmost-off-bit/](https://www.geeksforgeeks.org/set-the-rightmost-off-bit/)

写一个设置整数最右边 0 位的程序。
**例:**

```
Input:  12 (00...01100)
Output: 13 (00...01101)

Input:  7 (00...00111)
Output: 15 (00...01111)
```

如果我们给一个数加 1，最右边的未置位(或零位)之后的所有置位都变成 0，最右边的未置位变成 1。

## C++

```
// CPP program to set the rightmost unset bit
#include<iostream>
using namespace std;

int setRightmostUnsetBit(int n)
{    
    // If all bits are set 
    if ((n & (n + 1)) == 0)    
        return n;

    // Set rightmost 0 bit
    return n | (n+1);    
}

// Driver program to test above
int main()
{
    int n = 21;
    cout << setRightmostUnsetBit(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java  program to set the rightmost unset bit

public class GFG {

    static int setRightmostUnsetBit(int n)
    {    
     // If all bits are set 
     if ((n & (n + 1)) == 0)    
         return n;

     // Set rightmost 0 bit
     return n | (n+1);    
    }

    //Driver program to test above
    public static void main(String[] args) {

         int n = 21;
         System.out.println(setRightmostUnsetBit(n));
    }

}
```

## 蟒蛇 3

```
# Python3 program to set the
# rightmost unset bit

def setRightmostUnsetBit(n) :

    # If all bits are set
    if n & (n + 1) == 0 :
        return n

    # Set rightmost 0 bit
    return n | (n+1)

# Driver code    
if __name__ == "__main__" :

    n = 21
    print(setRightmostUnsetBit(n))

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# program to set the rightmost unset bit

using System;

public class GFG {

    static int setRightmostUnsetBit(int n)
    {    
     // If all bits are set 
     if ((n & (n + 1)) == 0)    
         return n;

     // Set rightmost 0 bit
     return n | (n+1);    
    }

    //Driver program to test above
    public static void Main() {

         int n = 21;
         Console.WriteLine(setRightmostUnsetBit(n));
    }

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to set the
// rightmost unset bit
function setRightmostUnsetBit($n)
{
    // If all bits are set
    if (($n & ($n + 1)) == 0)
        return $n;

    // Set rightmost 0 bit
    return $n | ($n + 1);
}

// Driver Code
$n = 21;
echo setRightmostUnsetBit($n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// JavaScript program to set the rightmost unset bit
function setRightmostUnsetBit(n)
{   
    // If all bits are set
    if ((n & (n + 1)) == 0)   
        return n;

    // Set rightmost 0 bit
    return n | (n + 1);   
}

// Driver program to test above
    let n = 21;
    document.write(setRightmostUnsetBit(n));

// This code is contributed by Manoj.
</script>
```

**Output:** 

```
23
```

**时间复杂度:** O(1)

**辅助空间:** O(1)