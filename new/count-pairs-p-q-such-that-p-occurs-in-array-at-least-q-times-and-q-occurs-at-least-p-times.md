# 对（p，q）进行计数，以使 p 在数组中至少出现 q 次，并且 q 出现至少 p 次

给定数组 **arr []** ，任务是对无序对正整数**（p，q）**进行计数，以使 **p 出现在数组**中。 至少 q 次**和 **q 发生至少 p 次**。**

**示例：**

> **输入：** arr [] = {1、2、3、4、5}
> **输出：** 1
> （1、1）是唯一有效的对
> 
> **输入：** arr [] = {3，3，2，2，2}
> **输出：** 2
> （2，3）和（2，2）是 唯一可能的对。

**方法：**

1.  这个想法是用数组的数量来哈希数组的每个元素，并从数组元素中创建一个唯一元素的向量。 将对数初始化为 0。
2.  遍历唯一元素的向量以计算对数。
3.  如果元素数小于元素本身，则在循环内继续执行；否则，如果元素数等于元素，则将对数增加 1（对形式为（x，x）），否则转到步骤 4。
4.  如果 j 的计数大于或等于 element，则将对的数量增加 1，并从 j =（element + 1）循环到更新 j 的元素的数量，如果 j 的计数大于或等于 element，则将对的数量增加 1，因为对是无序的。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the count of required pairs 
int get_unordered_pairs(int a[], int n) 
{ 
    // To store unique elements 
    vector<int> vs; 

    // To hash elements with their frequency 
    unordered_map<int, int> m; 

    // Store frequencies in m and all distinct 
    // items in vs 
    for (int i = 0; i < n; i++) { 
        m[a[i]]++; 
        if (m[a[i]] == 1) 
            vs.push_back(a[i]); 
    } 

    // Traverse through distinct elements 
    int number_of_pairs = 0; 
    for (int i = 0; i < vs.size(); i++) { 

        // If current element is greater than 
        // its frequency in the array 
        if (m[vs[i]] < vs[i]) 
            continue; 

        // If element is equal to its frequency, 
        // a pair of the form (x, x) is formed. 
        else if (m[vs[i]] == vs[i]) 
            number_of_pairs += 1; 

        // If element is less than its frequency 
        else { 
            number_of_pairs += 1; 
            for (int j = vs[i] + 1; j <= m[vs[i]]; j++) { 
                if (m[j] >= vs[i]) 
                    number_of_pairs += 1; 
            } 
        } 
    } 
    return number_of_pairs; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 3, 3, 2, 2, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << get_unordered_pairs(arr, n); 
    return 0; 
} 

```

## 爪哇

```

// Java implementation of the approach 
import java.util.*; 

class GFG 
{ 

// Function to return the count of required pairs 
static int get_unordered_pairs(int []a, int n) 
{ 
    // To store unique elements 
    ArrayList<Integer> vs = new ArrayList<Integer>(); 

    // To hash elements with their frequency 
    int[] m = new int[maximum(a)+1]; 

    // Store frequencies in m and all distinct 
    // items in vs 
    for (int i = 0; i < n; i++)  
    { 
        m[(int)a[i]]++; 
        if (m[a[i]] == 1) 
            vs.add(a[i]); 
    } 

    // Traverse through distinct elements 
    int number_of_pairs = 0; 
    for (int i = 0; i < vs.size(); i++)  
    { 

        // If current element is greater than 
        // its frequency in the array 
        if (m[(int)vs.get(i)] < (int)vs.get(i)) 
            continue; 

        // If element is equal to its frequency, 
        // a pair of the form (x, x) is formed. 
        else if (m[(int)vs.get(i)] == (int)vs.get(i)) 
            number_of_pairs += 1; 

        // If element is less than its frequency 
        else
        { 
            number_of_pairs += 1; 
            for (int j = (int)vs.get(i) + 1; j <= m[(int)vs.get(i)]; j++) 
            { 
                if (m[j] >= (int)vs.get(i)) 
                    number_of_pairs += 1; 
            } 
        } 
    } 
    return number_of_pairs; 
} 
static int maximum(int []arr) 
{ 
    int max = Integer.MIN_VALUE; 
    for(int i = 0; i < arr.length; i++) 
    { 
        if(arr[i] > max) 
        { 
            max = arr[i]; 
        } 
    } 
    return max; 
} 

// Driver code 
public static void main (String[] args)  
{ 

    int []arr = { 3, 3, 2, 2, 2 }; 
    int n = arr.length; 
    System.out.println(get_unordered_pairs(arr, n)); 
} 
} 

// This code is contributed by mits 

```

## Python3

```

# Python3 implementation of the approach  
from collections import defaultdict 

