# 删除数组

的所有元素所需的最小操作数

给定一个整数数组 *arr* ，任务是打印删除该数组所有元素所需的最少操作数。
在操作中，可以从数组中随机选择任何元素，并且可以将其整除的每个元素从数组中删除。

**示例：**

> **输入：** arr [] = {2，4，6，3，5，10}
> **输出：** 3
> 选择 2 作为第一个元素将删除 2， 数组中的 4、6 和 10。
> 现在选择 3，这将删除 3。
> 最后，剩下唯一要选择的元素是 5。
> 
> **输入：** arr [] = {2，5，3，7，11}
> **输出：** 5

**方法：**为获得最佳结果，应从其余元素中依次选择数组中最小的元素，直到删除数组中的所有元素。

*   以升序对数组进行排序，并为出现的事件准备一个哈希。
*   对于从开始处开始的每个未标记元素，标记所有可被 select 元素整除的元素，并增加结果计数器。

下面是上述方法的实现

## C ++

```

// C++ implementation of the above approach 

#include <bits/stdc++.h> 
#define MAX 10000 

using namespace std; 

int hashTable[MAX]; 

// function to find minimum operations 
int minOperations(int arr[], int n) 
{ 
    // sort array 
    sort(arr, arr + n); 

    // prepare hash of array 
    for (int i = 0; i < n; i++) 
        hashTable[arr[i]]++; 

    int res = 0; 
    for (int i = 0; i < n; i++) { 
        if (hashTable[arr[i]]) { 
            for (int j = i; j < n; j++) 
                if (arr[j] % arr[i] == 0) 
                    hashTable[arr[j]] = 0; 
            res++; 
        } 
    } 

    return res; 
} 

// Driver program 
int main() 
{ 
    int arr[] = { 4, 6, 2, 8, 7, 21, 24, 49, 44 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    cout << minOperations(arr, n); 
    return 0; 
} 

```

## 爪哇

```

//Java implementation of the above approach  
import java.util.*; 
class Solution 
{ 
static final int MAX=10000;  

static int hashTable[]= new int[MAX];  

// function to find minimum operations  
static int minOperations(int arr[], int n)  
{  
    // sort array  
    Arrays.sort(arr);  

    // prepare hash of array  
    for (int i = 0; i < n; i++)  
        hashTable[arr[i]]++;  

    int res = 0;  
    for (int i = 0; i < n; i++) {  
        if (hashTable[arr[i]]!=0) {  
            for (int j = i; j < n; j++)  
                if (arr[j] % arr[i] == 0)  
                    hashTable[arr[j]] = 0;  
            res++;  
        }  
    }  

    return res;  
}  

// Driver program  
public static void main(String args[])  
{  
    int arr[] = { 4, 6, 2, 8, 7, 21, 24, 49, 44 };  
    int n = arr.length;  

    System.out.print( minOperations(arr, n));  

}  
} 
// This code is contributed by Arnab Kundu 

```

## Python 3

```

# Python 3 implementation of  
# the above approach 
MAX = 10000

hashTable = [0] * MAX

# function to find minimum operations 
def minOperations(arr, n): 

    # sort array 
    arr.sort() 

    # prepare hash of array 
    for i in range(n): 
        hashTable[arr[i]] += 1

    res = 0
    for i in range(n) : 
        if (hashTable[arr[i]]) : 
            for j in range(i, n): 
                if (arr[j] % arr[i] == 0): 
                    hashTable[arr[j]] = 0
            res += 1

    return res 

# Driver Code 
if __name__ == "__main__": 
    arr = [ 4, 6, 2, 8, 7, 21, 24, 49, 44 ] 
    n = len(arr) 

    print(minOperations(arr, n)) 

# This code is contributed  
# by ChitraNayal 

```

## C＃

```

using System; 

// C# implementation of the above approach   
public class Solution 
{ 
public const int MAX = 10000; 

public static int[] hashTable = new int[MAX]; 

// function to find minimum operations   
public static int minOperations(int[] arr, int n) 
{ 
    // sort array   
    Array.Sort(arr); 

    // prepare hash of array   
    for (int i = 0; i < n; i++) 
    { 
        hashTable[arr[i]]++; 
    } 

    int res = 0; 
    for (int i = 0; i < n; i++) 
    { 
        if (hashTable[arr[i]] != 0) 
        { 
            for (int j = i; j < n; j++) 
            { 
                if (arr[j] % arr[i] == 0) 
                { 
                    hashTable[arr[j]] = 0; 
                } 
            } 
            res++; 
        } 
    } 

    return res; 
} 

// Driver program   
public static void Main(string[] args) 
{ 
    int[] arr = new int[] {4, 6, 2, 8, 7, 21, 24, 49, 44}; 
    int n = arr.Length; 

    Console.Write(minOperations(arr, n)); 

} 
} 

// This code is contributed by Shrikant13 

```

## 的 PHP

```

<?php 
// PHP implementation of the  
// above approach 

// function to find minimum operations 
function minOperations(&$arr, $n) 
{ 
    $hashTable = array(); 

    // sort array 
    sort($arr); 

    // prepare hash of array 
    for ($i = 0; $i < $n; $i++) 
        $hashTable[$arr[$i]]++; 

    $res = 0; 
    for ($i = 0; $i < $n; $i++)  
    { 
        if ($hashTable[$arr[$i]]) 
        { 
            for ($j = $i; $j < $n; $j++) 
                if ($arr[$j] % $arr[$i] == 0) 
                    $hashTable[$arr[$j]] = 0; 
            $res++; 
        } 
    } 

    return $res; 
} 

// Driver Code 
$arr = array(4, 6, 2, 8, 7, 21,  
                    24, 49, 44); 
$n = sizeof($arr); 

echo minOperations($arr, $n); 

// This code is contributed  
// by Shivi_Aggarwal  
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