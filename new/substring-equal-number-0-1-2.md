# 计数具有相等数量的 0s，1s 和 2s 的子字符串

给定一个仅包含 0、1s 或 2s 的字符串，请计算具有相等数目的 0s，1s 和 2s 的子字符串的数量。

**示例：**

```
Input  :  str = “0102010”
Output :  2
Explanation : Substring str[2, 4] = “102” and 
              substring str[4, 6] = “201” has 
              equal number of 0, 1 and 2

Input : str = "102100211"
Output : 5

```

**简单解决方案**遍历 str 的所有子串，并检查它们是否包含等于 0、1、2 的值。 str 的子字符串总数为 O（n <sup>2</sup> ），检查每个子字符串的计数需要 O（n）次，因此解决此问题所需的总时间为 O（n <sup>3</sup> ） 时间用蛮力方法。

一种有效的**解决方案**是跟踪计数 0、1 和 2。

```
Let zc[i] denotes number of zeros between index 1 and i
    oc[i] denotes number of ones between index 1 and i
    tc[i] denotes number of twos between index 1 and i
for substring str[i, j] to be counted in result we should have :
    zc[i] – zc[j-1] = oc[i] – oc[j-1] = tc[i] - tc[j-1]
we can write above relation as follows :
z[i] – o[i] = z[j-1] – o[j-1]    and
z[i] – t[i] = z[j-1] – t[j-1]

```

可以在循环执行字符串时跟踪上述关系，在每个索引处，我们将计算该差异对，并检查该差异对之前发生了多少次，并将该计数添加到结果中以保持跟踪 在下面的代码中，我们使用了[映射](http://quiz.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。 考虑到[映射操作](http://quiz.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)（例如搜索和插入）花费 O（Log n）时间这一事实，该解决方案的总时间复杂度为 O（n log n）。

## C ++

```

// C++ program to find substring with equal 
// number of 0's, 1's and 2's 
#include <bits/stdc++.h> 
using namespace std; 

// Method to count number of substring which 
// has equal 0, 1 and 2 
int getSubstringWithEqual012(string str) 
{ 
    int n = str.length(); 

    // map to store, how many times a difference 
    // pair has occurred previously 
    map< pair<int, int>, int > mp; 
    mp[make_pair(0, 0)] = 1; 

    //  zc (Count of zeroes), oc(Count of 1s) 
    //  and tc(count of twos) 
    //  In starting all counts are zero 
    int zc = 0, oc = 0, tc = 0; 

    //  looping into string 
    int res = 0;  // Initialize result 
    for (int i = 0; i < n; ++i) 
    { 
        // increasing the count of current character 
        if (str[i] == '0') zc++; 
        else if (str[i] == '1') oc++; 
        else tc++;  // Assuming that string doesn't contain 
                    // other characters 

        // making pair of differences (z[i] - o[i], 
        // z[i] - t[i]) 
        pair<int, int> tmp = make_pair(zc - oc, 
                                       zc - tc); 

        // Count of previous occurrences of above pair 
        // indicates that the subarrays forming from 
        // every previous occurrence to this occurrence 
        // is a subarray with equal number of 0's, 1's 
        // and 2's 
        res = res + mp[tmp]; 

        // increasing the count of current difference 
        // pair by 1 
        mp[tmp]++; 
    } 

    return res; 
} 

//  driver code to test above method 
int main() 
{ 
    string str = "0102010"; 
    cout << getSubstringWithEqual012(str) << endl; 
    return 0; 
} 

```

## Python3

```

# Python3 program to find substring with equal 
# number of 0's, 1's and 2's 

# Method to count number of substring which 
# has equal 0, 1 and 2 
def getSubstringWithEqual012(string): 
    n = len(string) 

    # map to store, how many times a difference 
    # pair has occurred previously 
    mp = dict() 
    mp[(0, 0)] = 1

    # zc (Count of zeroes), oc(Count of 1s) 
    # and tc(count of twos) 
    # In starting all counts are zero 
    zc, oc, tc = 0, 0, 0

    # looping into string 
    res = 0 # Initialize result 
    for i in range(n): 

        # increasing the count of current character 
        if string[i] == '0': 
            zc += 1
        elif string[i] == '1': 
            oc += 1
        else: 
            tc += 1 # Assuming that string doesn't contain 
                    # other characters 

        # making pair of differences (z[i] - o[i], 
        # z[i] - t[i]) 
        tmp = (zc - oc, zc - tc) 

        # Count of previous occurrences of above pair 
        # indicates that the subarrays forming from 
        # every previous occurrence to this occurrence 
        # is a subarray with equal number of 0's, 1's 
        # and 2's 
        if tmp not in mp: 
            res += 0
        else: 
            res += mp[tmp] 

        # increasing the count of current difference 
        # pair by 1 
        if tmp in mp: 
            mp[tmp] += 1
        else: 
            mp[tmp] = 1

    return res 

# Driver Code 
if __name__ == "__main__": 
    string = "0102010"
    print(getSubstringWithEqual012(string)) 

# This code is conributed by 
# sanjeev2552 

```

Output:

```
2

```

本文由 **[Utkarsh Trivedi](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)** 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。