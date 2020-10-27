# 在数组中找到四个元素 a，b，c 和 d，使得 a + b = c + d

给定一个由不同整数组成的数组，请查找是否有两对（a，b）和（c，d），使得 a + b = c + d，而 a，b，c 和 d 是不同的元素。 如果有多个答案，请打印其中的任何一个。

例：

```
Input:   {3, 4, 7, 1, 2, 9, 8}
Output:  (3, 8) and (4, 7)
Explanation: 3+8 = 4+7

Input:   {3, 4, 7, 1, 12, 9};
Output:  (4, 12) and (7, 9)
Explanation: 4+12 = 7+9

Input:  {65, 30, 7, 90, 1, 9, 8};
Output:  No pairs found

```

预期时间复杂度：O（n <sup>2</sup> ）

**简单解决方案**是运行四个循环以生成所有可能的四倍数组元素。 对于每四个（a，b，c，d），检查（a + b）=（c + d）。 该解决方案的时间复杂度为 O（n <sup>4</sup> ）。

有效的**解决方案**可以在 O（n <sup>2</sup> ）时间内解决此问题。 这个想法是使用[哈希](http://geeksquiz.com/hashing-set-1-introduction/)。 在哈希表中，我们将 sum 作为键，将 pair 作为值。

```
Loop i = 0 to n-1 :
    Loop j = i + 1 to n-1 :
        calculate sum
        If in hash table any index already exist
            Then print (i, j) and previous pair 
            from hash table  
        Else update hash table
    EndLoop;
EndLoop;

```

以下是上述想法的实现。 在下面的实现中，使用 map 代替哈希。 映射插入和搜索的时间复杂度实际上是 O（Log n）而不是 O（1）。 因此，下面的实现是 O（n <sup>2</sup> Log n）。

## C / C ++

```

// Find four different elements a,b,c and d of array such that 
// a+b = c+d 
#include<bits/stdc++.h> 
using namespace std; 

bool findPairs(int arr[], int n) 
{ 
    // Create an empty Hash to store mapping from sum to 
    // pair indexes 
    map<int, pair<int, int> > Hash; 

    // Traverse through all possible pairs of arr[] 
    for (int i = 0; i < n; ++i) 
    { 
        for (int j = i + 1; j < n; ++j) 
        { 
            // If sum of current pair is not in hash, 
            // then store it and continue to next pair 
            int sum = arr[i] + arr[j]; 
            if (Hash.find(sum) == Hash.end()) 
                Hash[sum] = make_pair(i, j); 

            else // Else (Sum already present in hash) 
            { 
                // Find previous pair 
                pair<int, int> pp = Hash[sum];// pp->previous pair 

                // Since array elements are distinct, we don't 
                // need to check if any element is common among pairs 
                cout << "(" << arr[pp.first] << ", " << arr[pp.second] 
                     << ") and (" << arr[i] << ", " << arr[j] << ")n"; 
                return true; 
            } 
        } 
    } 

    cout << "No pairs found"; 
    return false; 
} 

// Driver program 
int main() 
{ 
    int arr[] = {3, 4, 7, 1, 2, 9, 8}; 
    int n  =  sizeof arr / sizeof arr[0]; 
    findPairs(arr, n); 
    return 0; 
} 

```

## 爪哇

```

// Java Program to find four different elements a,b,c and d of 
// array such that a+b = c+d 
import java.io.*; 
import java.util.*; 

class ArrayElements 
{ 
    // Class to represent a pair 
    class pair 
    { 
        int first, second; 
        pair(int f,int s) 
        { 
            first = f; second = s; 
        } 
    }; 

    boolean findPairs(int arr[]) 
    { 
        // Create an empty Hash to store mapping from sum to 
        // pair indexes 
        HashMap<Integer,pair> map = new HashMap<Integer,pair>(); 
        int n=arr.length; 

        // Traverse through all possible pairs of arr[] 
        for (int i=0; i<n; ++i) 
        { 
            for (int j=i+1; j<n; ++j) 
            { 
                // If sum of current pair is not in hash, 
                // then store it and continue to next pair 
                int sum = arr[i]+arr[j]; 
                if (!map.containsKey(sum)) 
                    map.put(sum,new pair(i,j)); 

                else // Else (Sum already present in hash) 
                { 
                    // Find previous pair 
                    pair p = map.get(sum); 

                    // Since array elements are distinct, we don't 
                    // need to check if any element is common among pairs 
                    System.out.println("("+arr[p.first]+", "+arr[p.second]+ 
                                      ") and ("+arr[i]+", "+arr[j]+")"); 
                    return true; 
                } 
            } 
        } 
        return false; 
    } 

    // Testing program 
    public static void main(String args[]) 
    { 
        int arr[] = {3, 4, 7, 1, 2, 9, 8}; 
        ArrayElements a = new ArrayElements(); 
        a.findPairs(arr); 
    } 
} 
// This code is contributed by Aakash Hasija 

```

## 蟒蛇

```

# Python Program to find four different elements a,b,c and d of 
# array such that a+b = c+d 

# function to find a, b, c, d such that 
# (a + b) = (c + d) 
def findPairs(arr, n): 

# Create an empty hashmap to store mapping  
# from sum to pair indexes 
Hash = {} 

# Traverse through all possible pairs of arr[] 
for i in range(n - 1): 
    for j in range(i + 1, n): 
    sum = arr[i] + arr[j] 
    # Sum already present in hash 
    if sum in Hash.keys(): 
        # print previous pair and current 
        prev = Hash.get(sum) 
        print (str(prev) + " and (%d, %d)"
        %(arr[i], arr[j]))      
        return True
    else: 
        # sum is not in hash 
        # store it and continue to next pair 
        Hash[sum] = (arr[i], arr[j]) 
return False

# driver program 
arr = [3, 4, 7, 1, 2, 9, 8] 
n = len(arr) 
findPairs(arr, n) 

# This code is contributed by Aditi Sharma 

```

## C＃

```

using System; 
using System.Collections.Generic; 

// C# Program to find four different elements a,b,c and d of  
// array such that a+b = c+d  

public class ArrayElements 
{ 
    // Class to represent a pair  
    public class pair 
    { 
        private readonly ArrayElements outerInstance; 

        public int first, second; 
        public pair(ArrayElements outerInstance, int f, int s) 
        { 
            this.outerInstance = outerInstance; 
            first = f; 
            second = s; 
        } 
    } 

    public virtual bool findPairs(int[] arr) 
    { 
        // Create an empty Hash to store mapping from sum to  
        // pair indexes  
        Dictionary<int, pair> map = new Dictionary<int, pair>(); 
        int n = arr.Length; 

        // Traverse through all possible pairs of arr[]  
        for (int i = 0; i < n; ++i) 
        { 
            for (int j = i + 1; j < n; ++j) 
            { 
                // If sum of current pair is not in hash,  
                // then store it and continue to next pair  
                int sum = arr[i] + arr[j]; 
                if (!map.ContainsKey(sum)) 
                { 
                    map[sum] = new pair(this, i,j); 
                } 

                else // Else (Sum already present in hash) 
                { 
                    // Find previous pair  
                    pair p = map[sum]; 

                    // Since array elements are distinct, we don't  
                    // need to check if any element is common among pairs  
                    Console.WriteLine("(" + arr[p.first] + ", " + arr[p.second] + ") and (" + arr[i] + ", " + arr[j] + ")"); 
                    return true; 
                } 
            } 
        } 
        return false; 
    } 

    // Testing program  
    public static void Main(string[] args) 
    { 
        int[] arr = new int[] {3, 4, 7, 1, 2, 9, 8}; 
        ArrayElements a = new ArrayElements(); 
        a.findPairs(arr); 
    } 
} 

// This code is contributed by Shrikant13 

```

**Output:**

```
(3, 8) and (4, 7)
```

感谢 [Gaurav Ahirwar](http://qa.geeksforgeeks.org/user/Mr.Lazy) 提出了上述解决方案。

**练习：**
1）扩展上述解决方案，并在数组中允许重复项。
2）进一步扩展解决方案，以在输出中打印所有四联而不是一个。 并且所有四联体应按字典顺序印刷（较小的值排在较大的值之前）。 假设我们有两个解决方案 S1 和 S2。

```
S1 : a1 b1 c1 d1 ( these are values of indices int the array )  
S2 : a2 b2 c2 d2

S1 is lexicographically smaller than S2 iff
  a1 < a2 OR
  a1 = a2 AND b1 < b2 OR
  a1 = a2 AND b1 = b2 AND c1 < c2 OR 
  a1 = a2 AND b1 = b2 AND c1 = c2 AND d1 < d2 
```

锻炼方法请参见[和](http://qa.geeksforgeeks.org/3921/find-index-values-that-satisfy-where-integers-values-array)。

**相关文章：**
[查找满足 ab = cd 的所有对（a，b）和（c，d）对](https://www.geeksforgeeks.org/find-pairs-ab-cd-array-satisfy-ab-cd/)

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。