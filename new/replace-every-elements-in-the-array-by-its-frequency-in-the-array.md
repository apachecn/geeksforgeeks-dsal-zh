# 用数组

中的频率替换数组中的每个元素

给定一个整数数组，将每个元素替换为其在数组中的频率。

**示例：**

```
Input : arr[] = { 1, 2, 5, 2, 2, 5 }
Output : 1 3 2 3 3 2

Input : arr[] = { 4 5 4 5 6 6 6 }
Output : 2 2 2 2 3 3 3

```

**方法：**

1.  拿一个哈希图，它将存储数组中所有元素的频率。
2.  现在，再次遍历。
3.  现在，用频率替换所有元素。
4.  打印修改后的数组。

## C ++

```

// C++ program to replace the elements 
// by their frequency in the array. 
#include "iostream" 
#include "unordered_map" 
using namespace std; 

void ReplaceElementsByFrequency(int arr[], int n) 
{ 
    // Hash map which will store the 
    // frequency of the elements of the array. 
    unordered_map<int, int> mp; 

    for (int i = 0; i < n; ++i) { 

        // Increment the frequency 
        // of the element by 1\. 
        mp[arr[i]]++; 
    } 

    // Replace every element by its frequency 
    for (int i = 0; i < n; ++i) { 
        arr[i] = mp[arr[i]]; 
    } 
} 

int main() 
{ 
    int arr[] = { 1, 2, 5, 2, 2, 5 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    ReplaceElementsByFrequency(arr, n); 

    // Print the modified array. 
    for (int i = 0; i < n; ++i) { 
        cout << arr[i] << " "; 
    } 
    return 0; 
} 

```

## 爪哇

```

import java.util.HashMap; 

// Java program to replace the elements  
// by their frequency in the array. 
class GFG { 

    static void ReplaceElementsByFrequency(int arr[], int n) { 
        // Hash map which will store the  
        // frequency of the elements of the array.  
        HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>(); 

        for (int i = 0; i < n; ++i) { 

            // Increment the frequency  
            // of the element by 1.  
            if (mp.get(arr[i]) == null) { 
                mp.put(arr[i], 1); 
            } else { 
                mp.put(arr[i], (mp.get(arr[i]) + 1)); 
            } 
            //mp[arr[i]]++;  
        } 

        // Replace every element by its frequency  
        for (int i = 0; i < n; ++i) { 
            if (mp.get(arr[i]) != null) { 
                arr[i] = mp.get(arr[i]); 
            } 
            //arr[i] = mp[arr[i]];  
        } 
    } 

    public static void main(String[] args) { 
        int arr[] = {1, 2, 5, 2, 2, 5}; 
        int n = arr.length; 

        ReplaceElementsByFrequency(arr, n); 

        // Print the modified array.  
        for (int i = 0; i < n; ++i) { 
            System.out.print(arr[i] + " "); 
        } 
    } 
} 
// This code contributed by 29AJayKumar 

```

## Python3

```

# Python 3 program to replace the elements 
# by their frequency in the array. 

def ReplaceElementsByFrequency(arr, n): 

    # Hash map which will store the 
    # frequency of the elements of the array. 
    mp = {i:0 for i in range(len(arr))} 

    for i in range(n): 

        # Increment the frequency of the  
        # element by 1\. 
        mp[arr[i]] += 1

    # Replace every element by its frequency 
    for i in range(n): 
        arr[i] = mp[arr[i]] 

# Driver Code 
if __name__ == '__main__': 
    arr = [1, 2, 5, 2, 2, 5] 
    n = len(arr) 

    ReplaceElementsByFrequency(arr, n); 

    # Print the modified array. 
    for i in range(n): 
        print(arr[i], end = " ") 

# This code is contributed by 
# Sahil_shelangia 

```

## C＃

```

// C# program to replace the elements  
// by their frequency in the array. 
using System; 
using System.Collections.Generic;  

class GFG  
{ 

    static void ReplaceElementsByFrequency(int []arr, int n)  
    { 
        // Hash map which will store the  
        // frequency of the elements of the array.  
        Dictionary<int,int> mp = new Dictionary<int,int>(); 

        for (int i = 0; i < n; ++i) 
        { 

            // Increment the frequency  
            // of the element by 1.  
            if (!mp.ContainsKey(arr[i]))  
            { 
                mp.Add(arr[i], 1); 
            }  
            else
            { 
                var a = mp[arr[i]] + 1; 
                mp.Remove(arr[i]); 
                mp.Add(arr[i], a); 
            } 
        } 

        // Replace every element by its frequency  
        for (int i = 0; i < n; ++i)  
        { 
            if (mp[arr[i]] != 0)  
            { 
                arr[i] = mp[arr[i]]; 
            } 
            //arr[i] = mp[arr[i]];  
        } 
    } 

    // Driver code 
    public static void Main(String[] args)  
    { 
        int []arr = {1, 2, 5, 2, 2, 5}; 
        int n = arr.Length; 

        ReplaceElementsByFrequency(arr, n); 

        // Print the modified array.  
        for (int i = 0; i < n; ++i) 
        { 
            Console.Write(arr[i] + " "); 
        } 
    } 
} 

// This code contributed by Rajput-Ji 

```

**输出：**

```
1 3 2 3 3 2

```

**时间复杂度** – O（N）

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。