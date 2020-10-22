# 查找给定数组中的两个重复元素

> 原文： [https://www.geeksforgeeks.org/find-the-two-repeating-elements-in-a-given-array/](https://www.geeksforgeeks.org/find-the-two-repeating-elements-in-a-given-array/)

您将得到一个`n + 2`个元素的数组。 数组的所有元素都在 1 到`n`的范围内。 并且所有元素发生一次，除了两个数字出现两次。 找到两个重复的数字。

例如，数组= `{4, 2, 4, 5, 2, 3, 1}`，`n = 5`。

上面的数组具有`n + 2 = 7`个元素，除 2 和 4 出现两次之外，所有元素都出现一次。 因此输出应为`4 2`。



**方法 1（基本）**：

使用两个循环。 在外循环中，一一拾取元素，然后计算内循环中被拾取元素的出现次数。

此方法未使用问题中提供的其他有用数据，例如数字范围在 1 到`n`之间，并且只有两个重复元素。

## C++ 

```cpp

// C++ program to Find the two repeating  
// elements in a given array 
#include<bits/stdc++.h> 
using namespace std; 

void printRepeating(int arr[], int size) 
{ 
    int i, j; 
    printf(" Repeating elements are "); 
    for(i = 0; i < size; i++) 
        for(j = i + 1; j < size; j++) 
        if(arr[i] == arr[j]) 
            cout << arr[i] << " "; 
}  

// Driver Code 
int main() 
{ 
    int arr[] = {4, 2, 4, 5, 2, 3, 1}; 
    int arr_size = sizeof(arr)/sizeof(arr[0]);  
    printRepeating(arr, arr_size); 
} 

// This code is contributed by Shivi_Aggarwal 

```

## C

```c
#include<stdio.h> 
#include<stdlib.h> 
void printRepeating(int arr[], int size) 
{ 
  int i, j; 
  printf(" Repeating elements are "); 
  for(i = 0; i < size; i++) 
    for(j = i+1; j < size; j++) 
      if(arr[i] == arr[j]) 
        printf(" %d ", arr[i]); 
}      
  
int main() 
{ 
  int arr[] = {4, 2, 4, 5, 2, 3, 1}; 
  int arr_size = sizeof(arr)/sizeof(arr[0]);   
  printRepeating(arr, arr_size); 
  getchar(); 
  return 0; 
}
```

## Java

```java
class RepeatElement  
{ 
    void printRepeating(int arr[], int size)  
    { 
        int i, j; 
        System.out.println("Repeated Elements are :"); 
        for (i = 0; i < size; i++)  
        { 
            for (j = i + 1; j < size; j++)  
            { 
                if (arr[i] == arr[j])  
                    System.out.print(arr[i] + " "); 
            } 
        } 
    } 
  
    public static void main(String[] args)  
    { 
        RepeatElement repeat = new RepeatElement(); 
        int arr[] = {4, 2, 4, 5, 2, 3, 1}; 
        int arr_size = arr.length; 
        repeat.printRepeating(arr, arr_size); 
    } 
}
```

## Python3

```py
# Python3 program to Find the two 
# repeating elements in a given array 
  
def printRepeating(arr, size): 
  
    print("Repeating elements are ", 
                         end = '') 
    for i in range (0, size): 
        for j in range (i + 1, size): 
            if arr[i] == arr[j]: 
                print(arr[i], end = ' ') 
      
# Driver code 
arr = [4, 2, 4, 5, 2, 3, 1] 
arr_size = len(arr) 
printRepeating(arr, arr_size) 
  
# This code is contributed by Smitha Dinesh Semwal
```

## C#

```cs
using System; 
  
class GFG 
{ 
          
    static void printRepeating(int []arr, int size)  
    { 
        int i, j; 
          
        Console.Write("Repeated Elements are :"); 
        for (i = 0; i < size; i++)  
        { 
            for (j = i + 1; j < size; j++)  
            { 
                if (arr[i] == arr[j])  
                    Console.Write(arr[i] + " "); 
            } 
        } 
    } 
    // driver code 
    public static void Main()  
    { 
        int []arr = {4, 2, 4, 5, 2, 3, 1}; 
        int arr_size = arr.Length; 
          
        printRepeating(arr, arr_size); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// PHP program to Find the two  
// repeating elements in  
// a given array 
  
function printRepeating($arr, $size) 
{ 
    $i; 
    $j; 
    echo " Repeating elements are "; 
  
    for($i = 0; $i < $size; $i++) 
        for($j = $i + 1; $j < $size; $j++) 
            if($arr[$i] == $arr[$j]) 
                echo $arr[$i], " "; 
}  
  
// Driver Code 
$arr = array(4, 2, 4, 5, 2, 3, 1); 
$arr_size = sizeof($arr, 0); 
printRepeating($arr, $arr_size); 
  
// This code is contributed by Ajit 
?>
```

输出：

```
Repeating elements are 4 2
```

时间复杂度：`O(n * n)`。

辅助空间：`O(1)`。

方法 2（使用计数数组）：

遍历数组一次。 遍历时，使用大小为`n`的临时数组`count[]`跟踪数组中所有元素的计数，当您看到已设置其计数的元素时，将其打印为重复。

此方法使用问题中给定的范围来限制`count[]`的大小，但不使用只有两个重复元素的数据。

## C++

```cpp
// C++ implementation of above approach 
#include <bits/stdc++.h> 
using namespace std; 
  
void printRepeating(int arr[], int size)  
{  
    int *count = new int[sizeof(int)*(size - 2)];  
    int i;  
          
    cout << " Repeating elements are ";  
    for(i = 0; i < size; i++)  
    {  
        if(count[arr[i]] == 1)  
            cout << arr[i] << " ";  
        else
            count[arr[i]]++;  
    }  
}  
  
// Driver code 
int main()  
{  
    int arr[] = {4, 2, 4, 5, 2, 3, 1};  
    int arr_size = sizeof(arr)/sizeof(arr[0]);  
    printRepeating(arr, arr_size);  
    return 0;  
}  
  
// This is code is contributed by rathbhupendra
```

## C

```c
#include<stdio.h> 
#include<stdlib.h> 
  
void printRepeating(int arr[], int size) 
{ 
  int *count = (int *)calloc(sizeof(int), (size - 2)); 
  int i; 
    
  printf(" Repeating elements are "); 
  for(i = 0; i < size; i++) 
  {   
    if(count[arr[i]] == 1) 
      printf(" %d ", arr[i]); 
    else
     count[arr[i]]++; 
  }     
}      
  
int main() 
{ 
  int arr[] = {4, 2, 4, 5, 2, 3, 1}; 
  int arr_size = sizeof(arr)/sizeof(arr[0]);   
  printRepeating(arr, arr_size); 
  getchar(); 
  return 0; 
}
```

## Java

```java
class RepeatElement 
{ 
    void printRepeating(int arr[], int size)  
    { 
        int count[] = new int[size]; 
        int i; 
  
        System.out.println("Repeated elements are : "); 
        for (i = 0; i < size; i++)  
        { 
            if (count[arr[i]] == 1) 
                System.out.print(arr[i] + " "); 
            else
                count[arr[i]]++; 
        } 
    } 
  
    public static void main(String[] args) 
    { 
        RepeatElement repeat = new RepeatElement(); 
        int arr[] = {4, 2, 4, 5, 2, 3, 1}; 
        int arr_size = arr.length; 
        repeat.printRepeating(arr, arr_size); 
    } 
}
```

## Python3

```py
# Python3 code for Find the two repeating  
# elements in a given array 
  
  
def printRepeating(arr,size) : 
    count = [0] * size 
    print(" Repeating elements are ",end = "") 
    for i in range(0, size) : 
        if(count[arr[i]] == 1) : 
            print(arr[i], end = " ") 
        else : 
            count[arr[i]] = count[arr[i]] + 1
  
  
# Driver code 
arr = [4, 2, 4, 5, 2, 3, 1] 
arr_size = len(arr) 
printRepeating(arr, arr_size) 
  
  
          
# This code is contributed by Nikita Tiwari.
```

## C#

```cs
// C# program to Find the two 
// repeating elements in a given array 
using System; 
  
class GFG 
{ 
          
    static void printRepeating(int []arr, 
                                    int size)  
    { 
        int []count = new int[size]; 
        int i; 
  
        Console.Write("Repeated elements are: "); 
        for (i = 0; i < size; i++)  
        { 
            if (count[arr[i]] == 1) 
                Console.Write(arr[i] + " "); 
            else
                count[arr[i]]++; 
        } 
    } 
  
    // driver code 
    public static void Main() 
    { 
        int []arr = {4, 2, 4, 5, 2, 3, 1}; 
        int arr_size = arr.Length; 
          
        printRepeating(arr, arr_size); 
    } 
} 
  
//This code is contributed by Sam007
```

## PHP

```php
<?php 
// PHP program to Find the two 
// repeating elements in a given array 
function printRepeating($arr, $size)  
{  
    $count = array_fill(0, $size, 0); 
    echo "Repeated elements are "; 
    for ($i = 0; $i < $size; $i++)  
    { 
        if ($count[$arr[$i]] == 1) 
            echo $arr[$i]." "; 
        else
            $count[$arr[$i]]++; 
    } 
} 
  
// Driver code 
$arr = array(4, 2, 4, 5, 2, 3, 1); 
$arr_size = count($arr); 
  
printRepeating($arr, $arr_size); 
          
// This code is contributed by mits 
?>
```

输出：

```
Repeating elements are 4 2
```

时间复杂度：`O(n)`。

辅助空间：`O(n)`。

方法 3（两个方程式）：

令要重复的数字为`X`和`Y`。我们为X和Y制作两个方程，剩下的简单任务是求解这两个方程。
我们知道从 1 到`n`的整数之和是`n (n + 1)/ 2`，乘积是`n!`。我们计算输入数组的总和，当从`n(n + 1) / 2`减去该总和时，我们得到`X + Y`，因为`X`和`Y`是集合`[1..n]`中缺少的两个数字。类似地计算输入数组的乘积，当该乘积除以`n!`时，得到`X * Y`。给定`X`和`Y`的和与乘积，我们可以轻松找出`X`和`Y`。

令数组中所有数字的总和为`S`，乘积为`P`：

```
X + Y = S – n (n + 1) / 2
XY = P / n!
```

使用上面的两个方程式，我们可以得出`X`和`Y`。对于`array = 4 2 4 5 2 3 1`，我们得到`S = 21`，而`P`为 960。

```
X + Y = 21 – 15 = 6

XY = 960/5! = 8

X – Y = sqrt((X + Y) ^ 2 – 4 * XY) = sqrt(4) = 2
```

使用下面的两个方程式，我们可以轻松得出`X = (6 + 2) / 2`和`Y = (6 - 2) / 2`：

```
X + Y = 6
X – Y = 2
```

感谢 geek4u 建议这种方法。正如 Beginer 指出的那样，此方法可能存在加法和乘法溢出问题。

方法 3 和 4 使用问题中给出的所有有用信息🙂。

## C++

```cpp
#include <bits/stdc++.h> 
using namespace std;  
  
/* function to get factorial of n */
int fact(int n);  
  
void printRepeating(int arr[], int size)  
{  
    int S = 0; /* S is for sum of elements in arr[] */
    int P = 1; /* P is for product of elements in arr[] */
    int x, y; /* x and y are two repeating elements */
    int D; /* D is for difference of x and y, i.e., x-y*/
    int n = size - 2, i;  
      
    /* Calculate Sum and Product of all elements in arr[] */
    for(i = 0; i < size; i++)  
    {  
        S = S + arr[i];  
        P = P*arr[i];  
    }      
          
    S = S - n*(n+1)/2; /* S is x + y now */
    P = P/fact(n);     /* P is x*y now */
          
    D = sqrt(S*S - 4*P); /* D is x - y now */
          
    x = (D + S)/2;  
    y = (S - D)/2;  
          
    cout<<"The two Repeating elements are "<<x<<" & "<<y;  
}  
  
int fact(int n)  
{  
    return (n == 0)? 1 : n*fact(n-1);  
}  
  
// Driver code 
int main()  
{  
    int arr[] = {4, 2, 4, 5, 2, 3, 1};  
    int arr_size = sizeof(arr)/sizeof(arr[0]);  
    printRepeating(arr, arr_size);  
    return 0;  
}  
  
// This code is contributed by rathbhupendra
```

## C

```c
#include<stdio.h> 
#include<stdlib.h> 
#include<math.h> 
  
/* function to get factorial of n */
int fact(int n); 
  
void printRepeating(int arr[], int size) 
{ 
  int S = 0;  /* S is for sum of elements in arr[] */
  int P = 1;  /* P is for product of elements in arr[] */  
  int x,  y;   /* x and y are two repeating elements */
  int D;      /* D is for difference of x and y, i.e., x-y*/
  int n = size - 2,  i; 
  
  /* Calculate Sum and Product of all elements in arr[] */
  for(i = 0; i < size; i++) 
  { 
    S = S + arr[i]; 
    P = P*arr[i]; 
  }         
    
  S = S - n*(n+1)/2;  /* S is x + y now */
  P = P/fact(n);         /* P is x*y now */
    
  D = sqrt(S*S - 4*P); /* D is x - y now */
    
  x = (D + S)/2; 
  y = (S - D)/2; 
    
  printf("The two Repeating elements are %d & %d", x, y); 
}      
  
int fact(int n) 
{ 
   return (n == 0)? 1 : n*fact(n-1); 
}     
  
int main() 
{ 
  int arr[] = {4, 2, 4, 5, 2, 3, 1}; 
  int arr_size = sizeof(arr)/sizeof(arr[0]);   
  printRepeating(arr, arr_size); 
  getchar(); 
  return 0; 
}
```

## Java

```java
class RepeatElement 
{ 
    void printRepeating(int arr[], int size)  
    { 
        /* S is for sum of elements in arr[] */
        int S = 0; 
          
        /* P is for product of elements in arr[] */
        int P = 1; 
          
        /* x and y are two repeating elements */
        int x, y; 
          
        /* D is for difference of x and y, i.e., x-y*/
        int D; 
          
        int n = size - 2, i; 
  
        /* Calculate Sum and Product of all elements in arr[] */
        for (i = 0; i < size; i++)  
        { 
            S = S + arr[i]; 
            P = P * arr[i]; 
        } 
  
        /* S is x + y now */
        S = S - n * (n + 1) / 2; 
          
        /* P is x*y now */
        P = P / fact(n); 
         
        /* D is x - y now */
        D = (int) Math.sqrt(S * S - 4 * P); 
          
  
        x = (D + S) / 2; 
        y = (S - D) / 2; 
  
        System.out.println("The two repeating elements are :"); 
        System.out.print(x + " " + y); 
    } 
  
    int fact(int n)  
    { 
        return (n == 0) ? 1 : n * fact(n - 1); 
    } 
  
    public static void main(String[] args) { 
        RepeatElement repeat = new RepeatElement(); 
        int arr[] = {4, 2, 4, 5, 2, 3, 1}; 
        int arr_size = arr.length; 
        repeat.printRepeating(arr, arr_size); 
    } 
} 
  
// This code has been contributed by Mayank Jaiswal
```

## Python3

```py
# Python3 code for Find the two repeating  
# elements in a given array 
import math 
  
def printRepeating(arr, size) : 
      
    # S is for sum of elements in arr[]  
    S = 0;  
      
    # P is for product of elements in arr[]  
    P = 1; 
      
    n = size - 2
  
    # Calculate Sum and Product  
    # of all elements in arr[]  
    for i in range(0, size) : 
        S = S + arr[i] 
        P = P * arr[i] 
      
    # S is x + y now  
    S = S - n * (n + 1) // 2 
      
     # P is x*y now  
    P = P // fact(n)     
      
    # D is x - y now  
    D = math.sqrt(S * S - 4 * P)  
      
    x = (D + S) // 2
    y = (S - D) // 2
      
    print("The two Repeating elements are ",  
          (int)(x)," & " ,(int)(y)) 
      
  
def fact(n) : 
    if(n == 0) : 
        return 1
    else : 
        return(n * fact(n - 1)) 
  
# Driver code 
arr = [4, 2, 4, 5, 2, 3, 1] 
arr_size = len(arr)  
printRepeating(arr, arr_size) 
  
          
# This code is contributed by Nikita Tiwari.
```

## C#

```cs
using System; 
  
class GFG 
{ 
          
    static void printRepeating(int []arr, int size)  
    { 
        /* S is for sum of elements in arr[] */
        int S = 0; 
          
        /* P is for product of elements in arr[] */
        int P = 1; 
          
        /* x and y are two repeating elements */
        int x, y; 
          
        /* D is for difference of x and y, i.e., x-y*/
        int D; 
          
        int n = size - 2, i; 
  
        /* Calculate Sum and Product  
         of all elements in arr[] */
        for (i = 0; i < size; i++)  
        { 
            S = S + arr[i]; 
            P = P * arr[i]; 
        } 
  
        /* S is x + y now */
        S = S - n * (n + 1) / 2; 
          
        /* P is x*y now */
        P = P / fact(n); 
          
        /* D is x - y now */
        D = (int) Math.Sqrt(S * S - 4 * P); 
          
  
        x = (D + S) / 2; 
        y = (S - D) / 2; 
  
        Console.WriteLine("The two" +  
                " repeating elements are :"); 
        Console.Write(x + " " + y); 
    } 
  
    static int fact(int n)  
    { 
        return (n == 0) ? 1 : n * fact(n - 1); 
    } 
  
    // driver code 
    public static void Main() { 
        int []arr = {4, 2, 4, 5, 2, 3, 1}; 
        int arr_size = arr.Length; 
          
        printRepeating(arr, arr_size); 
    } 
} 
// This code is contributed by Sam007
```

## PHP

```php
<?php 
  
/* function to get factorial of n */
function fact($n){ 
    
return ($n == 0)? 1 : $n*fact($n-1); 
} 
  
function printRepeating($arr, $size) 
{ 
 $S = 0; /* S is for sum of elements in arr[] */
 $P = 1; /* P is for product of elements in arr[] */
 $x; $y; /* x and y are two repeating elements */
 $D;     /* D is for difference of x and y, i.e., x-y*/
 $n = $size - 2; 
   
  
/* Calculate Sum and Product of all elements in arr[] */
for($i = 0; $i < $size; $i++) 
{ 
    $S = $S + $arr[$i]; 
    $P = $P*$arr[$i]; 
}      
  
$S = $S - $n*($n+1)/2; /* S is x + y now */
$P = $P/fact($n);         /* P is x*y now */
  
$D = sqrt($S*$S - 4*$P); /* D is x - y now */
  
$x = ($D + $S)/2; 
$y = ($S - $D)/2; 
  
echo "The two Repeating elements are ".$x." & ".$y; 
}      
  
  
  
$arr = array(4, 2, 4, 5, 2, 3, 1); 
$arr_size = count($arr);  
printRepeating($arr, $arr_size); 
?>
```

输出：

```
Repeating elements are 4 2
```

时间复杂度：`O(n)`。

辅助空间：`O(1)`。