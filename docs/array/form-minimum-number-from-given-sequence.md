# 从给定序列中形成最小数

> 原文： [https://www.geeksforgeeks.org/form-minimum-number-from-given-sequence/](https://www.geeksforgeeks.org/form-minimum-number-from-given-sequence/)

给定一个仅包含`I`和`D`的模式。 `I`用于增加， `D`用于减少。 设计一种算法以按照该模式打印最小数量。 1 到 9 的数字不能重复。

**示例**：

```
   Input: D        Output: 21
   Input: I        Output: 12
   Input: DD       Output: 321
   Input: II       Output: 123
   Input: DIDI     Output: 21435
   Input: IIDDD    Output: 126543
   Input: DDIDDIID Output: 321654798 

```

资料来源：[亚马逊面试问题](https://www.geeksforgeeks.org/amazon-interview-experience-set-241-1-5-years-experience/)

[](https://practice.geeksforgeeks.org/problem-page.php?pid=371)

## 强烈建议您在继续解决方案之前，单击这里进行练习。

以下是一些重要的观察：

由于数字不能重复，因此输出中最多可以有 9 个数字。

同样，输出中的位数比输入中的字符数多一。 请注意，输入的第一个字符对应于输出中的两位数字。

想法是遍历输入数组，并跟踪到目前为止的最后打印数字和最大打印数字。 以下是上述想法的实现。

## C++ 

```cpp

// C++ program to print minimum number that can be formed 
// from a given sequence of Is and Ds 
#include <bits/stdc++.h> 
using namespace std; 

// Prints the minimum number that can be formed from 
// input sequence of I's and D's 
void PrintMinNumberForPattern(string arr) 
{ 
    // Initialize current_max (to make sure that 
    // we don't use repeated character 
    int curr_max = 0; 

    // Initialize last_entry (Keeps track for 
    // last printed digit) 
    int last_entry = 0; 

    int j; 

    // Iterate over input array 
    for (int i=0; i<arr.length(); i++) 
    { 
        // Initialize 'noOfNextD' to get count of 
        // next D's available 
        int noOfNextD = 0; 

        switch(arr[i]) 
        { 
        case 'I': 
            // If letter is 'I' 

            // Calculate number of next consecutive D's 
            // available 
            j = i+1; 
            while (arr[j] == 'D' && j < arr.length()) 
            { 
                noOfNextD++; 
                j++; 
            } 

            if (i==0) 
            { 
                curr_max = noOfNextD + 2; 

                // If 'I' is first letter, print incremented 
                // sequence from 1 
                cout << " " << ++last_entry; 
                cout << " " << curr_max; 

                // Set max digit reached 
                last_entry = curr_max; 
            } 
            else
            { 
                // If not first letter 

                // Get next digit to print 
                curr_max = curr_max + noOfNextD + 1; 

                // Print digit for I 
                last_entry = curr_max; 
                cout << " " << last_entry; 
            } 

            // For all next consecutive 'D' print  
            // decremented sequence 
            for (int k=0; k<noOfNextD; k++) 
            { 
                cout << " " << --last_entry; 
                i++; 
            } 
            break; 

        // If letter is 'D' 
        case 'D': 
            if (i == 0) 
            { 
                // If 'D' is first letter in sequence 
                // Find number of Next D's available 
                j = i+1; 
                while (arr[j] == 'D' && j < arr.length()) 
                { 
                    noOfNextD++; 
                    j++; 
                } 

                // Calculate first digit to print based on  
                // number of consecutive D's 
                curr_max = noOfNextD + 2; 

                // Print twice for the first time 
                cout << " " << curr_max << " " << curr_max - 1; 

                // Store last entry 
                last_entry = curr_max - 1; 
            } 
            else
            { 
                // If current 'D' is not first letter 

                // Decrement last_entry 
                cout << " " << last_entry - 1; 
                last_entry--; 
            } 
            break; 
        } 
    } 
    cout << endl; 
} 

// Driver program to test above 
int main() 
{ 
    PrintMinNumberForPattern("IDID"); 
    PrintMinNumberForPattern("I"); 
    PrintMinNumberForPattern("DD"); 
    PrintMinNumberForPattern("II"); 
    PrintMinNumberForPattern("DIDI"); 
    PrintMinNumberForPattern("IIDDD"); 
    PrintMinNumberForPattern("DDIDDIID"); 
    return 0; 
} 

```

## Java

```java

// Java program to print minimum number that can be formed  
// from a given sequence of Is and Ds  
class GFG  
{ 

    // Prints the minimum number that can be formed from  
    // input sequence of I's and D's  
    static void PrintMinNumberForPattern(String arr)  
    { 
        // Initialize current_max (to make sure that  
        // we don't use repeated character  
        int curr_max = 0; 

        // Initialize last_entry (Keeps track for  
        // last printed digit)  
        int last_entry = 0; 

        int j; 

        // Iterate over input array  
        for (int i = 0; i < arr.length(); i++)  
        { 
            // Initialize 'noOfNextD' to get count of  
            // next D's available  
            int noOfNextD = 0; 

            switch (arr.charAt(i)) 
            { 
                case 'I': 
                    // If letter is 'I'  

                    // Calculate number of next consecutive D's  
                    // available  
                    j = i + 1; 
                    while (j < arr.length() && arr.charAt(j) == 'D')  
                    { 
                        noOfNextD++; 
                        j++; 
                    } 

                    if (i == 0)  
                    { 
                        curr_max = noOfNextD + 2; 

                        // If 'I' is first letter, print incremented  
                        // sequence from 1  
                        System.out.print(" " + ++last_entry); 
                        System.out.print(" " + curr_max); 

                        // Set max digit reached  
                        last_entry = curr_max; 
                    }  
                    else 
                    { 
                        // If not first letter  

                        // Get next digit to print  
                        curr_max = curr_max + noOfNextD + 1; 

                        // Print digit for I  
                        last_entry = curr_max; 
                        System.out.print(" " + last_entry); 
                    } 

                    // For all next consecutive 'D' print  
                    // decremented sequence  
                    for (int k = 0; k < noOfNextD; k++) 
                    { 
                        System.out.print(" " + --last_entry); 
                        i++; 
                    } 
                    break; 

                // If letter is 'D'  
                case 'D': 
                    if (i == 0) 
                    { 
                        // If 'D' is first letter in sequence  
                        // Find number of Next D's available  
                        j = i + 1; 
                        while (j < arr.length()&&arr.charAt(j) == 'D')  
                        { 
                            noOfNextD++; 
                            j++; 
                        } 

                        // Calculate first digit to print based on  
                        // number of consecutive D's  
                        curr_max = noOfNextD + 2; 

                        // Print twice for the first time  
                        System.out.print(" " + curr_max + " " + (curr_max - 1)); 

                        // Store last entry  
                        last_entry = curr_max - 1; 
                    }  
                    else
                    { 
                        // If current 'D' is not first letter  

                        // Decrement last_entry  
                        System.out.print(" " + (last_entry - 1)); 
                        last_entry--; 
                    } 
                    break; 
            } 
        } 
        System.out.println(); 
    } 

    // Driver code  
    public static void main(String[] args)  
    { 
        PrintMinNumberForPattern("IDID"); 
        PrintMinNumberForPattern("I"); 
        PrintMinNumberForPattern("DD"); 
        PrintMinNumberForPattern("II"); 
        PrintMinNumberForPattern("DIDI"); 
        PrintMinNumberForPattern("IIDDD"); 
        PrintMinNumberForPattern("DDIDDIID"); 
    } 
} 

// This code is contributed by Princi Singh 

```

## Python3

```py

# Python3 program to print minimum number that 
# can be formed from a given sequence of Is and Ds 

# Prints the minimum number that can be formed from 
# input sequence of I's and D's 
def PrintMinNumberForPattern(arr): 

    # Initialize current_max (to make sure that 
    # we don't use repeated character 
    curr_max = 0

    # Initialize last_entry (Keeps track for 
    # last printed digit) 
    last_entry = 0
    i = 0

    # Iterate over input array 
    while i < len(arr): 

        # Initialize 'noOfNextD' to get count of 
        # next D's available 
        noOfNextD = 0
        if arr[i] == "I": 

            # If letter is 'I' 

            # Calculate number of next consecutive D's 
            # available 
            j = i + 1
            while j < len(arr) and arr[j] == "D": 
                noOfNextD += 1
                j += 1
            if i == 0: 
                curr_max = noOfNextD + 2
                last_entry += 1

                # If 'I' is first letter, print incremented 
                # sequence from 1 
                print("", last_entry, end = "") 
                print("", curr_max, end = "") 

                # Set max digit reached 
                last_entry = curr_max 
            else: 

                # If not first letter 

                # Get next digit to print 
                curr_max += noOfNextD + 1

                # Print digit for I 
                last_entry = curr_max 
                print("", last_entry, end = "") 

            # For all next consecutive 'D' print 
            # decremented sequence 
            for k in range(noOfNextD): 
                last_entry -= 1
                print("", last_entry, end = "") 
                i += 1

        # If letter is 'D' 
        elif arr[i] == "D": 
            if i == 0: 

                # If 'D' is first letter in sequence 
                # Find number of Next D's available 
                j = i + 1
                while j < len(arr) and arr[j] == "D": 
                    noOfNextD += 1
                    j += 1

                # Calculate first digit to print based on 
                # number of consecutive D's 
                curr_max = noOfNextD + 2

                # Print twice for the first time 
                print("", curr_max, curr_max - 1, end = "") 

                # Store last entry 
                last_entry = curr_max - 1
            else: 

                # If current 'D' is not first letter 

                # Decrement last_entry 
                print("", last_entry - 1, end = "") 
                last_entry -= 1
        i += 1
    print() 

# Driver code 
if __name__ == "__main__": 
    PrintMinNumberForPattern("IDID") 
    PrintMinNumberForPattern("I") 
    PrintMinNumberForPattern("DD") 
    PrintMinNumberForPattern("II") 
    PrintMinNumberForPattern("DIDI") 
    PrintMinNumberForPattern("IIDDD") 
    PrintMinNumberForPattern("DDIDDIID") 

# This code is contributed by 
# sanjeev2552 

```

## C# 

```cs

// C# program to print minimum number that can be formed  
// from a given sequence of Is and Ds  
using System; 

class GFG  
{ 

    // Prints the minimum number that can be formed from  
    // input sequence of I's and D's  
    static void PrintMinNumberForPattern(String arr)  
    { 
        // Initialize current_max (to make sure that  
        // we don't use repeated character  
        int curr_max = 0; 

        // Initialize last_entry (Keeps track for  
        // last printed digit)  
        int last_entry = 0; 

        int j; 

        // Iterate over input array  
        for (int i = 0; i < arr.Length; i++)  
        { 
            // Initialize 'noOfNextD' to get count of  
            // next D's available  
            int noOfNextD = 0; 

            switch (arr[i]) 
            { 
                case 'I': 
                    // If letter is 'I'  

                    // Calculate number of next consecutive D's  
                    // available  
                    j = i + 1; 
                    while (j < arr.Length && arr[j] == 'D')  
                    { 
                        noOfNextD++; 
                        j++; 
                    } 

                    if (i == 0)  
                    { 
                        curr_max = noOfNextD + 2; 

                        // If 'I' is first letter, print incremented  
                        // sequence from 1  
                        Console.Write(" " + ++last_entry); 
                        Console.Write(" " + curr_max); 

                        // Set max digit reached  
                        last_entry = curr_max; 
                    }  
                    else
                    { 
                        // If not first letter  

                        // Get next digit to print  
                        curr_max = curr_max + noOfNextD + 1; 

                        // Print digit for I  
                        last_entry = curr_max; 
                        Console.Write(" " + last_entry); 
                    } 

                    // For all next consecutive 'D' print  
                    // decremented sequence  
                    for (int k = 0; k < noOfNextD; k++) 
                    { 
                        Console.Write(" " + --last_entry); 
                        i++; 
                    } 
                    break; 

                // If letter is 'D'  
                case 'D': 
                    if (i == 0) 
                    { 
                        // If 'D' is first letter in sequence  
                        // Find number of Next D's available  
                        j = i + 1; 
                        while (j < arr.Length&&arr[j] == 'D')  
                        { 
                            noOfNextD++; 
                            j++; 
                        } 

                        // Calculate first digit to print based on  
                        // number of consecutive D's  
                        curr_max = noOfNextD + 2; 

                        // Print twice for the first time  
                        Console.Write(" " + curr_max + " " + (curr_max - 1)); 

                        // Store last entry  
                        last_entry = curr_max - 1; 
                    }  
                    else
                    { 
                        // If current 'D' is not first letter  

                        // Decrement last_entry  
                        Console.Write(" " + (last_entry - 1)); 
                        last_entry--; 
                    } 
                    break; 
            } 
        } 
        Console.WriteLine(); 
    } 

    // Driver code  
    public static void Main(String[] args)  
    { 
        PrintMinNumberForPattern("IDID"); 
        PrintMinNumberForPattern("I"); 
        PrintMinNumberForPattern("DD"); 
        PrintMinNumberForPattern("II"); 
        PrintMinNumberForPattern("DIDI"); 
        PrintMinNumberForPattern("IIDDD"); 
        PrintMinNumberForPattern("DDIDDIID"); 
    } 
} 

// This code is contributed by Princi Singh 

```

## PHP

```php

<?php 
// PHP program to print minimum 
// number that can be formed 
// from a given sequence of  
// Is and Ds 

// Prints the minimum number  
// that can be formed from 
// input sequence of I's and D's 
function PrintMinNumberForPattern($arr) 
{ 
    // Initialize current_max  
    // (to make sure that 
    // we don't use repeated  
    // character 
    $curr_max = 0; 

    // Initialize last_entry  
    // (Keeps track for 
    // last printed digit) 
    $last_entry = 0; 

    $j; 

    // Iterate over 
    // input array 
    for ($i = 0; $i < strlen($arr); $i++) 
    { 
        // Initialize 'noOfNextD' 
        // to get count of 
        // next D's available 
        $noOfNextD = 0; 

        switch($arr[$i]) 
        { 
        case 'I': 
            // If letter is 'I' 

            // Calculate number of  
            // next consecutive D's 
            // available 
            $j = $i + 1; 
            while ($arr[$j] == 'D' &&  
                   $j < strlen($arr)) 
            { 
                $noOfNextD++; 
                $j++; 
            } 

            if ($i == 0) 
            { 
                $curr_max = $noOfNextD + 2; 

                // If 'I' is first letter,  
                // print incremented 
                // sequence from 1 
                echo " " , ++$last_entry; 
                echo " " , $curr_max; 

                // Set max  
                // digit reached 
                $last_entry = $curr_max; 
            } 
            else
            { 
                // If not first letter 

                // Get next digit 
                // to print 
                $curr_max = $curr_max +  
                            $noOfNextD + 1; 

                // Print digit for I 
                $last_entry = $curr_max; 
                echo " " , $last_entry; 
            } 

            // For all next consecutive 'D'  
            // print decremented sequence 
            for ($k = 0; $k < $noOfNextD; $k++) 
            { 
                echo " " , --$last_entry; 
                $i++; 
            } 
            break; 

        // If letter is 'D' 
        case 'D': 
            if ($i == 0) 
            { 
                // If 'D' is first letter  
                // in sequence. Find number 
                // of Next D's available 
                $j = $i+1; 
                while (($arr[$j] == 'D') &&  
                       ($j < strlen($arr))) 
                { 
                    $noOfNextD++; 
                    $j++; 
                } 

                // Calculate first digit  
                // to print based on  
                // number of consecutive D's 
                $curr_max = $noOfNextD + 2; 

                // Print twice for 
                // the first time 
                echo " " , $curr_max ,  
                     " " ,$curr_max - 1; 

                // Store last entry 
                $last_entry = $curr_max - 1; 
            } 
            else
            { 
                // If current 'D'  
                // is not first letter 

                // Decrement last_entry 
                echo " " , $last_entry - 1; 
                $last_entry--; 
            } 
            break; 
        } 
    } 

echo "\n"; 
} 

// Driver Code 
PrintMinNumberForPattern("IDID"); 
PrintMinNumberForPattern("I"); 
PrintMinNumberForPattern("DD"); 
PrintMinNumberForPattern("II"); 
PrintMinNumberForPattern("DIDI"); 
PrintMinNumberForPattern("IIDDD"); 
PrintMinNumberForPattern("DDIDDIID"); 

// This code is contributed by aj_36 
?> 

```

**输出**：

```
 1 3 2 5 4
 1 2
 3 2 1
 1 2 3
 2 1 4 3 5
 1 2 6 5 4 3
 3 2 1 6 5 4 7 9 8

```

Swapnil Trambake 建议此解决方案。

**替代解决方案**：

让我们观察一下最小数量的一些事实：

*   这些数字不能重复，因此输出最多可以有 9 个数字。

*   为了在输出的每个索引处形成一个最小数量，我们对可以放置在该索引上的最小数量感兴趣。

想法是遍历整个输入数组，跟踪可放置在输出的那个位置的最小数字（1-9）。

当然，棘手的部分是在索引不是 0 的位置遇到`D`时发生的。在这种情况下，我们必须跟踪`D`左侧最接近的`I`，并在输出向量中`I`和`D`之间的每个数字增加 1。

我们介绍了以下基本情况：

*   如果输入的第一个字符是`I`，那么我们将在输出向量中追加 1 和 2，并将最小可用数字设置为 3。将最新的`I`的索引设置为 1。

*   如果输入的第一个字符为`D`，则我们在输出向量中附加 2 和 1，最小可用数字设置为 3，而最新的`D`的索引设置为 0。

现在，我们将输入字符串从索引 1 迭代到结束，并：

*   如果扫描的字符为`I`，则尚未使用的最小值附加到输出矢量上。我们将最小数字的值增加。 可用，最近的`I`的索引也会更新。

*   如果在输入数组的索引`i`处扫描的字符为`D`，则在输出中将输出向量中的第`i`个元素附加到输出中，并跟踪最接近`D`左侧的`I`，并将输出向量中`I`和`D`之间的每个数字加 1。

以下是相同的程序：

## C++

```cpp

// C++ program to print minimum number that can be formed 
// from a given sequence of Is and Ds 
#include<bits/stdc++.h> 
using namespace std; 

void printLeast(string arr) 
{ 
    // min_avail represents the minimum number which is 
    // still available for inserting in the output vector. 
    // pos_of_I keeps track of the most recent index 
    // where 'I' was encountered w.r.t the output vector 
    int min_avail = 1, pos_of_I = 0; 

    //vector to store the output 
    vector<int>v; 

    // cover the base cases 
    if (arr[0]=='I') 
    { 
        v.push_back(1); 
        v.push_back(2); 
        min_avail = 3; 
        pos_of_I = 1; 
    } 
    else
    { 
        v.push_back(2); 
        v.push_back(1); 
        min_avail = 3; 
        pos_of_I = 0; 
    } 

    // Traverse rest of the input 
    for (int i=1; i<arr.length(); i++) 
    { 
        if (arr[i]=='I') 
        { 
            v.push_back(min_avail); 
            min_avail++; 
            pos_of_I = i+1; 
        } 
        else
        { 
            v.push_back(v[i]); 
            for (int j=pos_of_I; j<=i; j++) 
                v[j]++; 

            min_avail++; 
        } 
    } 

    // print the number 
    for (int i=0; i<v.size(); i++) 
        cout << v[i] << " "; 
    cout << endl; 
} 

// Driver program to check the above function 
int main() 
{ 
    printLeast("IDID"); 
    printLeast("I"); 
    printLeast("DD"); 
    printLeast("II"); 
    printLeast("DIDI"); 
    printLeast("IIDDD"); 
    printLeast("DDIDDIID"); 
    return 0; 
} 

```

## Java

```java
// Java program to print minimum number that can be formed  
// from a given sequence of Is and Ds  
import java.io.*; 
import java.util.*; 
public class GFG { 
  
       static void printLeast(String arr) 
       { 
              // min_avail represents the minimum number which is  
              // still available for inserting in the output vector.  
              // pos_of_I keeps track of the most recent index  
              // where 'I' was encountered w.r.t the output vector  
              int min_avail = 1, pos_of_I = 0;  
  
              //vector to store the output 
              ArrayList<Integer> al = new ArrayList<>(); 
                
              // cover the base cases 
              if (arr.charAt(0) == 'I')  
              {  
                  al.add(1);  
                  al.add(2);  
                  min_avail = 3;  
                  pos_of_I = 1;  
              }  
  
              else
              { 
                  al.add(2); 
                  al.add(1); 
                  min_avail = 3;  
                  pos_of_I = 0;  
              } 
  
              // Traverse rest of the input 
              for (int i = 1; i < arr.length(); i++) 
              { 
                   if (arr.charAt(i) == 'I') 
                   { 
                       al.add(min_avail); 
                       min_avail++; 
                       pos_of_I = i + 1; 
                   } 
                   else
                   { 
                       al.add(al.get(i)); 
                       for (int j = pos_of_I; j <= i; j++) 
                            al.set(j, al.get(j) + 1); 
  
                       min_avail++; 
                   } 
              } 
  
              // print the number 
              for (int i = 0; i < al.size(); i++) 
                   System.out.print(al.get(i) + " "); 
              System.out.println(); 
       } 
  
  
       // Driver code 
       public static void main(String args[]) 
       { 
              printLeast("IDID");  
              printLeast("I");  
              printLeast("DD");  
              printLeast("II");  
              printLeast("DIDI");  
              printLeast("IIDDD");  
              printLeast("DDIDDIID");  
       } 
} 
// This code is contributed by rachana soma 
```

## C#

```cs
// C# program to print minimum number that can be formed  
// from a given sequence of Is and Ds  
using System; 
using System.Collections.Generic;  
  
class GFG  
{ 
      
static void printLeast(String arr) 
{ 
    // min_avail represents the minimum number which is  
    // still available for inserting in the output vector.  
    // pos_of_I keeps track of the most recent index  
    // where 'I' was encountered w.r.t the output vector  
    int min_avail = 1, pos_of_I = 0;  
  
    //vector to store the output 
    List<int> al = new List<int>(); 
          
    // cover the base cases 
    if (arr[0] == 'I')  
    {  
        al.Add(1);  
        al.Add(2);  
        min_avail = 3;  
        pos_of_I = 1;  
    }  
  
    else
    { 
        al.Add(2); 
        al.Add(1); 
        min_avail = 3;  
        pos_of_I = 0;  
    } 
  
    // Traverse rest of the input 
    for (int i = 1; i < arr.Length; i++) 
    { 
        if (arr[i] == 'I') 
        { 
            al.Add(min_avail); 
            min_avail++; 
            pos_of_I = i + 1; 
        } 
        else
        { 
            al.Add(al[i]); 
            for (int j = pos_of_I; j <= i; j++) 
                al[j] = al[j] + 1; 
  
            min_avail++; 
        } 
    } 
  
    // print the number 
    for (int i = 0; i < al.Count; i++) 
        Console.Write(al[i] + " "); 
    Console.WriteLine(); 
} 
  
  
// Driver code 
public static void Main(String []args) 
{ 
    printLeast("IDID");  
    printLeast("I");  
    printLeast("DD");  
    printLeast("II");  
    printLeast("DIDI");  
    printLeast("IIDDD");  
    printLeast("DDIDDIID");  
} 
} 
  
// This code is contributed by Rajput-Ji 
```

输出：

```
1 3 2 5 4 
1 2 
3 2 1 
1 2 3 
2 1 4 3 5 
1 2 6 5 4 3 
3 2 1 6 5 4 7 9 8 
```

该解决方案由 Ashutosh Kumar 建议。

方法 3：

我们可以做到的是，当遇到I时，数字按升序排列，但是如果遇到`D`，我们希望数字按降序排列。 输出字符串的长度总是比输入字符串大一。 因此循环是从 0 到字符串的长度。 我们必须取 1-9 之间的数字，因此我们总是将`i + 1`压入堆栈。 然后我们检查指定索引处的结果字符是什么。因此，将出现以下两种情况：

+  情况 1：如果遇到`I`或我们位于输入字符串的最后一个字符，则从堆栈中弹出，并将其添加到输出字符串的末尾，直到堆栈变空。
+  情况 2：如果遇到`D`，那么我们希望数字按降序排列，因此我们只需将`i + 1`压入堆栈。

## C++

```cpp
// C++ program to print minimum number that can be formed 
// from a given sequence of Is and Ds 
#include <bits/stdc++.h> 
using namespace std; 
  
// Function to decode the given sequence to construct 
// minimum number without repeated digits 
void PrintMinNumberForPattern(string seq) 
{ 
    // result store output string 
    string result; 
  
    // create an empty stack of integers 
    stack<int> stk; 
  
    // run n+1 times where n is length of input sequence 
    for (int i = 0; i <= seq.length(); i++) 
    { 
        // push number i+1 into the stack 
        stk.push(i + 1); 
  
        // if all characters of the input sequence are 
        // processed or current character is 'I' 
        // (increasing) 
        if (i == seq.length() || seq[i] == 'I') 
        { 
            // run till stack is empty 
            while (!stk.empty()) 
            { 
                // remove top element from the stack and 
                // add it to solution 
                result += to_string(stk.top()); 
                result += " "; 
                stk.pop(); 
            } 
        } 
    } 
  
    cout << result << endl; 
} 
  
// main function 
int main() 
{ 
    PrintMinNumberForPattern("IDID"); 
    PrintMinNumberForPattern("I"); 
    PrintMinNumberForPattern("DD"); 
    PrintMinNumberForPattern("II"); 
    PrintMinNumberForPattern("DIDI"); 
    PrintMinNumberForPattern("IIDDD"); 
    PrintMinNumberForPattern("DDIDDIID"); 
    return 0; 
} 
```

## Java

```java
import java.util.Stack; 
  
// Java program to print minimum number that can be formed 
// from a given sequence of Is and Ds 
class GFG { 
  
// Function to decode the given sequence to construct 
// minimum number without repeated digits 
    static void PrintMinNumberForPattern(String seq) { 
        // result store output string 
        String result = ""; 
  
        // create an empty stack of integers 
        Stack<Integer> stk = new Stack<Integer>(); 
  
        // run n+1 times where n is length of input sequence 
        for (int i = 0; i <= seq.length(); i++) { 
            // push number i+1 into the stack 
            stk.push(i + 1); 
  
            // if all characters of the input sequence are 
            // processed or current character is 'I' 
            // (increasing) 
            if (i == seq.length() || seq.charAt(i) == 'I') { 
                // run till stack is empty 
                while (!stk.empty()) { 
                    // remove top element from the stack and 
                    // add it to solution 
                    result += String.valueOf(stk.peek()); 
                    result += " "; 
                    stk.pop(); 
                } 
            } 
        } 
  
        System.out.println(result); 
    } 
  
// main function 
    public static void main(String[] args) { 
        PrintMinNumberForPattern("IDID"); 
        PrintMinNumberForPattern("I"); 
        PrintMinNumberForPattern("DD"); 
        PrintMinNumberForPattern("II"); 
        PrintMinNumberForPattern("DIDI"); 
        PrintMinNumberForPattern("IIDDD"); 
        PrintMinNumberForPattern("DDIDDIID"); 
    } 
} 
// This code is contributed by PrinciRaj1992  
```

## Python3

```py
# Python3 program to print minimum  
# number that can be formed from a 
# given sequence of Is and Ds  
def PrintMinNumberForPattern(Strr): 
      
    # Take a List to work as Stack 
    stack = [] 
  
    # String for storing result  
    res = '' 
  
    # run n+1 times where n is length  
    # of input sequence, As length of 
    # result string is always 1 greater 
    for i in range(len(Strr) + 1): 
  
        # Push number i+1 into the stack 
        stack.append(i + 1) 
  
        # If all characters of the input 
        # sequence are processed or current 
        # character is 'I  
        if (i == len(Strr) or Strr[i] == 'I'): 
  
            # Run While Loop Untill stack is empty 
            while len(stack) > 0: 
                  
                # pop the element on top of stack  
                # And store it in result String 
                res += str(stack.pop()) 
                res += ' '
                  
    # Print the result 
    print(res)  
  
# Driver Code 
PrintMinNumberForPattern("IDID") 
PrintMinNumberForPattern("I") 
PrintMinNumberForPattern("DD") 
PrintMinNumberForPattern("II") 
PrintMinNumberForPattern("DIDI") 
PrintMinNumberForPattern("IIDDD") 
PrintMinNumberForPattern("DDIDDIID") 
  
# This code is contributed by AyushManglani 
```

## C#

```cs
// C# program to print minimum number that can be formed 
// from a given sequence of Is and Ds 
using System; 
using System.Collections; 
public class GFG { 
   
// Function to decode the given sequence to construct 
// minimum number without repeated digits 
    static void PrintMinNumberForPattern(String seq) { 
        // result store output string 
        String result = ""; 
   
        // create an empty stack of integers 
        Stack stk = new Stack(); 
   
        // run n+1 times where n is length of input sequence 
        for (int i = 0; i <= seq.Length; i++) { 
            // push number i+1 into the stack 
            stk.Push(i + 1); 
   
            // if all characters of the input sequence are 
            // processed or current character is 'I' 
            // (increasing) 
            if (i == seq.Length || seq[i] == 'I') { 
                // run till stack is empty 
                while (stk.Count!=0) { 
                    // remove top element from the stack and 
                    // add it to solution 
                    result += String.Join("",stk.Peek()); 
                    result += " "; 
                    stk.Pop(); 
                } 
            } 
        } 
   
        Console.WriteLine(result); 
    } 
   
// main function 
    public static void Main() { 
        PrintMinNumberForPattern("IDID"); 
        PrintMinNumberForPattern("I"); 
        PrintMinNumberForPattern("DD"); 
        PrintMinNumberForPattern("II"); 
        PrintMinNumberForPattern("DIDI"); 
        PrintMinNumberForPattern("IIDDD"); 
        PrintMinNumberForPattern("DDIDDIID"); 
    } 
} 
// This code is contributed by 29AjayKumar 
```

输出：

```
1 3 2 5 4 
1 2 
3 2 1 
1 2 3 
2 1 4 3 5 
1 2 6 5 4 3 
3 2 1 6 5 4 7 9 8 
```

时间复杂度：`O(n)`。

辅助空间：`O(n)`。