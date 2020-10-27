# 质数大于或等于 k 的数字

给定一个数组，找到出现在最小 k 频率（频率> = k）中的素数次的元素。

**示例：**

```
Input : int[] arr = { 11, 11, 11, 23, 11, 37, 51, 
                      37, 37, 51, 51, 51, 51 };
        k = 2
Output : 37, 51
Explanation :
11's count is 4, 23 count 1, 37 count 3, 51 count 5\. 
37 and 51 are two number that appear prime number of
time and frequencies greater than or equal to k.

Input : int[] arr = { 11, 22, 33 } min Occurrence = 1
Output : -1
None of the count is prime number of times

```

**方法：**
1.创建一个映射，该映射将数字保存为键，并将值保存为输入数组中的值。
2.迭代映射键，并查找与它们的键相对应的值，并返回
具有最小值的键，满足条件的键的值是质数，并且提供> =最小出现次数，并提供
。

## C ++

```

// C++ code to find number  
// occurring prime number  
// of times with frequency >= k 
#include <bits/stdc++.h> 
using namespace std; 

// Check if the number of  
// occurrences are primes 
// or not 
bool isPrime(int n) 
{ 
    // Corner case 
    if (n <= 1) return false; 

    // Check from 2 to n-1 
    for (int i = 2; i < n; i++) 
        if (n % i == 0) 
            return false; 

    return true; 
} 

// Function to find number 
// with prime occurrences 
void primeOccurences(int arr[], int k) 
{ 
    unordered_map<int, int> map; 

    // Insert values and 
    // their frequencies 
    for (int i = 0; i < 12; i++)  
        map[arr[i]]++; 

    // Traverse map and find 
    // elements with prime  
    // frequencies and frequency  
    // at least k 
    for (auto x : map)  
    { 
        if (isPrime(x.second) &&  
                    x.second >= k) 
            cout << x.first << endl; 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = {11, 11, 11, 23,  
                 11, 37, 37, 51,  
                 51, 51, 51, 51}; 
    int k = 2; 

    primeOccurences(arr, k); 
    return 0; 
} 

// This code is contributed by 
// Manish Shaw(manishshaw1) 

```

## 爪哇

```

// Java code to find number occurring prime 
// number of times with frequency >= k 
import java.util.*; 

public class PrimeNumber { 

    // Function to find number with prime occurrences 
    static void primeOccurences(int[] arr, int k) 
    { 
        Map<Integer, Integer> map = new HashMap<>(); 

        // Insert values and their frequencies 
        for (int i = 0; i < arr.length; i++) { 
            int val = arr[i]; 

            int freq; 
            if (map.containsKey(val)) { 
                freq = map.get(val); 
                freq++; 
            } 
            else
                freq = 1; 
            map.put(val, freq); 
        } 

        // Traverse map and find elements with 
        // prime frequencies and frequency at 
        // least k 
        for (Map.Entry<Integer, Integer> entry :  
                               map.entrySet()) { 
            int value = entry.getValue(); 
            if (isPrime(value) && value >= k) 
                System.out.println(entry.getKey()); 
        } 
    } 

    // Check if the number of occurrences 
    // are primes or not 
    private static boolean isPrime(int n) 
    { 

        if ((n > 2 && n % 2 == 0) || n == 1)  
            return false;         

        for (int i = 3; i <= (int)Math.sqrt(n); 
             i += 2) { 
            if (n % i == 0)  
                return false;             
        } 
        return true; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int[] arr = { 11, 11, 11, 23, 11, 37, 
                      37, 51, 51, 51, 51, 51 }; 
        int k = 2; 

        primeOccurences(arr, k); 
    } 
} 

```

## Python3

```

# Python3 code to find number  
# occurring prime number of 
# times with frequency >= k 

# Function to find number  
# with prime occurrences 
def primeOccurences(arr, k): 
    map = {} 

    # Insert values and their frequencies 
    for val in arr: 
        freq = 0

        if val in map : 
            freq = map[val] 
            freq += 1

        else : 
            freq = 1
        map[val] = freq 

    # Traverse map and find elements  
    # with prime frequencies and  
    # frequency at least k 
    for entry in map : 
        value = map[entry] 

        if isPrime(value) and value >= k: 
            print(entry) 

# Check if the number of occurrences 
# are primes or not 
def isPrime(n): 

    if (n > 2 and not n % 2) or n == 1: 
        return False     

    for i in range(3, int(n**0.5 + 1), 2): 
        if not n % i: 
            return False

    return True

# Driver code 

arr = [ 11, 11, 11, 23, 11, 37, 
        37, 51, 51, 51, 51, 51 ] 
k = 2

primeOccurences(arr, k) 

# This code is contributed by Ansu Kumari. 

```

## C＃

```

// C# code to find number  
// occurring prime number 
// of times with frequency >= k 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

    // Function to find number 
    // with prime occurrences 
    static void primeOccurences(int[] arr,  
                                int k) 
    { 
        Dictionary<int, int> map =  
                   new Dictionary<int, int>(); 

        // Insert values and 
        // their frequencies 
        for (int i = 0; i < arr.Length; i++)  
        { 
            int val = arr[i]; 

            int freq; 
            if (map.ContainsKey(val))  
            { 
                freq = map[val]; 
                freq++; 
                map.Remove(val); 
            } 
            else
                freq = 1; 
            map.Add(val, freq); 
        } 

        // Traverse map and find elements 
        // with prime frequencies and  
        // frequency atleast k 
        foreach (KeyValuePair<int, int>  
                           pair in map) 
        { 
            int value = pair.Value; 
            if (isPrime(value) &&  
                        value >= k) 
                Console.WriteLine(pair.Key); 
        } 
    } 

    // Check if the number 
    // of occurrences 
    // are primes or not 
    static bool isPrime(int n) 
    { 
        if ((n > 2 &&  
             n % 2 == 0) || n == 1)  
            return false;      

        for (int i = 3;  
                 i <= (int)Math.Sqrt(n);  
                 i += 2)  
            { 
                if (n % i == 0)  
                    return false;          
            } 
        return true; 
    } 

    // Driver code 
    static void Main() 
    { 
        int[] arr = new int[]{11, 11, 11, 23, 11, 37, 
                              37, 51, 51, 51, 51, 51}; 
        int k = 2; 

        primeOccurences(arr, k); 
    } 
} 

// This code is contributed by  
// Manish Shaw(manishshaw1) 

```

**Output :**

```
37
51

```

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。