# Function to return the count of  
# required pairs  
def get_unordered_pairs(a, n):  

    # To store unique elements  
    vs = []  

    # To hash elements with their frequency  
    m = defaultdict(lambda:0)  

    # Store frequencies in m and  
    # all distinct items in vs  
    for i in range(0, n):  
        m[a[i]] += 1
        if m[a[i]] == 1:  
            vs.append(a[i])  

    # Traverse through distinct elements  
    number_of_pairs = 0
    for i in range(0, len(vs)):  

        # If current element is greater  
        # than its frequency in the array  
        if m[vs[i]] < vs[i]: 
            continue

        # If element is equal to its frequency,  
        # a pair of the form (x, x) is formed.  
        elif m[vs[i]] == vs[i]:  
            number_of_pairs += 1

        # If element is less than its 
        # frequency  
        else: 
            number_of_pairs += 1
            for j in range(vs[i] + 1, m[vs[i]] + 1):  
                if m[j] >= vs[i]:  
                    number_of_pairs += 1

    return number_of_pairs  

# Driver code  
if __name__ == "__main__":  

    arr = [3, 3, 2, 2, 2]  
    n = len(arr)  
    print(get_unordered_pairs(arr, n)) 

# This code is contributed 
# by Rituraj Jain 

```

## C＃

```

// C# implementation of the approach 
using System; 
using System.Collections; 
using System.Linq; 

class GFG 
{ 
// Function to return the count of required pairs 
static int get_unordered_pairs(int []a, int n) 
{ 
    // To store unique elements 
    ArrayList vs = new ArrayList(); 

    // To hash elements with their frequency 
    int[] m = new int[a.Max()+1]; 

    // Store frequencies in m and all distinct 
    // items in vs 
    for (int i = 0; i < n; i++)  
    { 
        m[(int)a[i]]++; 
        if (m[a[i]] == 1) 
            vs.Add(a[i]); 
    } 

    // Traverse through distinct elements 
    int number_of_pairs = 0; 
    for (int i = 0; i < vs.Count; i++)  
    { 

        // If current element is greater than 
        // its frequency in the array 
        if (m[(int)vs[i]] < (int)vs[i]) 
            continue; 

        // If element is equal to its frequency, 
        // a pair of the form (x, x) is formed. 
        else if (m[(int)vs[i]] == (int)vs[i]) 
            number_of_pairs += 1; 

        // If element is less than its frequency 
        else 
        { 
            number_of_pairs += 1; 
            for (int j = (int)vs[i] + 1; j <= m[(int)vs[i]]; j++) 
            { 
                if (m[j] >= (int)vs[i]) 
                    number_of_pairs += 1; 
            } 
        } 
    } 
    return number_of_pairs; 
} 

// Driver code 
static void Main() 
{ 
    int []arr = { 3, 3, 2, 2, 2 }; 
    int n = arr.Length; 
    Console.WriteLine(get_unordered_pairs(arr, n)); 
} 
} 

// This code is contributed by mits 

```

## 的 PHP

```

<?php 
// PHP implementation of the approach  

// Function to return the count of  
// required pairs  
function get_unordered_pairs($a, $n)  
{  
    // To store unique elements  
    $vs = array();  

    // To hash elements with  
    // their frequency  
    $m = array(); 

    for($i = 0; $i < $n; $i++) 
        $m[$a[$i]] = 0 ; 

    // Store frequencies in m and  
    // all distinct items in vs  
    for ($i = 0; $i < $n; $i++) 
    {  
        $m[$a[$i]]++;  
        if ($m[$a[$i]] == 1)  
            array_push($vs, $a[$i]);  
    }  

    // Traverse through distinct elements  
    $number_of_pairs = 0;  
    for ($i = 0; $i < sizeof($vs); $i++)  
    {  

        // If current element is greater  
        // than its frequency in the array  
        if ($m[$vs[$i]] < $vs[$i])  
            continue;  

        // If element is equal to its frequency,  
        // a pair of the form (x, x) is formed.  
        else if ($m[$vs[$i]] == $vs[$i])  
            $number_of_pairs += 1;  

        // If element is less than its  
        // frequency  
        else
        {  
            $number_of_pairs += 1;  
            for ($j = $vs[$i] + 1;  
                 $j <= $m[$vs[$i]]; $j++)  
            { 
                if ($m[$j] >= $vs[$i])  
                    $number_of_pairs += 1;  
            }  
        }  
    }  
    return $number_of_pairs;  
}  

// Driver code  
$arr = array(3, 3, 2, 2, 2);  
$n = sizeof($arr); 
echo get_unordered_pairs($arr, $n);  

// This code is contributed by Ryuga 
?> 

```

**Output:**

```
2

```

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。