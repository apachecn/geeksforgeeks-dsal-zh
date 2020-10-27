# 根据数字乘积进行分组时最大组的数量

给定**整数 N** ，任务是查找具有最大大小的组数。 从 1 到 N 的每个数字都根据其数字的**乘积进行分组。
**范例：****

> **输入：** N = 13
> **输出：** 3
> **说明：**
> 共有 9 个组，根据它们的分组 1 至 13 的数字
> 的乘积：[1，11] [2，12] [3，13] [4] [5] [6] [7] [8] [9]。
> 其中，有 3 个小组的人数最多，为 2 个。
> 
> **输入：** N = 2
> **输出：** 2
> **说明：**
> 共有 2 个组，它们根据对应的分组 其数字
> 从 1 到 2 的数字乘积：[1] [2]。
> 其中，有 2 个群组的最大大小为 1。

**方法：**
要解决上述问题，我们必须使用**哈希图**存储每个元素的数字从 1 到 N 的乘积，并重复它的频率。 然后，我们必须在哈希图中找到最大频率，该最大频率将是组的最大大小。 最后，计数与最大组具有相同频率计数的所有组，然后返回计数。

下面是上述方法的实现：

## C ++

```

// C++ implementation to Count the 
// groups having largest size while 
// grouping is according to 
// the product of its digits 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find out product of digit 
int digit_prod(int x) 
{ 
    int prod = 1; 

    // calculate product 
    while (x) { 
        prod *= x % 10; 
        x = x / 10; 
    } 

    // return the product of digits 
    return prod; 
} 

// Function to find the count 
int find_count(int n) 
{ 

    // hash map for 
    // counting frequency 
    map<int, int> mpp; 

    for (int i = 1; i <= n; i++) { 
        // counting freq of each element 
        mpp[digit_prod(i)] += 1; 
    } 

    int ans = 1; 
    int maxm = 0; 
    for (auto x : mpp) { 

        // find the maximum 
        if (x.second > maxm) { 
            maxm = x.second; 
            ans = 1; 
        } 

        else if (x.second == maxm) { 
            // count the number of groups having 
            // size of equal to largest group. 
            ans++; 
        } 
    } 

    return ans; 
} 

// Driver code 
int main() 
{ 

    // initialise N 
    int N = 13; 

    cout << find_count(N); 

    return 0; 
} 

```

## 爪哇

```

// Java implementation to Count the  
// groups having largest size while  
// grouping is according to  
// the product of its digits  
import java.io.*; 
import java.util.*;  

class GFG{ 

// Function to find out product of digit  
static int digit_prod(int x)  
{  
    int prod = 1;  

    // Calculate product  
    while (x != 0)  
    {  
        prod *= x % 10;  
        x = x / 10;  
    }  

    // Return the product of digits  
    return prod;  
}  

// Function to find the count  
static int find_count(int n)  
{  

    // Hash map for counting frequency  
    Map<Integer, Integer> mpp = new HashMap<>();  

    for(int i = 1; i <= n; i++) 
    {  

        // Counting freq of each element  
        int t = digit_prod(i); 
        mpp.put(t, mpp.getOrDefault(t, 0) + 1); 
    }  

    int ans = 1;  
    int maxm = 0;  

    for(Integer x : mpp.values()) 
    {  

        // Find the maximum  
        if (x > maxm)  
        {  
            maxm = x;  
            ans = 1;  
        }  

        else if (x == maxm)  
        { 

            // Count the number of groups having  
            // size of equal to largest group.  
            ans++;  
        }  
    }  
    return ans;  
}  

// Driver Code  
public static void main(String args[])  
{  

    // Initialise N  
    int N = 13;  

    System.out.print(find_count(N));  
} 
}  

// This code is contributed by offbeat

```

## Python3

```

# Python3 implementation to Count the  
# groups having largest size while  
# grouping is according to  
# the product of its digits  

# Function to find out product of digit  
def digit_prod(x) : 
    prod = 1

    # calculate product  
    while(x) :  
        prod = prod * (x % 10)  
        x = x // 10

    # return the product of digits  
    return prod  

# Function to find the count  
def find_count(n) : 

    # hash map for  
    # counting frequency  
    mpp = {}  

    for i in range(1, n + 1):  

        # counting freq of each element  
        x = digit_prod(i) 

        if x in mpp : 
            mpp[x] += 1
        else : 
            mpp[x] = 1

    ans = 1
    maxm = 0

    for value in mpp.values() :  

        # find the maximum  
        if (value > maxm) : 
            maxm = value  
            ans = 1
        elif (value == maxm) : 

            # count the number of groups having  
            # size of equal to largest group.  
            ans = ans + 1

    return ans  

# Driver code  

# initialise N  
N = 13

print(find_count(N)) 

# This code is contributed by Sanjit_Prasad 

```

## C＃

```

// C# implementation to count the  
// groups having largest size while  
// grouping is according to  
// the product of its digits  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  

class GFG{ 

// Function to find out product of digit  
static int digit_prod(int x)  
{  
    int prod = 1;  

    // Calculate product  
    while (x != 0)  
    {  
        prod *= x % 10;  
        x = x / 10;  
    }  

    // Return the product of digits  
    return prod;  
}  

// Function to find the count  
static int find_count(int n)  
{  

    // Hash map for counting frequency  
    Dictionary<int, 
               int> mpp = new Dictionary<int, 
                                         int>();  

    for(int i = 1; i <= n; i++) 
    {  

        // Counting freq of each element  
        int t = digit_prod(i); 
        if (mpp.ContainsKey(t)) 
        { 
            mpp[t]++; 
        } 
        else
        { 
            mpp[i] = 1; 
        } 
    }  

    int ans = 1;  
    int maxm = 0;  

    foreach(KeyValuePair<int, int> x in mpp) 
    {  

        // Find the maximum  
        if (x.Value > maxm)  
        {  
            maxm = x.Value;  
            ans = 1;  
        }  
        else if (x.Value == maxm)  
        { 

            // Count the number of groups having  
            // size of equal to largest group.  
            ans++;  
        }  
    }  
    return ans;  
} 

// Driver Code 
public static void Main(string[] args) 
{ 

    // Initialise N  
    int N = 13;  

    Console.Write(find_count(N)); 
} 
} 

// This code is contributed by rutvik_56 

```

**Output:** 

```
3

```

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。