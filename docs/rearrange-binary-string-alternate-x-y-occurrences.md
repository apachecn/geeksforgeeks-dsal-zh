# 重新排列二进制字符串为`x`和`y`的交替出现

> 原文： [https://www.geeksforgeeks.org/rearrange-binary-string-alternate-x-y-occurrences/](https://www.geeksforgeeks.org/rearrange-binary-string-alternate-x-y-occurrences/)

给定一个二进制字符串`s`，并给出两个整数`x`和`y`。 任务是按照给定的字符串进行排列，以使 0 代表`X`，然后 1 代表`Y`，依此类推，直到完成 0 或 1 之一。 然后将字符串的其余部分连接起来并打印最终的字符串。

给出：`x`或`y`不能为 0

例子：

```
Input : s = "0011"
        x = 1
        y = 1
Output : 0101
x is 1 and y is 1\. So first we print
'0' one time the '1' one time and 
then we print '0', after printing '0',
all 0's are vanished from the given
string so we concatenate rest of the 
string which is '1'. 

Input : s = '1011011'
        x = 1
        y = 1
Output : 0101111

```



1.  计算字符串中 0 和 1 的数量。

2.  执行循环，直到两个字母之一完成。

    1.  首先打印 0 直到`x`且递减计数为 0。

    2.  然后打印 1 直到`y`且递减计数为 0。

## C++ 

```cpp

// C++ program to arrange given string 
#include <bits/stdc++.h> 
using namespace std; 

// Function which arrange the given string 
void arrangeString(string str, int x, int y) 
{ 
    int count_0 = 0; 
    int count_1 = 0; 
    int len = str.length(); 

    // Counting number of 0's and 1's in the 
    // given string. 
    for (int i = 0; i < len; i++) { 
        if (str[i] == '0') 
            count_0++; 
        else
            count_1++; 
    } 

    // Printing first all 0's x-times 
    // and decrement count of 0's x-times 
    // and do the similar task with '1' 
    while (count_0 > 0 || count_1 > 0) { 
     for (int j = 0; j < x && count_0 > 0; j++) { 
        if (count_0 > 0) { 
           cout << "0"; 
           count_0--; 
        } 
     } 
     for (int j = 0; j < y && count_1 > 0; j++) { 
        if (count_1 > 0) { 
           cout << "1"; 
           count_1--; 
        } 
      } 
    } 
} 

// Driver Code 
int main() 
{ 
    string str = "01101101101101101000000"; 
    int x = 1; 
    int y = 2; 
    arrangeString(str, x, y); 
    return 0; 
} 

```

## Java

```java
// Java program to arrange given string 
import java.io.*; 
  
class GFG  
{ 
    // Function which arrange the given string 
    static void arrangeString(String str, int x, int y) 
    { 
        int count_0 = 0; 
        int count_1 = 0; 
        int len = str.length(); 
      
        // Counting number of 0's and 1's in the 
        // given string. 
        for (int i = 0; i < len; i++)  
        { 
            if (str.charAt(i) == '0') 
                count_0++; 
            else
                count_1++; 
        } 
      
        // Printing first all 0's x-times 
        // and decrement count of 0's x-times 
        // and do the similar task with '1' 
        while (count_0 > 0 || count_1 > 0)  
        { 
            for (int j = 0; j < x && count_0 > 0; j++) 
            { 
                if (count_0 > 0)  
                { 
                    System.out.print ("0"); 
                    count_0--; 
                } 
            } 
            for (int j = 0; j < y && count_1 > 0; j++) 
            { 
                if (count_1 > 0)  
                { 
                    System.out.print("1"); 
                    count_1--; 
                } 
            } 
        } 
    } 
      
    // Driver Code 
    public static void main (String[] args)  
    { 
        String str = "01101101101101101000000"; 
        int x = 1; 
        int y = 2; 
        arrangeString(str, x, y); 
  
    } 
} 
  
// This code is contributed by vt_m. 
```

## Python3

```py
# Python3 program to arrange given string  
  
# Function which arrange the given string  
def arrangeString(str1,x,y): 
    count_0=0
    count_1 =0
    n = len(str1) 
  
    # Counting number of 0's and 1's in the  
    # given string.  
    for i in range(n): 
        if str1[i] == '0': 
            count_0 +=1
        else: 
            count_1 +=1
  
    # Printing first all 0's x-times  
    # and decrement count of 0's x-times  
    # and do the similar task with '1'  
    while count_0>0 or count_1>0: 
        for i in range(0,x): 
            if count_0>0: 
                print("0",end="") 
                count_0 -=1
        for j in range(0,y): 
            if count_1>0: 
                print("1",end="") 
                count_1 -=1
  
# Driver code 
if __name__=='__main__': 
    str1 = "01101101101101101000000"
    x = 1
    y = 2
    arrangeString(str1, x, y) 
  
# This code is contributed by  
# Shrikant13 
```

## C#

```cs
// C# program to arrange given string 
using System; 
  
class GFG { 
      
    // Function which arrange the 
    // given string 
    static void arrangeString(string str, 
                             int x, int y) 
    { 
        int count_0 = 0; 
        int count_1 = 0; 
        int len = str.Length; 
      
        // Counting number of 0's and 1's 
        // in the given string. 
        for (int i = 0; i < len; i++)  
        { 
            if (str[i] == '0') 
                count_0++; 
            else
                count_1++; 
        } 
      
        // Printing first all 0's x-times 
        // and decrement count of 0's x-times 
        // and do the similar task with '1' 
        while (count_0 > 0 || count_1 > 0)  
        { 
            for (int j = 0; j < x && 
                            count_0 > 0; j++) 
            { 
                if (count_0 > 0)  
                { 
                    Console.Write("0"); 
                    count_0--; 
                } 
            } 
              
            for (int j = 0; j < y &&  
                            count_1 > 0; j++) 
            { 
                if (count_1 > 0)  
                { 
                    Console.Write("1"); 
                    count_1--; 
                } 
            } 
        } 
    } 
      
    // Driver Code 
    public static void Main ()  
    { 
        string str = "01101101101101101000000"; 
        int x = 1; 
        int y = 2; 
        arrangeString(str, x, y); 
  
    } 
} 
  
// This code is contributed by vt_m. 
```

## PHP

```php
<?php 
// PHP program to arrange given string 
  
// Function which arrange 
// the given string 
function arrangeString($str, $x, $y) 
{ 
    $count_0 = 0; 
    $count_1 = 0; 
    $len =strlen($str); 
  
    // Counting number of 0's and 
    // 1's in the given string. 
    for ( $i = 0; $i < $len; $i++) 
    { 
        if ($str[$i] == '0') 
            $count_0++; 
        else
            $count_1++; 
    } 
  
    // Printing first all 0's x-times 
    // and decrement count of 0's x-times 
    // and do the similar task with '1' 
    while ($count_0 > 0 || $count_1 > 0)  
    { 
        for ($j = 0; $j < $x &&  
             $count_0 > 0; $j++)  
        { 
            if ($count_0 > 0)  
            { 
                echo "0"; 
                $count_0--; 
            } 
        } 
        for ($j = 0; $j < $y &&  
             $count_1 > 0; $j++) 
        { 
            if ($count_1 > 0)  
            { 
                echo "1"; 
                $count_1--; 
            } 
        } 
    } 
} 
  
    // Driver Code 
    $str = "01101101101101101000000"; 
    $x = 1; 
    $y = 2; 
    arrangeString($str, $x, $y); 
  
// This code is contributed by m_kit 
?> 
```

输出：

```
01101101101101101000000
```

