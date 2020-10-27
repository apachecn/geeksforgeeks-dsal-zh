# 最大化给定数组

的任意排列所引起的重复之间的最小距离

给定一个数组 **arr []** ，该数组由 **[1，N]** 范围内的 **N** 个正整数组成，任务是找到任意一个之间的最大最小距离 从给定数组的任何排列中元素的连续重复。

**示例：**

> **输入：** arr [] = {1、2、1、3}
> **输出：** 3
> **说明：**之间的最大可能距离 重复是从排列{ **1** ，2、3， **1** }或{ **1** ，3、2， **1** } 。
> **输入：** arr [] = {1、2、3、4}
> **输出：** 0

**方法：**请按照以下步骤解决问题：

1.  存储每个数组元素的频率。
2.  找到包含最大频率的元素，例如 **maxFreqElement** 。
3.  计算具有最大频率的元素的出现次数，例如 **maxFreqCount** 。
4.  通过公式**（N- maxFreqCount）/（maxFreqElement-1））计算所需距离**

下面是上述方法的实现。

## C ++

```

// C++ Program to implement  
// the above approach  
#include <bits/stdc++.h>  
using namespace std;  
int findMaxLen(vector<int>& a)  
{  

    // Size of the array  
    int n = a.size();  

    // Stores the frequency of  
    // array elements  
    int freq[n + 1];  
    memset(freq, 0, sizeof freq);  

    for (int i = 0; i < n; ++i) {  
        freq[a[i]]++;  
    }  

    int maxFreqElement = INT_MIN;  
    int maxFreqCount = 1;  

    for (int i = 1; i <= n; ++i) {  

        // Find the highest frequency  
        // in the array  
        if (freq[i] > maxFreqElement) {  
            maxFreqElement = freq[i];  
            maxFreqCount = 1;  
        }  

        // Increase count of max frequent element  
        else if (freq[i] == maxFreqElement)  
            maxFreqCount++;  
    }  

    int ans;  

    // If no repetition is present  
    if (maxFreqElement == 1)  
        ans = 0;  
    else {  
        // Find the maximum distance  
        ans = ((n - maxFreqCount)  
            / (maxFreqElement - 1));  
    }  

    // Return the max distance  
    return ans;  
}  

// Driver Code  
int main()  
{  

    vector<int> a = { 1, 2, 1, 2 };  
    cout << findMaxLen(a) << endl;  

}  

```

## 爪哇

```

// Java program to implement  
// the above approach  
class GFG{ 

static int findMaxLen(int a[], int n)  
{  

    // Stores the frequency of  
    // array elements  
    int freq[] = new int[n + 1];  

    for(int i = 0; i < n; ++i) 
    {  
        freq[a[i]]++;  
    }  

    int maxFreqElement = Integer.MIN_VALUE;  
    int maxFreqCount = 1;  

    for(int i = 1; i <= n; ++i) 
    {  

        // Find the highest frequency  
        // in the array  
        if (freq[i] > maxFreqElement) 
        {  
            maxFreqElement = freq[i];  
            maxFreqCount = 1;  
        }  

        // Increase count of max frequent element  
        else if (freq[i] == maxFreqElement)  
            maxFreqCount++;  
    }  

    int ans;  

    // If no repetition is present  
    if (maxFreqElement == 1)  
        ans = 0;  
    else 
    { 

        // Find the maximum distance  
        ans = ((n - maxFreqCount) /  
               (maxFreqElement - 1));  
    }  

    // Return the max distance  
    return ans;  
}  

// Driver Code  
public static void main(String [] args)  
{  
    int a[] = { 1, 2, 1, 2 };  
    int n = a.length; 

    System.out.print(findMaxLen(a, n)); 
} 
} 

// This code is contributed by chitranayal 

```

## Python3

```

# Python3 program to implement 
# the above approach 
import sys 

def findMaxLen(a): 

    # Size of the array 
    n = len(a) 

    # Stores the frequency of 
    # array elements 
    freq = [0] * (n + 1) 

    for i in range(n): 
        freq[a[i]] += 1

    maxFreqElement = -sys.maxsize - 1
    maxFreqCount = 1

    for i in range(1, n + 1): 

        # Find the highest frequency 
        # in the array 
        if(freq[i] > maxFreqElement): 
            maxFreqElement = freq[i] 
            maxFreqCount = 1

        # Increase count of max frequent element 
        elif(freq[i] == maxFreqElement): 
            maxFreqCount += 1

    # If no repetition is present 
    if(maxFreqElement == 1): 
        ans = 0
    else: 

        # Find the maximum distance 
        ans = ((n - maxFreqCount) // 
               (maxFreqElement - 1)) 

    # Return the max distance 
    return ans 

# Driver Code 
a = [ 1, 2, 1, 2 ] 

# Function call 
print(findMaxLen(a)) 

# This code is contributed by Shivam Singh 

```

## C＃

```

// C# program to implement 
// the above approach 
using System; 
class GFG{ 

    static int findMaxLen(int[] a, int n) 
    { 

        // Stores the frequency of 
        // array elements 
        int[] freq = new int[n + 1]; 

        for (int i = 0; i < n; ++i)  
        { 
            freq[a[i]]++; 
        } 

        int maxFreqElement = int.MinValue; 
        int maxFreqCount = 1; 

        for (int i = 1; i <= n; ++i)  
        { 

            // Find the highest frequency 
            // in the array 
            if (freq[i] > maxFreqElement)  
            { 
                maxFreqElement = freq[i]; 
                maxFreqCount = 1; 
            } 

            // Increase count of max  
            // frequent element 
            else if (freq[i] == maxFreqElement) 
                maxFreqCount++; 
        } 

        int ans; 

        // If no repetition is present 
        if (maxFreqElement == 1) 
            ans = 0; 
        else
        { 

            // Find the maximum distance 
            ans = ((n - maxFreqCount) /  
                   (maxFreqElement - 1)); 
        } 

        // Return the max distance 
        return ans; 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        int[] a = {1, 2, 1, 2}; 
        int n = a.Length; 
        Console.Write(findMaxLen(a, n)); 
    } 
} 

// This code is contributed by Amit Katiyar

```

**Output:** 

```
2

```

***时间复杂度：** O（N）*
***辅助空间：** O（N）*

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。