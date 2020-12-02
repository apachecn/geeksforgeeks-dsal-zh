# 通过将 N 到 M 的除数连接来创建图，并找到最短路径

> 原文： [https://www.geeksforgeeks.org/create-a-graph-by-connecting-divisors-from-n-to-m-and-find-shortest-path/](https://www.geeksforgeeks.org/create-a-graph-by-connecting-divisors-from-n-to-m-and-find-shortest-path/)

给定两个自然数`N`和`M`，请使用这两个自然数建立一个[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，其关系是数字与其自身以外的最大因子相关。 任务是在创建图形后找到这两个数字之间的最短路径。

**示例**：

> **输入**：N = 6，M = 18
> **输出**：6 < – > 3 < – > 9 < – > 18
> **说明**：
> 对于 N = 6，图形的连接为：
> 6 — 3 — 1
> 对于 N = 18，图形的连接为：
> 18 — 9 — 3 — 1
> 结合以上两个图，最短路径为：
> 6 — 3 — 9 — 18
> 
> **输入**：N = 4，M = 8
> **输出**：4 < – > 8

**方法**：的想法是[找到除自身以外的每个数字中最大的因子](https://www.geeksforgeeks.org/largest-divisor-for-each-element-in-an-array-other-than-1-and-the-number-itself/)，并通过连接这些因子创建图，然后找到它们之间的最短路径。 步骤如下：

1.  找到`M`的最大公因数并将其存储并设置为`M`。
2.  现在，在`M`不等于 1 之前，请重复上述步骤，并将生成的因子存储在数组 **mfactor []** 中。
3.  以`N`为数字，重复**步骤 1** 和**步骤 2** ，并将生成的因子存储在数组 **nfactor []** 中。
4.  现在，遍历两个数组 **mfactor []** 和 **mfactor []** ，并打印最短路径。

下面是上述方法的实现：

## C ++ 14

```

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to check the number is 
// prime or not 
int isprm(int n) 
{ 
    // Base Cases 
    if (n <= 1) 
        return 0; 
    if (n <= 3) 
        return 1; 
    if (n % 2 == 0 || n % 3 == 0) 
        return 0; 

    // Iterate till [5, sqrt(N)] to 
    // detect primarility of numbers 
    for (int i = 5; i * i <= n; i = i + 6) 
        if (n % i == 0 || n % (i + 2) == 0) 
            return 0; 
    return 1; 
} 

// Function to print the shortest path 
void shortestpath(int m, int n) 
{ 
    // Use vector to store the factor 
    // of m and n 
    vector<int> mfactor, nfactor; 

    // Use map to check if largest common 
    // factor previously present or not 
    map<int, int> fre; 

    // First store m 
    mfactor.push_back(m); 
    fre[m] = 1; 

    while (m != 1) { 

        // Check whether m is prime or not 
        if (isprm(m)) { 
            mfactor.push_back(1); 
            fre[1] = 1; 
            m = 1; 
        } 

        // Largest common factor of m 
        else { 
            for (int i = 2; 
                 i <= sqrt(m); i++) { 

                // If m is divisible by i 
                if (m % i == 0) { 

                    // Store the largest 
                    // common factor 
                    mfactor.push_back(m / i); 
                    fre[m / i] = 1; 
                    m = (m / i); 
                    break; 
                } 
            } 
        } 
    } 

    // For number n 
    nfactor.push_back(n); 

    while (fre[n] != 1) { 

        // Check whether n is prime 
        if (isprm(n)) { 
            nfactor.push_back(1); 
            n = 1; 
        } 

        // Largest common factor of n 
        else { 
            for (int i = 2; 
                 i <= sqrt(n); i++) { 
                if (n % i == 0) { 

                    // Store the largest 
                    // common factor 
                    nfactor.push_back(n / i); 
                    n = (n / i); 
                    break; 
                } 
            } 
        } 
    } 

    // Print the path 
    // Print factors from m 
    for (int i = 0; 
         i < mfactor.size(); i++) { 

        // To avoid duplicate printing 
        // of same element 
        if (mfactor[i] == n) 
            break; 

        cout << mfactor[i] 
             << " <--> "; 
    } 

    // Print the factors from n 
    for (int i = nfactor.size() - 1; 
         i >= 0; i--) { 
        if (i == 0) 
            cout << nfactor[i]; 
        else
            cout << nfactor[i] 
                 << " <--> "; 
    } 
} 

// Driver Code 
int main() 
{ 
    // Given N and M 
    int m = 18, n = 19; 

    // Function Call 
    shortestpath(m, n); 
    return 0; 
} 

```

## 爪哇

```

// Java program for the above approach 
import java.util.*; 

class GFG{ 

// Function to check the number is 
// prime or not 
static int isprm(int n) 
{ 

    // Base Cases 
    if (n <= 1) 
        return 0; 
    if (n <= 3) 
        return 1; 
    if (n % 2 == 0 || n % 3 == 0) 
        return 0; 

    // Iterate till [5, Math.sqrt(N)] to 
    // detect primarility of numbers 
    for(int i = 5; i * i <= n; i = i + 6) 
        if (n % i == 0 || n % (i + 2) == 0) 
            return 0; 

    return 1; 
} 

// Function to print the shortest path 
static void shortestpath(int m, int n) 
{ 

    // Use vector to store the factor 
    // of m and n 
    Vector<Integer> mfactor = new Vector<>(); 
    Vector<Integer> nfactor = new Vector<>(); 

    // Use map to check if largest common 
    // factor previously present or not 
    HashMap<Integer, Integer> fre = new HashMap<>(); 

    // First store m 
    mfactor.add(m); 
    fre.put(m, 1); 

    while (m != 1)  
    { 

        // Check whether m is prime or not 
        if (isprm(m) != 0) 
        { 
            mfactor.add(1); 
            fre.put(1, 1); 
            m = 1; 
        } 

        // Largest common factor of m 
        else
        { 
            for(int i = 2;  
                    i <= Math.sqrt(m); i++) 
            { 

                // If m is divisible by i 
                if (m % i == 0)  
                { 

                    // Store the largest 
                    // common factor 
                    mfactor.add(m / i); 
                    fre.put(m / i, 1); 
                    m = (m / i); 
                    break; 
                } 
            } 
        } 
    } 

    // For number n 
    nfactor.add(n); 

    while (fre.containsKey(n) && fre.get(n) != 1) 
    { 

        // Check whether n is prime 
        if (isprm(n) != 0) 
        { 
            nfactor.add(1); 
            n = 1; 
        } 

        // Largest common factor of n 
        else
        { 
            for(int i = 2;  
                    i <= Math.sqrt(n); i++)  
            { 
                if (n % i == 0)  
                { 

                    // Store the largest 
                    // common factor 
                    nfactor.add(n / i); 
                    n = (n / i); 
                    break; 
                } 
            } 
        } 
    } 

    // Print the path 
    // Print factors from m 
    for(int i = 0; i < mfactor.size(); i++) 
    { 

        // To astatic void duplicate printing 
        // of same element 
        if (mfactor.get(i) == n) 
            break; 

        System.out.print(mfactor.get(i) + 
                         " <--> "); 
    } 

    // Print the factors from n 
    for(int i = nfactor.size() - 1; 
            i >= 0; i--) 
    { 
        if (i == 0) 
            System.out.print(nfactor.get(i)); 
        else
            System.out.print(nfactor.get(i) + 
                             " <--> "); 
    } 
} 

// Driver Code 
public static void main(String[] args) 
{ 

    // Given N and M 
    int m = 18, n = 19; 

    // Function call 
    shortestpath(m, n); 
} 
} 

// This code is contributed by 29AjayKumar  

```

## Python3

```

# Python3 program for the above approach 
import math 

# Function to check the number is 
# prime or not 
def isprm(n): 

    # Base Cases 
    if (n <= 1): 
        return 0
    if (n <= 3): 
        return 1
    if (n % 2 == 0 or n % 3 == 0): 
        return 0

    # Iterate till [5, sqrt(N)] to 
    # detect primarility of numbers 
    i = 5
    while i * i <= n: 
        if (n % i == 0 or n % (i + 2) == 0): 
            return 0

        i += 6

    return 1

# Function to print the shortest path 
def shortestpath(m, n): 

    # Use vector to store the factor 
    # of m and n 
    mfactor = [] 
    nfactor = [] 

    # Use map to check if largest common 
    # factor previously present or not 
    fre = dict.fromkeys(range(n + 1), 0) 

    # First store m 
    mfactor.append(m) 
    fre[m] = 1

    while (m != 1): 

        # Check whether m is prime or not 
        if (isprm(m)): 
            mfactor.append(1) 
            fre[1] = 1
            m = 1

        # Largest common factor of m 
        else: 
            sqt = (int)(math.sqrt(m)) 
            for i in range(2, sqt + 1): 

                # If m is divisible by i 
                if (m % i == 0): 

                    # Store the largest 
                    # common factor 
                    mfactor.append(m // i) 
                    fre[m // i] = 1
                    m = (m // i) 
                    break

    # For number n 
    nfactor.append(n) 

    while (fre[n] != 1): 

        # Check whether n is prime 
        if (isprm(n)): 
            nfactor.append(1) 
            n = 1

        # Largest common factor of n 
        else: 
            sqt = (int)(math.sqrt(n)) 
            for i in range(2, sqt + 1): 
                if (n % i == 0): 

                    # Store the largest 
                    # common factor 
                    nfactor.append(n // i) 
                    n = (n // i) 
                    break

    # Print the path 
    # Print factors from m 
    for i in range(len(mfactor)): 

        # To avoid duplicate printing 
        # of same element 
        if (mfactor[i] == n): 
            break

        print(mfactor[i], end = " <--> ") 

    # Print the factors from n 
    for i in range(len(nfactor) - 1, -1, -1): 
        if (i == 0): 
            print (nfactor[i], end = "") 
        else: 
            print(nfactor[i], end = " <--> ") 

# Driver Code 
if __name__ == "__main__": 

    # Given N and M 
    m = 18
    n = 19

    # Function call 
    shortestpath(m, n) 

# This code is contributed by chitranayal 

```

## C＃

```

// C# program for the above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to check the number is 
// prime or not 
static int isprm(int n) 
{ 

    // Base Cases 
    if (n <= 1) 
        return 0; 
    if (n <= 3) 
        return 1; 
    if (n % 2 == 0 || n % 3 == 0) 
        return 0; 

    // Iterate till [5, Math.Sqrt(N)] to 
    // detect primarility of numbers 
    for(int i = 5; i * i <= n; i = i + 6) 
        if (n % i == 0 || n % (i + 2) == 0) 
            return 0; 

    return 1; 
} 

// Function to print the shortest path 
static void shortestpath(int m, int n) 
{ 

    // Use vector to store the factor 
    // of m and n  
    List<int> mfactor = new List<int>(); 
    List<int> nfactor = new List<int>(); 

    // Use map to check if largest common 
    // factor previously present or not 
    Dictionary<int,  
               int> fre = new Dictionary<int, 
                                         int>(); 

    // First store m 
    mfactor.Add(m); 
    fre.Add(m, 1); 

    while (m != 1)  
    { 

        // Check whether m is prime or not 
        if (isprm(m) != 0) 
        { 
            mfactor.Add(1); 
            if(!fre.ContainsKey(1)) 
                fre.Add(1, 1); 

            m = 1; 
        } 

        // Largest common factor of m 
        else
        { 
            for(int i = 2;  
                    i <= Math.Sqrt(m); i++) 
            { 

                // If m is divisible by i 
                if (m % i == 0)  
                { 

                    // Store the largest 
                    // common factor 
                    mfactor.Add(m / i); 
                    if(!fre.ContainsKey(m/i)) 
                        fre.Add(m / i, 1); 

                    m = (m / i); 
                    break; 
                } 
            } 
        } 
    } 

    // For number n 
    nfactor.Add(n); 

    while (fre.ContainsKey(n) && fre[n] != 1) 
    { 

        // Check whether n is prime 
        if (isprm(n) != 0) 
        { 
            nfactor.Add(1); 
            n = 1; 
        } 

        // Largest common factor of n 
        else
        { 
            for(int i = 2;  
                    i <= Math.Sqrt(n); i++)  
            { 
                if (n % i == 0)  
                { 

                    // Store the largest 
                    // common factor 
                    nfactor.Add(n / i); 
                    n = (n / i); 
                    break; 
                } 
            } 
        } 
    } 

    // Print the path 
    // Print factors from m 
    for(int i = 0; i < mfactor.Count; i++) 
    { 

        // To astatic void duplicate printing 
        // of same element 
        if (mfactor[i] == n) 
            break; 

        Console.Write(mfactor[i] + 
                        " <--> "); 
    } 

    // Print the factors from n 
    for(int i = nfactor.Count - 1; 
            i >= 0; i--) 
    { 
        if (i == 0) 
            Console.Write(nfactor[i]); 
        else
            Console.Write(nfactor[i] + 
                            " <--> "); 
    } 
} 

// Driver Code 
public static void Main(String[] args) 
{ 

    // Given N and M 
    int m = 18, n = 19; 

    // Function call 
    shortestpath(m, n); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:** 

```
18 <--> 9 <--> 3 <--> 1 <--> 19

```

***时间复杂度**：O（log（max（M，N））*
***辅助空间**：O（N）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。