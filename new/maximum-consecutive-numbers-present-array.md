# 数组

中存在的最大连续数

查找在数组中混杂的最大连续数的长度。

例子：

```
Input : arr[] = {1, 94, 93, 1000, 5, 92, 78};
Output : 3 
The largest set of consecutive elements is
92, 93, 94 

Input  : arr[] = {1, 5, 92, 4, 78, 6, 7};
Output : 4 
The largest set of consecutive elements is
4, 5, 6, 7

```

这个想法是使用哈希。 我们遍历数组，对于每个元素，我们检查它是否是其序列的起始元素。 如果是，则通过增加其值来搜索集合并增加长度。 通过对所有元素重复此操作，我们可以找到数组中所有连续集的长度。 最后，我们返回最大集合的长度。

## C ++

```

// CPP program to find largest consecutive numbers 
// present in arr[]. 
#include <bits/stdc++.h> 
using namespace std; 

int findLongestConseqSubseq(int arr[], int n) 
{ 
    /* We insert all the array elements into 
       unordered set. */
    unordered_set<int> S; 
    for (int i = 0; i < n; i++) 
        S.insert(arr[i]); 

    // check each possible sequence from the start 
    // then update optimal length 
    int ans = 0; 
    for (int i = 0; i < n; i++) { 

        // if current element is the starting 
        // element of a sequence 
        if (S.find(arr[i] - 1) == S.end()) { 

            // Then check for next elements in the 
            // sequence 
            int j = arr[i]; 

            // increment the value of array element 
            // and repeat search in the set 
            while (S.find(j) != S.end()) 
                j++;  

            // Update  optimal length if this length 
            // is more. To get the length as it is  
            // incremented one by one 
            ans = max(ans, j - arr[i]);  
        } 
    } 
    return ans; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, 94, 93, 1000, 5, 92, 78 }; 
    int n = sizeof(arr) / sizeof(int); 
    cout << findLongestConseqSubseq(arr, n) << endl; 
    return 0; 
} 

```

## 爪哇

```

// Java program to find largest consecutive  
// numbers present in arr[]. 
import java.util.*; 

class GFG 
{ 

static int findLongestConseqSubseq(int arr[], int n) 
{ 
    /* We insert all the array elements into 
    unordered set. */
    HashSet<Integer> S = new HashSet<Integer>(); 
    for (int i = 0; i < n; i++) 
        S.add(arr[i]); 

    // check each possible sequence from the start 
    // then update optimal length 
    int ans = 0; 
    for (int i = 0; i < n; i++)  
    { 

        // if current element is the starting 
        // element of a sequence 
        if(S.contains(arr[i]))  
        { 

            // Then check for next elements in the 
            // sequence 
            int j = arr[i]; 

            // increment the value of array element 
            // and repeat search in the set 
            while (S.contains(j)) 
                j++;  

            // Update optimal length if this length 
            // is more. To get the length as it is  
            // incremented one by one 
            ans = Math.max(ans, j - arr[i]);  
        } 
    } 
    return ans; 
} 

// Driver code 
public static void main(String[] args)  
{ 
    int arr[] = {1, 94, 93, 1000, 5, 92, 78}; 
    int n = arr.length; 
        System.out.println(findLongestConseqSubseq(arr, n)); 
} 
} 

// This code contributed by Rajput-Ji 

```

## Python3

```

# Python3 program to find largest consecutive 
# numbers present in arr. 

def findLongestConseqSubseq(arr, n): 
    '''We insert all the array elements into unordered set.'''

    S = set(); 
    for i in range(n): 
        S.add(arr[i]); 

    # check each possible sequence from the start 
    # then update optimal length 
    ans = 0; 
    for i in range(n): 

        # if current element is the starting 
        # element of a sequence 
        if S.__contains__(arr[i]): 

            # Then check for next elements in the 
            # sequence 
            j = arr[i]; 

            # increment the value of array element 
            # and repeat search in the set 
            while(S.__contains__(j)): 
                j += 1; 

            # Update optimal length if this length 
            # is more. To get the length as it is 
            # incremented one by one 
            ans = max(ans, j - arr[i]); 
    return ans; 

# Driver code 
if __name__ == '__main__': 
    arr = [ 1, 94, 93, 1000, 5, 92, 78 ]; 
    n = len(arr); 
    print(findLongestConseqSubseq(arr, n)); 

# This code is contributed by 29AjayKumar 

```

## C＃

```

// C# program to find largest consecutive  
// numbers present in arr[]. 
using System; 
using System.Collections.Generic; public

class GFG 
{ 

static int findLongestConseqSubseq(int []arr, int n) 
{ 
    /* We insert all the array elements into 
    unordered set. */
    HashSet<int> S = new HashSet<int>(); 
    for (int i = 0; i < n; i++) 
        S.Add(arr[i]); 

    // check each possible sequence from the start 
    // then update optimal length 
    int ans = 0; 
    for (int i = 0; i < n; i++)  
    { 

        // if current element is the starting 
        // element of a sequence 
        if(S.Contains(arr[i]))  
        { 

            // Then check for next elements in the 
            // sequence 
            int j = arr[i]; 

            // increment the value of array element 
            // and repeat search in the set 
            while (S.Contains(j)) 
                j++;  

            // Update optimal length if this length 
            // is more. To get the length as it is  
            // incremented one by one 
            ans = Math.Max(ans, j - arr[i]);  
        } 
    } 
    return ans; 
} 

// Driver code 
public static void Main(String[] args)  
{ 
    int []arr = {1, 94, 93, 1000, 5, 92, 78}; 
    int n = arr.Length; 
    Console.WriteLine(findLongestConseqSubseq(arr, n)); 
} 
} 

// This code has been contributed by 29AjayKumar 

```

**输出：**

```
3

```

**时间复杂度：** O（n）

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。