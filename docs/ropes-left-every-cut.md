# 每次取下最小的钢丝绳后剩下的钢丝绳

> 原文： [https://www.geeksforgeeks.org/ropes-left-every-cut/](https://www.geeksforgeeks.org/ropes-left-every-cut/)

给定一个大小为`N`的整数数组。数组包含`N`条长度为`Ropes[i]`的绳索。 您必须对绳索进行切割操作，以使所有绳索均减小最小绳索的长度。 显示每次切割后剩余的绳索数量。 进行操作，直到每条绳索的长度变为零。

注意：如果单次操作后没有剩余绳子，在这种情况下，我们将打印 0。

**示例**：

> 输入：`Ropes[] = {5, 1, 1, 2, 3, 5}`
> 
> 输出：`4 3 2`
> 
> 说明：在第一个操作中，最小绳索为 1，因此我们将所有长度的长度都减少 1 减少我们剩下的 4 条绳索，我们会做同样的休息。
> 
> 输入：`Ropes[] = {5, 1, 6, 9, 8, 11, 2, 2, 6, 6, 5}`
> 
> 输出：`9 7 5 3 2 1`

**简单的解决方案是**是从[0…n-1]遍历一个循环。在每次迭代中，我们首先找到最小长度的绳索。 之后，我们将所有的绳索长度减少，然后计算剩下的长度大于零的绳索。 一直执行此过程，直到所有绳索长度都大于零为止。 此解决方案的工作时间为 `O(n^2)`。

**高效解决方案**适用于`O(nlog(n))`。 首先，我们必须按照长度的增加顺序对所有绳索进行排序。 之后，我们将按照步骤进行操作。

```
//initial cutting length "min rope"  
CuttingLength = Ropes[0]
Now Traverse a loop from left to right [1...n]
 .During traverse we check that 
  is current ropes length is greater than zero or not 
 IF ( Ropes[i] - CuttingLength > 0 ) 
 .... IF Yes then all ropes to it's right side also greater than 0
 .... Print number of ropes remains (n - i)
 ....update Cutting Length by current rope length
 ...... CuttingLength = Ropes[i]          
Do the same process for the rest.

```

以下是上述想法的实现。

## C++ 

```cpp

// C++ program to print how many 
// Ropes are Left After Every Cut 
#include <bits/stdc++.h> 
using namespace std; 

// Function print how many Ropes are  
// Left AfterEvery Cutting operation 
void cuttringRopes(int Ropes[], int n) 
{ 
    // sort all Ropes in increase  
    // of there length 
    sort(Ropes, Ropes + n); 

    int singleOperation = 0; 

    // min length rope 
    int cuttingLenght = Ropes[0]; 

    // now traverse through the given 
    // Ropes in increase order of length 
    for (int i = 1; i < n; i++) 
    { 
        // After cutting if current rope length 
        // is greater than '0' that mean all 
        // ropes to it's right side are also  
        // greater than 0 
        if (Ropes[i] - cuttingLenght > 0) 
        { 
            // print number of ropes remains 
            cout << (n - i) << " "; 

            // now current rope become 
            // min length rope 
            cuttingLenght = Ropes[i]; 
            singleOperation++; 
        } 
    } 
    if (singleOperation == 0) 
        cout << "0 "; 
} 
int main() 
{ 
    int Ropes[] = { 5, 1, 1, 2, 3, 5 }; 
    int n = sizeof(Ropes) / sizeof(Ropes[0]); 
    cuttringRopes(Ropes, n); 
    return 0; 
} 

```

## Java

```
// Java program to print how many 
// Ropes are Left After Every Cut 
import java.util.*; 
import java.lang.*; 
import java.io.*; 
  
class GFG { 
      
    // function print how many Ropes are Left After 
    // Every Cutting operation 
    public static void cuttringRopes(int Ropes[], int n) 
    { 
        // sort all Ropes in increasing 
        // order of their length 
        Arrays.sort(Ropes); 
  
        int singleOperation = 0; 
  
        // min length rope 
        int cuttingLenght = Ropes[0]; 
  
        // now traverse through the given Ropes in 
        // increase order of length 
        for (int i = 1; i < n; i++) 
        { 
            // After cutting if current rope length 
            // is greater than '0' that mean all 
            // ropes to it's right side are also 
            // greater than 0 
            if (Ropes[i] - cuttingLenght > 0) 
            { 
                System.out.print(n - i + " "); 
                  
                // now current rope become  
                // min length rope 
                cuttingLenght = Ropes[i]; 
  
                singleOperation++; 
            } 
        } 
          
        // after first operation all ropes 
        // length become zero 
        if (singleOperation == 0) 
            System.out.print("0"); 
    } 
  
    public static void main(String[] arg) 
    { 
        int[] Ropes = { 5, 1, 1, 2, 3, 5 }; 
        int n = Ropes.length; 
        cuttringRopes(Ropes, n); 
    } 
}
```

## Python3

```
# Python 3 program to 
# print how many 
# Ropes are Left After 
# Every Cut 
  
# Function print how many Ropes are  
# Left AfterEvery Cutting operation 
def cuttringRopes(Ropes, n) : 
  
    # sort all Ropes in increase  
    # of there length 
    Ropes.sort() 
   
    singleOperation = 0
   
    # min length rope 
    cuttingLenght = Ropes[0] 
   
    # now traverse through the given 
    # Ropes in increase order of length 
    for i in range(1,n) : 
  
        # After cutting if current rope length 
        # is greater than '0' that mean all 
        # ropes to it's right side are also  
        # greater than 0 
        if (Ropes[i] - cuttingLenght > 0) : 
  
            # print number of ropes remains 
            print((n - i) ,end= " ") 
               
            # now current rope become 
            # min length rope 
            cuttingLenght = Ropes[i] 
            singleOperation = singleOperation + 1
          
          
    if (singleOperation == 0) : 
        print("0 ",end="") 
  
  
Ropes = [ 5, 1, 1, 2, 3, 5 ] 
n = len(Ropes) 
cuttringRopes(Ropes, n) 
  
  
  
# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to print how many 
// Ropes are Left After Every Cut 
using System; 
  
class GFG { 
      
    // function print how many Ropes are Left After 
    // Every Cutting operation 
    public static void cuttringRopes(int []Ropes, int n) 
    { 
        // sort all Ropes in increasing 
        // order of their length 
        Array.Sort(Ropes); 
  
        int singleOperation = 0; 
  
        // min length rope 
        int cuttingLenght = Ropes[0]; 
  
        // now traverse through the given Ropes in 
        // increase order of length 
        for (int i = 1; i < n; i++) 
        { 
            // After cutting if current rope length 
            // is greater than '0' that mean all 
            // ropes to it's right side are also 
            // greater than 0 
            if (Ropes[i] - cuttingLenght > 0) 
            { 
                Console.Write(n - i + " "); 
                  
                // now current rope become  
                // min length rope 
                cuttingLenght = Ropes[i]; 
  
                singleOperation++; 
            } 
        } 
          
        // after first operation all ropes 
        // length become zero 
        if (singleOperation == 0) 
            Console.Write("0"); 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[] Ropes = { 5, 1, 1, 2, 3, 5 }; 
        int n = Ropes.Length; 
        cuttringRopes(Ropes, n); 
    } 
} 
  
// This code is contributed by vt_m.
```

## php

```
<?php 
// PHP program to print how many 
// Ropes are Left After Every Cut 
  
// Function print how many Ropes are  
// Left AfterEvery Cutting operation 
function cuttringRopes($Ropes, $n) 
{ 
      
    // sort all Ropes in increase  
    // of there length 
    sort($Ropes); 
  
    $singleOperation = 0; 
  
    // min length rope 
    $cuttingLenght = $Ropes[0]; 
  
    // now traverse through the given 
    // Ropes in increase order of length 
    for ($i = 1; $i < $n; $i++) 
    { 
          
        // After cutting if current rope length 
        // is greater than '0' that mean all 
        // ropes to it's right side are also  
        // greater than 0 
        if ($Ropes[$i] - $cuttingLenght > 0) 
        { 
            // print number of ropes remains 
            echo ($n - $i). " "; 
              
            // now current rope become 
            // min length rope 
            $cuttingLenght = $Ropes[$i]; 
            $singleOperation++; 
        } 
    } 
    if ($singleOperation == 0) 
        echo "0 "; 
} 
  
    // Driver Code 
    $Ropes = array(5, 1, 1, 2, 3, 5); 
    $n = count($Ropes); 
    cuttringRopes($Ropes, $n); 
  
// This code is contributed by Sam007 
?>
```

输出：

```
4 3 2 
```

时间复杂度：`O(n long(n))`。

空间复杂度：`O(1)`。