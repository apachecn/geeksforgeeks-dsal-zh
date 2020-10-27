# 为每个查询找到映射到给定组合键的值

给定三个数组 **firstkey []** ， **secondkey []** 和 **value []** 其中元素 **firstkey [i]** 和 **secondkey [ i]** 表示组合键，其值为 **value [i]** ，任务是回答 **Q** 个查询，每个查询都有两个元素代表复合键，其对应 值需要打印。
**范例：**

> **输入：** firstkey [] = {4，4，5}
> secondkey [] = {2，1，3}
> value [] = {5，3，8}，Q = {（4，1）}
> **输出：** 3
> **说明：**
> 复合键位于 firstkey [1]（= 4）和 secondkey [ 1]（= 1）
> 因此，相应的值为 value [1] = 3
> **输入：** firstkey [] = {3，4，3}
> secondkey [] = {7，1，3}
> value [] = {2，3，6}，Q = {（3，3）}
> **输出：** 6
> **说明 ：**。
> 组合键位于 firstkey [2]（= 3）和 secondkey [2]（= 3）上。
> 因此，相应的值为 value [2] = 6

**方法：**的想法是使用[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，其中映射的键是 C ++中两个整数的[对，它们是 python](https://www.geeksforgeeks.org/pair-in-cpp-stl/) 中的两个整数。 表示 **firstkey []** 和 **secondkey []** 的各个元素，它们映射到相应的 **value []** 元素。 这使我们能够在 **O（1）**时间内回答每个查询。
**例如：**

```
Given arrays be -
firstkey[] = {4, 4, 5}
secondkey[] = {7, 1, 3}
value[] = {5, 3, 8}

Iterating over the Array, the map thus 
formed is {(4, 7): 5, (4, 1): 3, (5, 3): 8}

```

下面是上述方法的实现：

## C ++

```

// C++ implementation to find the 
// value of the given composite keys 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find the composite 
// key value for multiple queries 
void findCompositeKey(int firstkey[], 
                      int secondkey[], int value[], int n, 
                      vector<pair<int, int> > q) 
{ 
    // Map to store the composite 
    // key with a value 
    map<pair<int, int>, int> M; 

    // Iterate over the arrays 
    // and generate the required 
    // mappings 
    for (int i = 0; i < n; i++) { 
        M.insert({ { firstkey[i], secondkey[i] }, 
                   value[i] }); 
    } 

    // Loop to iterate over the 
    // elements of the queries 
    for (auto i : q) { 

        // Condition to check if there 
        // is the composite key in map 
        if (M.find({ i.first, 
                     i.second }) 
            != M.end()) { 
            cout << M[{ i.first, i.second }] 
                 << endl; 
        } 
        else { 
            cout << "Not Found" << endl; 
        } 
    } 
} 

// Driver Code 
int main() 
{ 
    int firstkey[] = { 4, 4, 5 }; 
    int secondkey[] = { 2, 1, 3 }; 
    int value[] = { 5, 3, 8 }; 
    int n = 3; 
    vector<pair<int, int> > q = { { 4, 1 }, 
                                  { 5, 2 }, 
                                  { 5, 3 } }; 

    findCompositeKey(firstkey, secondkey, 
                     value, n, q); 
    return 0; 
} 

```

## 爪哇

```

// Java implementation to find the 
// value of the given composite keys 
import java.util.*; 

class GFG{ 

static class Pair 
{ 
    int first, second; 

    Pair(int first, int second) 
    { 
        this.first = first; 
        this.second = second; 
    } 

    @Override
    public boolean equals(Object obj) 
    { 
        if (obj == null) 
            return false; 
        if (!(obj instanceof Pair)) 
            return false; 
        if (obj == this) 
            return true; 

        return (this.first == ((Pair)obj).first) && 
               (this.second == ((Pair)obj).second); 
    } 

    @Override
    public int hashCode() 
    { 
        return this.first + this.second; 
    } 
} 

// Function to find the composite 
// key value for multiple queries 
static void findCompositeKey(int firstkey[], 
                            int secondkey[],  
                            int value[], int n, 
                            int[][] q) 
{ 

    // Map to store the composite 
    // key with a value 
    Map<Pair, Integer> M = new HashMap<>(); 

    // Iterate over the arrays 
    // and generate the required 
    // mappings 
    for(int i = 0; i < n; i++) 
    { 
        M.put(new Pair(firstkey[i],  
                      secondkey[i]),  
                          value[i]); 
    } 

    // Loop to iterate over the 
    // elements of the queries 
    for(int i = 0; i < q.length; i++) 
    { 

        // Condition to check if there 
        // is the composite key in map 
        if (M.containsKey(new Pair(q[i][0], 
                                   q[i][1]))) 
        { 
            System.out.println(M.get(new Pair(q[i][0], 
                                              q[i][1]))); 
        } 
        else 
        { 
            System.out.println("Not Found"); 
        } 
    } 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int firstkey[] = { 4, 4, 5 }; 
    int secondkey[] = { 2, 1, 3 }; 
    int value[] = { 5, 3, 8 }; 
    int n = 3; 

    int[][] q = { { 4, 1 }, 
                  { 5, 2 }, 
                  { 5, 3 } }; 

    findCompositeKey(firstkey, secondkey, 
                     value, n, q); 
} 
} 

// This code is contributed by offbeat 

```

**Output:** 

```
3
Not Found
8

```

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。