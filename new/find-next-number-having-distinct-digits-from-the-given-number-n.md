# 查找与给定数字`N`有不同数字的下一个数字

> 原文：[https://www.geeksforgeeks.org/find-next-number-having-distinct-digits-from-the-given-number-n/](https://www.geeksforgeeks.org/find-next-number-having-distinct-digits-from-the-given-number-n/)

给定自然数`N`，任务是查找与给定数字具有不同数字的下一个数字。

**示例**：

> **输入**：`N = 19`
>
> **输出**：20
>
> **说明**：
>
> 与 19 数字不同的下一个数字是 20。
> 
> **输入**：`N = 2019`
>
> **输出**：3333
>
> **说明**：
>
> 与 2019 数字不同的下一个数字是 3333。

**方法**：的想法是使用散列来计算下一个与给定数字具有不同数字的数字：

*   创建一个哈希数组以存储数字中存在的数字，存储最高有效数字，还将数字中存在的数字的数目存储在`count`变量中

*   查找数字中不存在的，比当前最高有效位更大的最高有效位的下一个数字。

*   如果找不到下一个最高有效位，则通过增加计数来增加位数，并找到数字中不存在的 1 到 9 之间的最高有效位。

*   如果找到下一个最高有效数字，则找到下一个最小数字，该数字不在 0 到 9 之间。

*   从 1 遍历数字位数进行计数

    *   将最高有效数字乘以 10，然后加上在给定数字中不存在的十进制位。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find 
// the next distinct digits number 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find the 
// next distinct digits number 
void findNextNumber(int n) 
{ 
    int h[10] = { 0 }; 
    int i = 0, msb = n, rem = 0; 
    int next_num = -1, count = 0; 

    // Loop to find the distinct  
    // digits using hash array 
    // and the number of digits 
    while (msb > 9) { 
        rem = msb % 10; 
        h[rem] = 1; 
        msb /= 10; 
        count++; 
    } 
    h[msb] = 1; 
    count++; 

    // Loop to find the most significant 
    // distinct digit of the next number 
    for (i = msb + 1; i < 10; i++) { 
        if (h[i] == 0) { 
            next_num = i; 
            break; 
        } 
    } 

    // Condition to check if the number 
    // is possible with the same number 
    // of digits count 
    if (next_num == -1){ 
        for (i = 1; i < msb; i++){ 
            if (h[i] == 0){ 
                next_num = i; 
                count++; 
                break; 
            } 
        } 
    } 

    // Condition to check if the desired 
    // most siginificant distinct  
    // digit is found 
    if (next_num > 0){ 

        // Loop to find the minimum next digit 
        // which is not present in the number 
        for (i = 0; i < 10; i++) { 
            if (h[i] == 0) { 
                msb = i; 
                break; 
            } 
        } 

        // Computation of the number  
        for (i = 1; i < count; i++) { 
            next_num = ((next_num * 10) + msb); 
        } 

        // Condition to check if the number is  
        // greater than the given number 
        if (next_num > n) 
            cout << next_num << "\n"; 
        else
            cout << "Not Possible \n"; 
    } 
    else{ 
        cout << "Not Possible \n"; 
    } 
} 

// Driver Code 
int main() 
{ 
    int n = 2019; 
    findNextNumber(n); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find 
// the next distinct digits number 
class GFG{ 

// Function to find the 
// next distinct digits number 
static void findNextNumber(int n) 
{ 
    int h[] = new int[10]; 
    int i = 0, msb = n, rem = 0; 
    int next_num = -1, count = 0; 

    // Loop to find the distinct  
    // digits using hash array 
    // and the number of digits 
    while (msb > 9) { 
        rem = msb % 10; 
        h[rem] = 1; 
        msb /= 10; 
        count++; 
    } 
    h[msb] = 1; 
    count++; 

    // Loop to find the most significant 
    // distinct digit of the next number 
    for (i = msb + 1; i < 10; i++) { 
        if (h[i] == 0) { 
            next_num = i; 
            break; 
        } 
    } 

    // Condition to check if the number 
    // is possible with the same number 
    // of digits count 
    if (next_num == -1){ 
        for (i = 1; i < msb; i++){ 
            if (h[i] == 0){ 
                next_num = i; 
                count++; 
                break; 
            } 
        } 
    } 

    // Condition to check if the desired 
    // most siginificant distinct  
    // digit is found 
    if (next_num > 0){ 

        // Loop to find the minimum next digit 
        // which is not present in the number 
        for (i = 0; i < 10; i++) { 
            if (h[i] == 0) { 
                msb = i; 
                break; 
            } 
        } 

        // Computation of the number  
        for (i = 1; i < count; i++) { 
            next_num = ((next_num * 10) + msb); 
        } 

        // Condition to check if the number is  
        // greater than the given number 
        if (next_num > n) 
            System.out.print(next_num+ "\n"); 
        else
            System.out.print("Not Possible \n"); 
    } 
    else{ 
        System.out.print("Not Possible \n"); 
    } 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    int n = 2019; 
    findNextNumber(n); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## C#

```cs

// C# implementation to find 
// the next distinct digits number 
using System; 

class GFG{ 

    // Function to find the 
    // next distinct digits number 
    static void findNextNumber(int n) 
    { 
        int []h = new int[10]; 
        int i = 0, msb = n, rem = 0; 
        int next_num = -1, count = 0; 

        // Loop to find the distinct  
        // digits using hash array 
        // and the number of digits 
        while (msb > 9) { 
            rem = msb % 10; 
            h[rem] = 1; 
            msb /= 10; 
            count++; 
        } 
        h[msb] = 1; 
        count++; 

        // Loop to find the most significant 
        // distinct digit of the next number 
        for (i = msb + 1; i < 10; i++) { 
            if (h[i] == 0) { 
                next_num = i; 
                break; 
            } 
        } 

        // Condition to check if the number 
        // is possible with the same number 
        // of digits count 
        if (next_num == -1){ 
            for (i = 1; i < msb; i++){ 
                if (h[i] == 0){ 
                    next_num = i; 
                    count++; 
                    break; 
                } 
            } 
        } 

        // Condition to check if the desired 
        // most siginificant distinct  
        // digit is found 
        if (next_num > 0){ 

            // Loop to find the minimum next digit 
            // which is not present in the number 
            for (i = 0; i < 10; i++) { 
                if (h[i] == 0) { 
                    msb = i; 
                    break; 
                } 
            } 

            // Computation of the number  
            for (i = 1; i < count; i++) { 
                next_num = ((next_num * 10) + msb); 
            } 

            // Condition to check if the number is  
            // greater than the given number 
            if (next_num > n) 
                Console.WriteLine(next_num); 
            else
                Console.WriteLine("Not Possible"); 
        } 
        else{ 
            Console.WriteLine("Not Possible"); 
        } 
    } 

    // Driver Code 
    public static void Main(string[] args) 
    { 
        int n = 2019; 
        findNextNumber(n); 
    } 
} 

// This code is contributed by Yash_R 

```

## Python 3

```

# Python 3 implementation to find 
# the next distinct digits number 

# Function to find the 
# next distinct digits number 
def findNextNumber(n): 
    h = [0 for i in range(10)] 
    i = 0
    msb = n 
    rem = 0
    next_num = -1
    count = 0

    # Loop to find the distinct  
    # digits using hash array 
    # and the number of digits 
    while (msb > 9): 
        rem = msb % 10
        h[rem] = 1
        msb //= 10
        count += 1

    h[msb] = 1
    count += 1

    # Loop to find the most significant 
    # distinct digit of the next number 
    for i in range(msb + 1,10,1): 
        if (h[i] == 0): 
            next_num = i 
            break

    # Condition to check if the number 
    # is possible with the same number 
    # of digits count 
    if (next_num == -1): 
        for i in range(1,msb,1): 
            if (h[i] == 0): 
                next_num = i 
                count += 1
                break

    # Condition to check if the desired 
    # most siginificant distinct  
    # digit is found 
    if (next_num > 0): 

                # Loop to find the minimum next digit 
        # which is not present in the number 
        for i in range(0,10,1): 
            if (h[i] == 0): 
                msb = i 
                break

        # Computation of the number  
        for i in range(1,count,1): 
            next_num = ((next_num * 10) + msb) 

        # Condition to check if the number is  
        # greater than the given number 
        if (next_num > n): 
            print(next_num) 
        else: 
            print("Not Possible") 
    else: 
        print("Not Possible") 

# Driver Code 
if __name__ == '__main__': 
    n = 2019
    findNextNumber(n) 

# This code is contributed by Surendra_Gangwar 

```

**Output:**

```
3333

```



* * *

* * *



