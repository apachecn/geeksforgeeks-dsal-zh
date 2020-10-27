# 阵列产品

的不同主要因素

给定一个整数数组，让我们说 P 是数组元素的乘积。 求出乘积 P 的不同素数的数量。

**示例：**

> 输入：1 2 3 4 5
> 输出：3
> 说明：此处 P = 1 * 2 * 3 * 4 * 5 =120。120 的不同素数是 2、3 和 5。因此，输出为 3。
> 
> 输入：21 30 15 24 16
> 输出：4
> 说明：此处 P = 21 * 30 * 15 * 24 * 16 =3628800。3628800 的不同主要除数分别是 2、3、5 和 7。 输出为 4。

**天真的方法：**
这个问题的简单解决方案是将数组中的每个数字相乘，然后找到乘积的不同素数。
但是此方法可能导致整数溢出。

**更好的方法：**
为了避免溢出而不是将数字相乘，我们可以分别找到每个元素的素因数，并将素因数存储在一组或唯一图中。

## C++

```cpp

// C++ program to count distinct prime 
// factors of a number. 
#include <bits/stdc++.h> 
using namespace std; 

// Function to count the number of distinct prime 
// factors of product of array 
int Distinct_Prime_factors(vector<int> a) 
{ 
    // use set to store distinct factors 
    unordered_set<int> m; 

    // iterate over every element of array 
    for (int i = 0; i < a.size(); i++) { 
        int sq = sqrt(a[i]); 

        // from 2 to square root of number run 
        // a loop and check the numbers which 
        // are factors. 
        for (int j = 2; j <= sq; j++) { 
            if (a[i] % j == 0) { 

                // if j is a factor store it in the set 
                m.insert(j); 

                // divide the number with j till it 
                // is divisible so that only prime factors 
                // are stored 
                while (a[i] % j == 0) { 
                    a[i] /= j; 
                } 
            } 
        } 

        // if the number is still greater than 1 then 
        // it is a prime factor, insert in set 
        if (a[i] > 1) { 
            m.insert(a[i]); 
        } 
    } 

    // the number of unique prime factors will 
    // the size of the set 
    return m.size(); 
} 

// Driver Function 
int main() 
{ 
    vector<int> a = { 1, 2, 3, 4, 5 }; 
    cout << Distinct_Prime_factors(a) << '\n'; 
    return 0; 
} 

```

## Java

```java

// Java program to count distinct 
// prime factors of a number. 
import java.util.*; 

class GFG { 

    // Function to count the number 
    // of distinct prime factors of 
    // product of array 
    static int Distinct_Prime_factors(Vector<Integer> a) 
    { 
        // use set to store distinct factors 
        HashSet<Integer> m = new HashSet<Integer>(); 

        // iterate over every element of array 
        for (int i = 0; i < a.size(); i++) { 
            int sq = (int)Math.sqrt(a.get(i)); 

            // from 2 to square root of number 
            // run a loop and check the numbers 
            // which are factors. 
            for (int j = 2; j <= sq; j++) { 
                if (a.get(i) % j == 0) { 

                    // if j is a factor store 
                    // it in the set 
                    m.add(j); 

                    // divide the number with j 
                    // till it is divisible so 
                    // that only prime factors 
                    // are stored 
                    while (a.get(i) % j == 0) { 
                        a.set(i, a.get(i) / j); 
                    } 
                } 
            } 

            // if the number is still greater 
            // than 1 then it is a prime factor, 
            // insert in set 
            if (a.get(i) > 1) { 
                m.add(a.get(i)); 
            } 
        } 

        // the number of unique prime 
        // factors will the size of the set 
        return m.size(); 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        Vector<Integer> a = new Vector<Integer>(); 
        a.add(1); 
        a.add(2); 
        a.add(3); 
        a.add(4); 
        a.add(5); 
        System.out.println(Distinct_Prime_factors(a)); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to count distinct  
# prime factors of a number 
import math 

# Function to count the number of distinct  
# prime factors of product of array 
def Distinct_Prime_factors( a): 

    # use set to store distinct factors 
    m = [] 

    # iterate over every element of array 
    for i in range (len(a)) : 
        sq = int(math.sqrt(a[i])) 

        # from 2 to square root of number run  
        # a loop and check the numbers which 
        # are factors. 
        for j in range(2, sq + 1) : 
            if (a[i] % j == 0) : 

                # if j is a factor store  
                # it in the set 
                m.append(j) 

                # divide the number with j till it 
                # is divisible so that only prime  
                # factors are stored 
                while (a[i] % j == 0) : 
                    a[i] //= j 

        # if the number is still greater  
        # than 1 then it is a prime factor, 
        # insert in set 
        if (a[i] > 2) : 
            m.append(a[i]) 

    # the number of unique prime factors  
    # will the size of the set 
    return len(m) 

# Driver Code 
if __name__ == "__main__": 

    a = [ 1, 2, 3, 4, 5 ] 
    print (Distinct_Prime_factors(a)) 

# This code is contributed by ita_c 

```c

## C#

```cs

// C# program to count distinct 
// prime factors of a number. 
using System; 
using System.Collections.Generic; 

class GFG { 

    // Function to count the number 
    // of distinct prime factors of 
    // product of array 
    static int Distinct_Prime_factors(List<int> a) 
    { 
        // use set to store distinct factors 
        HashSet<int> m = new HashSet<int>(); 

        // iterate over every element of array 
        for (int i = 0; i < a.Count; i++) { 
            int sq = (int)Math.Sqrt(a[i]); 

            // from 2 to square root of number 
            // run a loop and check the numbers 
            // which are factors. 
            for (int j = 2; j <= sq; j++) { 
                if (a[i] % j == 0) { 

                    // if j is a factor store 
                    // it in the set 
                    m.Add(j); 

                    // divide the number with j 
                    // till it is divisible so 
                    // that only prime factors 
                    // are stored 
                    while (a[i] % j == 0) { 
                        a[i] = a[i] / j; 
                    } 
                } 
            } 

            // if the number is still greater 
            // than 1 then it is a prime factor, 
            // insert in set 
            if (a[i] > 1) { 
                m.Add(a[i]); 
            } 
        } 

        // the number of unique prime 
        // factors will the size of the set 
        return m.Count; 
    } 

    // Driver Code 
    public static void Main() 
    { 
        List<int> a = new List<int>(); 
        a.Add(1); 
        a.Add(2); 
        a.Add(3); 
        a.Add(4); 
        a.Add(5); 
        Console.WriteLine(Distinct_Prime_factors(a)); 
    } 
} 

// This code is contributed by ihritik 

```

**Output :**

```
3

```

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *



