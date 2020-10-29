# 数组中的唯一元素，其中除一个

> 原文：[https://www.geeksforgeeks.org/find-unique-element-element-occurs-k-times-except-one/](https://www.geeksforgeeks.org/find-unique-element-element-occurs-k-times-except-one/)

以外，所有元素均出现 k 次

给定一个包含所有元素出现 k 次的数组，但是一个数组仅出现一次。 找到那个独特的元素。

**示例**：

```
Input  : arr[] = {6, 2, 5, 2, 2, 6, 6}
            k = 3
Output : 5
Every element appears 3 times accept 5.

Input  : arr[] = {2, 2, 2, 10, 2}
            k = 4
Output : 10
Every element appears 4 times accept 10.

```

**简单解决方案**是使用两个嵌套循环。 外循环从最左边的元素开始一个接一个地选择一个元素。 内部循环检查元素是否存在 k 次。 如果存在，则忽略该元素，否则打印该元素。

上述解决方案的时间复杂度为 O（n <sup>2</sup> ）。 我们可以**使用排序**解决 O（nLogn）时间问题。 这个想法很简单，首先对数组进行排序，以便每个元素的所有出现变为连续。 一旦出现连续的情况，我们就可以遍历排序后的数组并在`O(n)`时间内打印出唯一元素。

我们可以**使用[散列](http://quiz.geeksforgeeks.org/hashing-set-1-introduction/)** 来平均解决`O(n)`时间。 这个想法是从左到右遍历给定的数组，并跟踪哈希表中的访问元素。 最后打印计数为 1 的元素。

基于哈希的解决方案需要`O(n)`额外空间。 我们可以**使用按位与**在`O(n)`时间和恒定的额外空间中找到唯一元素。

1.  创建一个数组 **count []** ，其大小等于数字的二进制表示形式的位数。

2.  填充计数数组，以便 count [i]存储设置了第 i 位的数组元素的计数。

3.  使用 count 数组形成结果。 如果 count [i]不为 k 的倍数，则将 1 放置在结果 i 中。 否则我们将 0。

## C++

```cpp

// CPP program to find unique element where 
// every element appears k times except one 
#include <bits/stdc++.h> 
using namespace std; 

int findUnique(unsigned int a[], int n, int k) 
{ 
    // Create a count array to store count of 
    // numbers that have a particular bit set. 
    // count[i] stores count of array elements 
    // with i-th bit set. 
    int INT_SIZE = 8 * sizeof(unsigned int); 
    int count[INT_SIZE]; 
    memset(count, 0, sizeof(count)); 

    // AND(bitwise) each element of the array 
    // with each set digit (one at a time) 
    // to get the count of set bits at each 
    // position 
    for (int i = 0; i < INT_SIZE; i++) 
        for (int j = 0; j < n; j++) 
            if ((a[j] & (1 << i)) != 0) 
                count[i] += 1; 

    // Now consider all bits whose count is 
    // not multiple of k to form the required 
    // number. 
    unsigned res = 0; 
    for (int i = 0; i < INT_SIZE; i++) 
        res += (count[i] % k) * (1 << i); 
    return res; 
} 

// Driver Code 
int main() 
{ 
    unsigned int a[] = { 6, 2, 5, 2, 2, 6, 6 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    int k = 3; 
    cout << findUnique(a, n, k); 
    return 0; 
} 

```

## Java

```java

// Java program to find unique element where  
// every element appears k times except one  

class GFG  
{ 

static int findUnique(int a[], int n, int k)  
{  
    // Create a count array to store count of  
    // numbers that have a particular bit set.  
    // count[i] stores count of array elements  
    // with i-th bit set.  
    byte sizeof_int = 4; 
    int INT_SIZE = 8 * sizeof_int;  
    int count[] = new int[INT_SIZE];  

    // AND(bitwise) each element of the array  
    // with each set digit (one at a time)  
    // to get the count of set bits at each  
    // position  
    for (int i = 0; i < INT_SIZE; i++)  
        for (int j = 0; j < n; j++)  
            if ((a[j] & (1 << i)) != 0)  
                count[i] += 1;  

    // Now consider all bits whose count is  
    // not multiple of k to form the required  
    // number.  
    int res = 0;  
    for (int i = 0; i < INT_SIZE; i++)  
        res += (count[i] % k) * (1 << i);  
    return res;  
}  

// Driver Code  
public static void main(String[] args)  
{ 
    int a[] = { 6, 2, 5, 2, 2, 6, 6 };  
    int n = a.length;  
    int k = 3;  
    System.out.println(findUnique(a, n, k)); 
} 
}  

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python 3 program to find unique element where 
# every element appears k times except one 
import sys 

def findUnique(a, n, k): 

    # Create a count array to store count of 
    # numbers that have a particular bit set. 
    # count[i] stores count of array elements 
    # with i-th bit set. 
    INT_SIZE = 8 * sys.getsizeof(int) 
    count = [0] * INT_SIZE 

    # AND(bitwise) each element of the array 
    # with each set digit (one at a time) 
    # to get the count of set bits at each 
    # position 
    for i in range(INT_SIZE): 
        for j in range(n): 
            if ((a[j] & (1 << i)) != 0): 
                count[i] += 1

    # Now consider all bits whose count is 
    # not multiple of k to form the required 
    # number. 
    res = 0
    for i in range(INT_SIZE): 
        res += (count[i] % k) * (1 << i) 
    return res 

# Driver Code 
if __name__ == '__main__': 
    a = [6, 2, 5, 2, 2, 6, 6] 
    n = len(a) 
    k = 3
    print(findUnique(a, n, k)); 

# This code is contributed by 
# Surendra_Gangwar 

```

## C#

```cs

// C# program to find unique element where  
// every element appears k times except one  
using System; 

class GFG  
{ 
static int findUnique(int []a, int n, int k)  
{  
    // Create a count array to store count of  
    // numbers that have a particular bit set.  
    // count[i] stores count of array elements  
    // with i-th bit set.  
    byte sizeof_int = 4; 
    int INT_SIZE = 8 * sizeof_int;  
    int []count = new int[INT_SIZE];  

    // AND(bitwise) each element of the array  
    // with each set digit (one at a time)  
    // to get the count of set bits at each  
    // position  
    for (int i = 0; i < INT_SIZE; i++)  
        for (int j = 0; j < n; j++)  
            if ((a[j] & (1 << i)) != 0)  
                count[i] += 1;  

    // Now consider all bits whose count is  
    // not multiple of k to form the required  
    // number.  
    int res = 0;  
    for (int i = 0; i < INT_SIZE; i++)  
        res += (count[i] % k) * (1 << i);  
    return res;  
}  

// Driver Code  
public static void Main(String[] args)  
{ 
    int []a = { 6, 2, 5, 2, 2, 6, 6 };  
    int n = a.Length;  
    int k = 3;  
    Console.WriteLine(findUnique(a, n, k)); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

## PHP

```php

<?php 
//PHP program to find unique element where  
// every element appears k times except one  

function findUnique($a, $n, $k)  
{  
    // Create a count array to store count of  
    // numbers that have a particular bit set.  
    // count[i] stores count of array elements  
    // with i-th bit set.  
    $INT_SIZE = 8 * PHP_INT_SIZE;  
    $count = array();  

    for($i=0; $i< $INT_SIZE; $i++) 
    $count[$i] = 0; 
    // AND(bitwise) each element of the array  
    // with each set digit (one at a time)  
    // to get the count of set bits at each  
    // position  
    for ( $i = 0; $i < $INT_SIZE; $i++)  
        for ( $j = 0; $j < $n; $j++)  
            if (($a[$j] & (1 << $i)) != 0)  
                $count[$i] += 1;  

    // Now consider all bits whose count is  
    // not multiple of k to form the required  
    // number.  
    $res = 0;  
    for ($i = 0; $i < $INT_SIZE; $i++)  
        $res += ($count[$i] % $k) * (1 << $i);  
    return $res;  
}  

    // Driver Code  
    $a = array( 6, 2, 5, 2, 2, 6, 6 );  
    $n = count($a);  
    $k = 3;  
    echo findUnique($a, $n, $k);  

// This code is contributed by Rajput-Ji 
?> 

```

**输出**：

```
5

```

本文由 **Dhiman Mayank** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

