# 数组

中的唯一对数

给定 N 个元素的数组，任务是找到可以使用给定数组的元素形成的所有唯一对。
**范例：**

> **输入：** arr [] = {1、1、2}
> **输出：** 4
> （1、1），（1、2），（2、1 ），（2，2）是唯一可能的对。
> 
> **输入：** arr [] = {1、2、3}
> **输出：** 9

**天真的方法：**简单的解决方案是遍历每个可能的对，并将它们添加到集合中，然后找出集合的大小。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number
// of unique pairs in the array
int countUnique(int arr[], int n)
{

    // Set to store unique pairs
    set<pair<int, int> > s;

    // Make all possible pairs
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            s.insert(make_pair(arr[i], arr[j]));

    // Return the size of the set
    return s.size();
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 2, 4, 2, 5, 3, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countUnique(arr, n);
    return 0;
}

```

## 爪哇

```

// Java implementation of the approach
import java.awt.Point;
import java.util.*;

class GFG
{

// Function to return the number
// of unique pairs in the array
static int countUnique(int arr[], int n)
{

    // Set to store unique pairs
    Set<Point> s = new HashSet<>();

    // Make all possible pairs
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            s.add(new Point(arr[i], arr[j]));

    // Return the size of the set
    return s.size();
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 2, 4, 2, 5, 3, 5 };
    int n = arr.length;

    System.out.print(countUnique(arr, n));
}
}

// This code is contributed by 29AjayKumar

```

## Python3

```

# Python3 implementation of the approach

# Function to return the number
# of unique pairs in the array
def countUnique(arr, n):
    # Set to store unique pairs
    s = set()

    # Make all possible pairs
    for i in range(n):
        for j in range(n):
            s.add((arr[i], arr[j]))

    # Return the size of the set
    return len(s)

# Driver code

arr = [ 1, 2, 2, 4, 2, 5, 3, 5 ]
n = len(arr)
print(countUnique(arr, n))

# This code is contributed by ankush_953

```

## C＃

```

// C# implementation of the approach 
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

public class store : IComparer<KeyValuePair<int, int>>
{
    public int Compare(KeyValuePair<int, int> x,
                       KeyValuePair<int, int> y)
    {
        if (x.Key != y.Key)
        {
            return x.Key.CompareTo(y.Key);    
        }
        else
        {
            return x.Value.CompareTo(y.Value);    
        }
    }
}

// Function to return the number 
// of unique pairs in the array 
static int countUnique(int []arr, int n) 
{ 

    // Set to store unique pairs 
    SortedSet<KeyValuePair<int, 
                           int>> s = new  SortedSet<KeyValuePair<int,
                                                                 int>>(new store());

    // Make all possible pairs 
    for(int i = 0; i < n; i++) 
        for(int j = 0; j < n; j++) 
            s.Add(new KeyValuePair<int, int>(arr[i], arr[j])); 

    // Return the size of the set 
    return s.Count; 
} 

// Driver code    
public static void Main(string []arg) 
{
    int []arr = { 1, 2, 2, 4, 2, 5, 3, 5 }; 
    int n = arr.Length; 

    Console.Write(countUnique(arr, n));
}
}

// This code is contributed by rutvik_56

```

**Output:** 

```
25

```

**时间复杂度：**上述实现的时间复杂度为 O（n <sup>2</sup> Log n）。 我们可以使用 [unordered_set 和用户定义的哈希函数](https://www.geeksforgeeks.org/how-to-create-an-unordered_set-of-user-defined-class-or-struct-in-c/)将其优化为 O（n <sup>2</sup> ）。

**高效方法：**首先找出数组中唯一元素的数量。 令唯一元素的数量为 **x** 。 那么，唯一对的数量将是 **x <sup>2</sup>** 。 这是因为每个唯一元素都可以与其他每个唯一元素（包括自身）形成一对。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number
// of unique pairs in the array
int countUnique(int arr[], int n)
{

    unordered_set<int> s;
    for (int i = 0; i < n; i++)
        s.insert(arr[i]);

    int count = pow(s.size(), 2);

    return count;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 2, 4, 2, 5, 3, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countUnique(arr, n);
    return 0;
}

```

## 爪哇

```

// Java implementation of the approach
import java.util.*;

class GFG 
{

    // Function to return the number
    // of unique pairs in the array
    static int countUnique(int arr[], int n) 
    {

        HashSet<Integer> s = new HashSet<>();
        for (int i = 0; i < n; i++)
        {
            s.add(arr[i]);
        }
        int count = (int) Math.pow(s.size(), 2);

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 2, 4, 2, 5, 3, 5};
        int n = arr.length;
        System.out.println(countUnique(arr, n));
    }
}

/* This code has been contributed 
by PrinciRaj1992*/

```

## Python3

```

# Python3 implementation of the approach 

# Function to return the number 
# of unique pairs in the array 
def countUnique(arr, n) :

    s = set(); 
    for i in range(n) :
        s.add(arr[i]); 

    count = pow(len(s), 2); 

    return count; 

# Driver code 
if __name__ == "__main__" : 

    arr = [ 1, 2, 2, 4, 2, 5, 3, 5 ]; 
    n = len(arr);

    print(countUnique(arr, n));

# This code is contributed by Ryuga

```

## C＃

```

// C# implementation of the approach
using System; 
using System.Collections.Generic; 

class GFG 
{

    // Function to return the number
    // of unique pairs in the array
    static int countUnique(int []arr, int n) 
    {

        HashSet<int> s = new HashSet<int>();
        for (int i = 0; i < n; i++)
        {
            s.Add(arr[i]);
        }
        int count = (int) Math.Pow(s.Count, 2);

        return count;
    }

    // Driver code
    static void Main()
    {
        int []arr = {1, 2, 2, 4, 2, 5, 3, 5};
        int n = arr.Length;
        Console.WriteLine(countUnique(arr, n));
    }
}

// This code has been contributed by mits

```

**Output:** 

```
25

```

**时间复杂度：** O（n）

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。