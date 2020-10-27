# 具有唯一（或不同）数字的数字

给定范围，请打印所有具有唯一数字的数字。

**示例：**

```
Input : 10 20
Output : 10 12 13 14 15 16 17 18 19 20  (Except 11)

Input : 1 10
Output : 1 2 3 4 5 6 7 8 9 10

```

```
As the problem is pretty simple, the only thing to be done is :-
1- Find the digits one by one and keep marking visited digits.
2- If all digits occurs one time only then print that number.
3- Else not.

```

## C++

```cpp

// C++ implementation to find unique digit 
// numbers in a range 
#include<bits/stdc++.h> 
using namespace std; 

// Function to print unique digit numbers 
// in range from l to r. 
void printUnique(int l, int r) 
{ 
    // Start traversing the numbers 
    for (int i=l ; i<=r ; i++) 
    { 
        int num = i; 
        bool visited[10] = {false}; 

        // Find digits and maintain its hash 
        while (num) 
        { 
            // if a digit occurs more than 1 time 
            // then break 
            if (visited[num % 10]) 
                break; 

            visited[num%10] = true; 

            num = num/10; 
        } 

        // num will be 0 only when above loop 
        // doesn't get break that means the 
        // number is unique so print it. 
        if (num == 0) 
            cout << i << " "; 
    } 
} 

// Driver code 
int main() 
{ 
    int l = 1, r = 20; 
    printUnique(l, r); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find unique digit 
// numbers in a range 
class Test 
{ 
    // Method to print unique digit numbers 
    // in range from l to r. 
    static void printUnique(int l, int r) 
    { 
        // Start traversing the numbers 
        for (int i=l ; i<=r ; i++) 
        { 
            int num = i; 
            boolean visited[] = new boolean[10]; 

            // Find digits and maintain its hash 
            while (num != 0) 
            { 
                // if a digit occurs more than 1 time 
                // then break 
                if (visited[num % 10]) 
                    break; 

                visited[num%10] = true; 

                num = num/10; 
            } 

            // num will be 0 only when above loop 
            // doesn't get break that means the 
            // number is unique so print it. 
            if (num == 0) 
                System.out.print(i + " "); 
        } 
    } 

    // Driver method 
    public static void main(String args[]) 
    { 
        int l = 1, r = 20; 
        printUnique(l, r); 
    } 
} 

```

## Python3

```py

# Python3 implementation 
# to find unique digit 
# numbers in a range 

# Function to print 
# unique digit numbers 
# in range from l to r. 
def printUnique(l,r): 

    # Start traversing 
    # the numbers 
    for i in range (l, r + 1): 
        num = i; 
        visited = [0,0,0,0,0,0,0,0,0,0]; 

        # Find digits and 
        # maintain its hash 
        while (num): 

            # if a digit occurs  
            # more than 1 time  
            # then break 
            if visited[num % 10] == 1: 
                break; 
            visited[num % 10] = 1; 
            num = (int)(num / 10); 

        # num will be 0 only when  
        # above loop doesn't get  
        # break that means the  
        # number is unique so  
        # print it. 
        if num == 0: 
            print(i, end = " "); 

# Driver code 
l = 1; 
r = 20; 
printUnique(l, r); 

# This code is 
# contributed by mits 

```

## C#

```cs

// C# implementation to find unique digit 
// numbers in a range 
using System; 

public class GFG { 

    // Method to print unique digit numbers 
    // in range from l to r. 
    static void printUnique(int l, int r) 
    { 

        // Start traversing the numbers 
        for (int i = l ; i <= r ; i++) 
        { 
            int num = i; 
            bool []visited = new bool[10]; 

            // Find digits and maintain 
            // its hash 
            while (num != 0) 
            { 

                // if a digit occurs more 
                // than 1 time then break 
                if (visited[num % 10]) 
                    break; 

                visited[num % 10] = true; 

                num = num / 10; 
            } 

            // num will be 0 only when 
            // above loop doesn't get 
            // break that means the number 
            // is unique so print it. 
            if (num == 0) 
                Console.Write(i + " "); 
        } 
    } 

    // Driver method 
    public static void Main() 
    { 
        int l = 1, r = 20; 
        printUnique(l, r); 
    } 
} 

// This code is contributed by Sam007\. 

```

## PHP

```php

<?php 
// PHP implementation to find unique  
// digit numbers in a range 

// Function to print unique digit  
// numbers in range from l to r. 
function printUnique($l, $r) 
{ 
    // Start traversing the numbers 
    for ($i = $l ; $i <= $r; $i++) 
    { 
        $num = $i; 
        $visited = (false); 

        // Find digits and  
        // maintain its hash 
        while ($num) 
        { 
            // if a digit occurs more  
            // than 1 time then break 
            if ($visited[$num % 10]) 

            $visited[$num % 10] = true; 

            $num = (int)$num / 10; 
        } 

        // num will be 0 only when above  
        // loop doesn't get break that  
        // means the number is unique 
        // so print it. 
        if ($num == 0) 
            echo $i , " "; 
    } 
} 

// Driver code 
$l = 1; $r = 20; 
printUnique($l, $r); 

// This code is contributed by aj_36 
?> 

```

**Output :**

```
1 2 3 4 5 6 7 8 9 10 12 13 14 15 16 17 18 19 20

```

本文由 **[Sahil Chhabra](https://www.facebook.com/sahil.chhabra.965)** 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

