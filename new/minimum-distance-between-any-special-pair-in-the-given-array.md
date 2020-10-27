# 给定数组

中任何特殊对之间的最小距离

给定 **N** 个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，任务是找到特殊对的索引之间的最小可能绝对差。

> **特殊对**被定义为一对索引**（i，j）**，使得如果 **arr [i]≤arr [j]** ，则不存在 在索引 i 和 j 之间存在元素 **X** （其中 arr [i] < X < arr [j]）。
> **例如：**，
> arr [] = {1，-5，5}
> 在这里，{1，5}形成一个特殊的对，因为范围内没有元素（ 1 至 5）在 arr [0]和 arr [2]之间。

打印最小绝对差 **abs（j – i）**，以便**（i，j）对**形成特殊的对。

**示例：**

> **输入：** arr [] = {0，-10，5，-5，1}
> **输出：** 2
> **说明： ]元素 1 和 5 形成一个特殊的对，因为它们之间没有元素 X 在 1 < X < 5 范围内，并且它们彼此相距 2 个索引。**
> 
> **输入：** arr [] = {3，3}
> **输出：** 1

**天真的方法：**最简单的方法是考虑[数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的每对元素，并检查它们是否形成特殊的对。 如果发现是正确的，则在所有形成的线对之间打印最小距离。

***时间复杂度：** O（N <sup>3</sup> ）*
***辅助空间：** O（1）*

**高效方法：**为了优化上述方法，我们的想法是观察到我们仅需考虑排序数组中相邻元素的位置之间的距离，因为那对元素将没有任何值 **X** 之间。 步骤如下：

1.  将数组元素的初始索引存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
2.  [对给定数组 arr []](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) 进行排序。
3.  现在，使用 **Map** 找到排序数组的相邻元素的索引之间的距离。
4.  在上述步骤中，为每对相邻元素保持最小距离。
5.  完成上述步骤后，打印形成的最小距离。

下面是上述方法的实现：

## C ++

```

// C++ program for the above approach  
#include <bits/stdc++.h>  
using namespace std;  

// Function that finds the minimum  
// difference between two vectors  
int mindist(vector<int>& left,  
            vector<int>& right)  
{  
    int res = INT_MAX;  
    for (int i = 0; i < left.size(); ++i) {  

        int num = left[i];  

        // Find lower bound of the index  
        int index  
            = lower_bound(right.begin(),  
                        right.end(), num)  
            - right.begin();  

        // Find two adjacent indices  
        // to take difference  
        if (index == 0)  
            res = min(res,  
                    abs(num  
                        - right[index]));  

        else if (index == right.size())  
            res = min(res,  
                    abs(num  
                        - right[index - 1]));  
        else
            res = min(res,  
                    min(abs(num  
                            - right[index - 1]),  
                        abs(num  
                            - right[index])));  
    }  

    // Return the result  
    return res;  
}  

// Function to find the minimum distance  
// between index of special pairs  
int specialPairs(vector<int>& nums)  
{  
    // Stores the index of each element  
    // in the array arr[]  
    map<int, set<int> > m;  
    vector<int> vals;  

    // Store the indexes  
    for (int i = 0;  
        i < nums.size(); ++i) {  
        m[nums[i]].insert(i);  
    }  

    // Get the unique values in list  
    for (auto p : m) {  
        vals.push_back(p.first);  
    }  

    int res = INT_MAX;  

    for (int i = 0;  
        i < vals.size(); ++i) {  

        vector<int> vec(m[vals[i]].begin(),  
                        m[vals[i]].end());  

        // Take adjacent difference  
        // of same values  
        for (int i = 1;  
            i < vec.size(); ++i)  
            res = min(res,  
                    abs(vec[i]  
                        - vec[i - 1]));  

        if (i) {  
            int a = vals[i];  

            // Left index array  
            vector<int> left(m[a].begin(),  
                            m[a].end());  

            int b = vals[i - 1];  

            // Right index array  
            vector<int> right(m[b].begin(),  
                            m[b].end());  

            // Find the minimum gap between  
            // the two adjacent different  
            // values  
            res = min(res,  
                    mindist(left, right));  
        }  
    }  
    return res;  
}  

// Driver Code  
int main()  
{  
    // Given array  
    vector<int> arr{ 0, -10, 5, -5, 1 };  

    // Function Call  
    cout << specialPairs(arr);  

    return 0;  
}  

```

## Python3

```

# Python3 program for the above approach 
import sys 

# Function that finds the minimum 
# difference between two vectors 
def mindist(left, right): 

    res = sys.maxsize 

    for i in range(len(left)): 
        num = left[i] 

        # Find lower bound of the index 
        index = right.index(min( 
                [i for i in right if num >= i])) 

        # Find two adjacent indices 
        # to take difference 
        if (index == 0): 
            res = min(res, 
                  abs(num - right[index])) 
        elif (index == len(right)): 
            res = min(res,  
                  min(abs(num - right[index -1]), 
                      abs(num - right[index]))) 

    # Return the result 
    return res 

# Function to find the minimum distance 
# between index of special pairs 
def specialPairs(nums): 

    # Stores the index of each element 
    # in the array arr[] 
    m = {} 
    vals = [] 

    for i in range(len(nums)): 
        m[nums[i]] = i 

    for p in m: 
        vals.append(p) 

    res = sys.maxsize 

    for i in range(1, len(vals)): 
        vec = [m[vals[i]]] 

        # Take adjacent difference 
        # of same values 
        for i in range(1, len(vec)): 
            res = min(res, 
                      abs(vec[i] - vec[i - 1])) 

        if (i): 
            a = vals[i] 

            # Left index array 
            left = [m[a]] 

            b = vals[i - 1] 

            # Right index array 
            right = [m[b]] 

            # Find the minimum gap between 
            # the two adjacent different 
            # values 
            res = min(res, 
                      mindist(left, right)) + 1

    return res 

# Driver Code 
if __name__ == "__main__": 

    # Given array  
    arr = [ 0, -10, 5, -5, 1 ] 

    # Function call 
    print(specialPairs(arr)) 

# This code is contributed by dadi madhav

```

**Output:** 

```
2

```

***时间复杂度：** O（N * log N）*
***辅助空间：** O（N）*

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。