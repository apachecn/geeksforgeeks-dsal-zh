# 多集等价问题

与集合不同，多重集可能包含相同编号的多次出现。 *多集*等价问题指出要检查两个给定的多集是否相等。 例如，令 **A** = {1,2,3}， **B** = {1,2,3,3}。 此处设置了 **A** ，但未设置 **B** （B 中出现两次），而 **A** 和 **B** 都是多集。 更正式地说，“对于两个给定的多集，定义为![ \(A' = \{ (a, frequency(a)) | a \in \mathbf{A} \}\) ](img/76708f2dcbd3dea50b7dba1f12a212a1.png "Rendered by QuickLaTeX.com")的对的*集*是否相等？”

给定两个多重集 A 和 B，编写一个程序来检查两个多重集是否相等。

**注意**：多集中的元素可以为 10 <sup>9</sup>

**示例：**

```
Input : A = {1, 1, 3, 4},  
        B = {1, 1, 3, 4}
Output : Yes

Input : A = {1, 3},  
        B = {1, 1}
Output : No

```

由于元素大至 10 ^ 9，因此我们无法使用[直接索引表](https://www.geeksforgeeks.org/direct-address-table/)。

一种解决方案是对两个多集进行排序并一一比较。

## C ++

```

// C++ program to check if two given multisets 
// are equivalent 
#include <bits/stdc++.h> 
using namespace std; 

bool areSame(vector<int>& a, vector<int>& b) 
{ 
    // sort the elements of both multisets 
    sort(a.begin(), a.end()); 
    sort(b.begin(), b.end()); 

    // Return true if both multisets are same. 
    return (a == b); 
} 

int main() 
{ 
    vector<int> a({ 7, 7, 5 }), b({ 7, 5, 5 }); 
    if (areSame(a, b)) 
        cout << "Yes\n"; 
    else
        cout << "No\n"; 
    return 0; 
} 

```

## 爪哇

```

// Java program to check if two given multisets  
// are equivalent  
import java.util.*; 
class GFG { 

static boolean areSame(Vector<Integer>a, Vector<Integer>b)  
{  
    // sort the elements of both multisets  
    Collections.sort(a);  
    Collections.sort(b);  

    // Return true if both multisets are same.  
    return (a == b);  
}  
 public static void main(String[] args) { 
       Vector<Integer> a = new Vector<Integer>(Arrays.asList( 7, 7, 5 )); 
       Vector<Integer> b = new Vector<Integer>(Arrays.asList( 7, 5, 5)); 
    if (areSame(a, b))  
        System.out.print("Yes\n");  
    else
        System.out.print("No\n"); 
    } 
} 
// This code is contributed by PrinciRaj1992 

```

## Python3

```

# Python3 program to check if  
# two given multisets are equivalent 

def areSame(a, b): 

    # sort the elements of both multisets 
    a.sort(); 
    b.sort(); 

    # Return true if both multisets are same. 
    return (a == b); 

# Driver Code 
a = [ 7, 7, 5 ]; 
b = [ 7, 5, 5 ]; 
if (areSame(a, b)): 
    print("Yes"); 
else: 
    print("No"); 

# This code is contributed by Princi Singh 

```

## C＃

```

// C# program to check if two given multisets  
// are equivalent  
using System; 
using System.Collections.Generic; 

class GFG 
{ 

static bool areSame(List<int>a, List<int>b)  
{  
    // sort the elements of both multisets  
    a.Sort(); 
    b.Sort(); 

    // Return true if both multisets are same.  
    return (a == b);  
}  

// Driver code 
public static void Main() 
{ 
    List<int> a = new List<int> { 7, 7, 5 }; 
    List<int> b = new List<int> { 7, 5, 5 }; 
    if (areSame(a, b))  
        Console.WriteLine("Yes\n");  
    else
        Console.WriteLine("No\n"); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
No

```

更好的解决方案是使用哈希。 我们创建了两个空的哈希表（使用 C ++ 中的 [unordered_map 实现）。 我们首先在第一个表中插入第一个多图的所有项目，然后在第二个表中插入第二个多集的所有项目。 现在我们检查两个哈希表是否包含相同的项目和频率。](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)

## C ++

```

// C++ program to check if two given multisets 
// are equivalent 
#include <bits/stdc++.h> 
using namespace std; 

bool areSame(vector<int>& a, vector<int>& b) 
{ 
    if (a.size() != b.size()) 
        return false; 

    // Create two unordered maps m1 and m2 
    // and insert values of both vectors. 
    unordered_map<int, int> m1, m2; 
    for (int i = 0; i < a.size(); i++) { 
        m1[a[i]]++; 
        m2[b[i]]++; 
    } 

    // Now we check if both unordered_maps 
    // are same of not. 
    for (auto x : m1) { 
        if (m2.find(x.first) == m2.end() ||  
            m2[x.first] != x.second) 
            return false; 
    } 

    return true; 
} 

// Driver code 
int main() 
{ 
    vector<int> a({ 7, 7, 5 }), b({ 7, 7, 5 }); 
    if (areSame(a, b)) 
        cout << "Yes\n"; 
    else
        cout << "No\n"; 
    return 0; 
} 

```

## 爪哇

```

// Java program to check if two given multisets 
// are equivalent 
import java.util.*; 

class GFG  
{ 
static boolean areSame(int []a, int []b) 
{ 
    if (a.length != b.length) 
        return false; 

    // Create two unordered maps m1 and m2 
    // and insert values of both vectors. 
    HashMap<Integer, Integer> m1, m2; 
    m1 = new HashMap<Integer, Integer>(); 
    m2 = new HashMap<Integer, Integer>(); 
    for (int i = 0; i < a.length; i++) 
    { 
        if(m1.containsKey(a[i])) 
        { 
            m1.put(a[i], m1.get(a[i]) + 1); 
        } 
        else
        { 
            m1.put(a[i], 1); 
        } 
        if(m2.containsKey(b[i])) 
        { 
            m2.put(b[i], m2.get(b[i]) + 1); 
        } 
        else
        { 
            m2.put(b[i], 1); 
        } 
    } 

    // Now we check if both unordered_maps 
    // are same of not. 
    for (Map.Entry<Integer, Integer> x : m1.entrySet()) 
    { 
        if (!m2.containsKey(x.getKey()) ||  
             m2.get(x.getKey()) != x.getValue()) 
            return false; 
    } 
    return true; 
} 

// Driver code 
public static void main(String args[])  
{ 
    int []a = { 7, 7, 5 }; 
    int []b = { 7, 7, 5 }; 
    if (areSame(a, b)) 
        System.out.println("Yes"); 
    else
        System.out.println("No"); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## C＃

```

// C# program to check if two given multisets 
// are equivalent  
using System; 
using System.Collections.Generic; 

class GFG  
{ 
static bool areSame(int []a, int []b) 
{ 
    if (a.Length != b.Length) 
        return false; 

    // Create two unordered maps m1 and m2 
    // and insert values of both vectors. 
    Dictionary<int, int> m1, m2; 
    m1 = new Dictionary<int, int>(); 
    m2 = new Dictionary<int, int>(); 
    for (int i = 0; i < a.Length; i++) 
    { 
        if(m1.ContainsKey(a[i])) 
        { 
            m1[a[i]] = m1[a[i]] + 1; 
        } 
        else
        { 
            m1.Add(a[i], 1); 
        } 
        if(m2.ContainsKey(b[i])) 
        { 
            m2[b[i]] = m2[b[i]] + 1; 
        } 
        else
        { 
            m2.Add(b[i], 1); 
        } 
    } 

    // Now we check if both unordered_maps 
    // are same of not. 
    foreach(KeyValuePair<int, int> x in m1) 
    { 
        if (!m2.ContainsKey(x.Key) ||  
             m2[x.Key] != x.Value) 
            return false; 
    } 
    return true; 
} 

// Driver code 
public static void Main(String []args)  
{ 
    int []a = { 7, 7, 5 }; 
    int []b = { 7, 7, 5 }; 
    if (areSame(a, b)) 
        Console.WriteLine("Yes"); 
    else
        Console.WriteLine("No"); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
Yes

```

**时间复杂度：** O（n）假定 unordered_map find（）和 insert（）操作在 O（1）时间内工作。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。