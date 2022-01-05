# 从小素数数组中移除重复项

> 原文:[https://www . geesforgeks . org/从小素数数组中移除重复项/](https://www.geeksforgeeks.org/remove-duplicates-from-an-array-of-small-primes/)

给定一组素数，使得素数的范围很小。从数组中删除重复项。

**示例:**

```
Input: arr[] = {3, 5, 7, 2, 2, 5, 7, 7};
Output: arr[] = {2, 3, 5, 7}
All the duplicates are removed from 
the array. The output can be printed in any order.

Input: arr[] = {3, 5, 7, 3, 3, 13, 5, 13, 29, 13};
Output: arr[] = {3, 5, 7, 13, 29}
All the duplicates are removed from  
the array. The output can be printed in any order.
```

**来源:** [亚马逊面试问题](https://www.geeksforgeeks.org/amazons-asked-interview-questions/)

**<u>方法 1</u> :** 该方法讨论了时间复杂度为 O(n <sup>2</sup> 的朴素方法。

**进场:**所以基本思路是检查每一个元素，之前有没有发生过。因此，该方法包括保持两个循环，一个选择当前元素或索引，另一个内部循环检查该元素以前是否出现过。

**算法:**

1.  从运行两个循环开始。
2.  逐个挑选所有元素。
3.  对于每个拾取的元素，检查它是否已经发生。
4.  如果已经看到，则忽略它，否则将其添加到数组中。

## C++

```
// A C++ program to implement Naive
// approach to remove duplicates.
#include <bits/stdc++.h>
using namespace std;

int removeDups(vector<int>& vect)
{
    int res_ind = 1;

    // Loop invariant: Elements from vect[0]
    // to vect[res_ind-1] are unique.
    for (int i = 1; i < vect.size(); i++) {
        int j;
        for (j = 0; j < i; j++)
            if (vect[i] == vect[j])
                break;
        if (j == i)
            vect[res_ind++] = vect[i];
    }

    // Removes elements from vect[res_ind] to
    // vect[end]
    vect.erase(vect.begin() + res_ind, vect.end());
}

// Driver code
int main()
{
    vector<int> vect{ 3, 5, 7, 2, 2, 5, 7, 7 };
    removeDups(vect);
    for (int i = 0; i < vect.size(); i++)
        cout << vect[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Naive
// approach to remove duplicates
class GFG {
    static int[] removeDups(int[] vect)
    {
        int res_ind = 1;

        // Loop invariant: Elements from vect[0]
        // to vect[res_ind-1] are unique.
        for (int i = 1; i < vect.length; i++) {
            int j;
            for (j = 0; j < i; j++)
                if (vect[i] == vect[j])
                    break;
            if (j == i)
                vect[res_ind++] = vect[i];
        }

        // Removes elements from vect[res_ind]
        // to vect[end]
        int[] new_arr = new int[res_ind];
        for (int i = 0; i < res_ind; i++)
            new_arr[i] = vect[i];

        return new_arr;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] vect = { 3, 5, 7, 2, 2, 5, 7, 7 };
        vect = removeDups(vect);

        for (int i = 0; i < vect.length; i++)
            System.out.print(vect[i] + " ");
        System.out.println();
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# A Python3 program to implement
# Naive approach to remove duplicates.
def removeDups(vect):

    res_ind = 1

# Loop invariant : Elements from vect[0]
# to vect[res_ind-1] are unique.
    for i in range(1, len(vect)):
        j = 0
        while (j < i):
            if (vect[i] == vect[j]):
                break
            j += 1
        if (j == i):
            vect[res_ind] = vect[i]
            res_ind += 1

# Removes elements from
# vect[res_ind] to vect[end]
    return vect[0:res_ind]

# Driver code
vect = [3, 5, 7, 2, 2, 5, 7, 7]
vect = removeDups(vect)
for i in range(len(vect)):
    print(vect[i], end = " ")

# This code is contributed
# by mohit kumar
```

## C#

```
// C# program to implement Naive approach
// to remove duplicates
using System;

class GFG {
    static int[] removeDups(int[] vect)
    {
        int res_ind = 1;

        // Loop invariant : Elements from vect[0]
        // to vect[res_ind-1] are unique.
        for (int i = 1; i < vect.Length; i++) {
            int j;
            for (j = 0; j < i; j++)
                if (vect[i] == vect[j])
                    break;
            if (j == i)
                vect[res_ind++] = vect[i];
        }

        // Removes elements from vect[res_ind]
        // to vect[end]
        int[] new_arr = new int[res_ind];
        for (int i = 0; i < res_ind; i++)
            new_arr[i] = vect[i];

        return new_arr;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] vect = { 3, 5, 7, 2, 2, 5, 7, 7 };
        vect = removeDups(vect);

        for (int i = 0; i < vect.Length; i++)
            Console.Write(vect[i] + " ");
        Console.WriteLine();
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to implement Naive
// approach to remove duplicates

    function removeDups(vect)
    {
        let res_ind = 1;

        // Loop invariant: Elements from vect[0]
        // to vect[res_ind-1] are unique.
        for (let i = 1; i < vect.length; i++) {
            let j;
            for (j = 0; j < i; j++)
                if (vect[i] == vect[j])
                    break;
            if (j == i)
                vect[res_ind++] = vect[i];
        }

        // Removes elements from vect[res_ind]
        // to vect[end]
        let new_arr = new Array(res_ind);
        for (let i = 0; i < res_ind; i++)
            new_arr[i] = vect[i];

        return new_arr;
    }

      // Driver Code
    let vect=[3, 5, 7, 2, 2, 5, 7, 7];
    vect = removeDups(vect);
    for (let i = 0; i < vect.length; i++)
        document.write(vect[i] + " ");
    document.write("<br>");

// This code is contributed by unknown2108

</script>
```

**输出:**

```
3 5 7 2
```

**复杂度分析:**

*   **时间复杂度:** O(n <sup>2</sup> )。
    由于使用了两个嵌套循环，因此时间复杂度变为 O(n <sup>2</sup> )。
*   **空间复杂度:** O(n)。
    由于额外的数组用于存储元素，空间复杂度为 O(n)。

**<u>方法二</u> :** 该方法涉及排序技术，需要 O(n log n)时间。

**方法:**与之前的方法相比，更好的解决方案是首先对数组进行排序，然后从排序后的数组中移除所有相似的相邻元素。

**算法:**

1.  首先对数组进行排序。
2.  可以巧妙地避免对额外空间的需求。保留两个变量，*先* = 1， *i* = 1。
3.  从第二个元素到最后遍历数组。
4.  对于每个元素，如果该元素不等于前一个元素，则*数组【first++】=数组【I】*，其中 *i* 是循环的计数器。
5.  所以没有重复的数组长度为*第一个*，去掉其余元素。

**注意:**在 CPP 中有一些内置的功能，比如**排序()**排序和**唯一()**删除相邻的重复项。unique()函数将所有唯一元素放在开头，并返回一个迭代器，指向唯一元素之后的第一个元素。 **erase()** 函数移除两个给定迭代器之间的元素。

## C++

```
// C++ program to remove duplicates using Sorting
#include <bits/stdc++.h>
using namespace std;

int removeDups(vector<int>& vect)
{
    // Sort the vector
    sort(vect.begin(), vect.end());

    // unique() removes adjacent duplicates.
    // unique function puts all unique elements at
    // the beginning and returns iterator pointing
    // to the first element after unique element.
    // Erase function removes elements between two
    // given iterators
    vect.erase(unique(vect.begin(), vect.end()),
               vect.end());
}

// Driver code
int main()
{
    vector<int> vect{ 3, 5, 7, 2, 2, 5, 7, 7 };
    removeDups(vect);
    for (int i = 0; i < vect.size(); i++)
        cout << vect[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove duplicates using Sorting
import java.util.*;

class GFG {

    static int[] removeDups(int[] vect)
    {
        // sort the array
        Arrays.sort(vect);

        // pointer
        int first = 1;

        // remove duplicate elements
        for (int i = 1; i < vect.length; i++)
            if (vect[i] != vect[i - 1])
                vect[first++] = vect[i];

        // mark rest of elements to INT_MAX
        for (int i = first; i < vect.length; i++)
            vect[i] = Integer.MAX_VALUE;

        return vect;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] vect = { 3, 5, 7, 2, 2, 5, 7, 7 };
        vect = removeDups(vect);
        for (int i = 0; i < vect.length; i++) {
            if (vect[i] == Integer.MAX_VALUE)
                break;
            System.out.print(vect[i] + " ");
        }
    }
}
```

## 蟒蛇 3

```
# Python3 program to remove duplicates
# using Sorting
import sys

def removeDups(vect):

    # Sort the array
    vect.sort()

    # Pointer
    first = 1

    # Remove duplicate elements
    for i in range(1, len(vect)):
        if (vect[i] != vect[i - 1]):
            vect[first] = vect[i]
            first += 1

    # Mark rest of elements to INT_MAX
    for  i in range(first, len(vect)):
        vect[i] = sys.maxsize

    return vect

# Driver code
vect = [ 3, 5, 7, 2, 2, 5, 7, 7 ]
vect = removeDups(vect)

for i in range(len(vect)):
    if (vect[i] == sys.maxsize):
        break

    print(vect[i], end = " ")

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to remove duplicates using Sorting
using System;
class GFG
{
    static int[] removeDups(int[] vect)
    {

        // sort the array
        Array.Sort(vect);

        // pointer
        int first = 1;

        // remove duplicate elements
        for (int i = 1; i < vect.Length; i++)
            if (vect[i] != vect[i - 1])
                vect[first++] = vect[i];

        // mark rest of elements to INT_MAX
        for (int i = first; i < vect.Length; i++)
            vect[i] = int.MaxValue;
        return vect;
    }

    // Driver code
    public static void Main(params string[] args)
    {
        int[] vect = { 3, 5, 7, 2, 2, 5, 7, 7 };
        vect = removeDups(vect);
        for (int i = 0; i < vect.Length; i++)
        {
            if (vect[i] == int.MaxValue)
                break;
            Console.Write(vect[i] + " ");
        }
    }
}

// This code is contributed by rutvik_56.
```

## java 描述语言

```
<script>
// Javascript program to remove duplicates using Sorting

function removeDups(vect) {
    // Sort the vector
    vect.sort((a, b) => a - b)

    // pointer
    let first = 1;

    // remove duplicate elements
    for (let i = 1; i < vect.length; i++){
        if (vect[i] != vect[i - 1])
            vect[first++] = vect[i];
    }

    // mark rest of elements to INT_MAX
    for (let i = first; i < vect.length; i++)
        vect[i] = Number.MAX_SAFE_INTEGER;

    return vect;
}

    // Driver code
    let vect = [ 3, 5, 7, 2, 2, 5, 7, 7 ];
    removeDups(vect);
    for (let i = 0; i < vect.length; i++) {
        if (vect[i] == Number.MAX_SAFE_INTEGER)
            break;
        document.write(vect[i] + " ");
    }

</script>
```

**输出:**

```
2 3 5 7
```

**复杂度分析:**

*   **时间复杂度:** O(n Log n)。
    排序数组*需要 O(n log n )* 时间复杂度，去除相邻元素*需要 O(n)* 时间复杂度。
*   **辅助空间:** O(1)
    由于不需要额外空间，空间复杂度不变。

**<u>方法 3</u> :** 该方法涉及哈希技术，耗时 O(n)。

**方法:**这种方法的时间复杂度可以降低，但空间复杂度会带来代价。这涉及到哈希的使用，在哈希映射中标记数字，这样如果再次遇到数字，就可以从数组中删除它。

**算法:**

1.  使用哈希集。HashSet 只存储唯一的元素。
2.  众所周知，如果将两个相同的元素放入一个哈希集中，哈希集中只存储一个元素(所有重复的元素都会消失)
3.  从头到尾遍历数组。
4.  对于每个元素，将该元素插入到哈希集中
5.  现在遍历 HashSet，并将 HashSet 中的元素放入数组中

## C++

```
// C++ program to remove duplicates using Hashing
#include <bits/stdc++.h>
using namespace std;

int removeDups(vector<int>& vect)
{
    // Create a set from vector elements
    unordered_set<int> s(vect.begin(), vect.end());

    // Take elements from set and put back in
    // vect[]
    vect.assign(s.begin(), s.end());
}

// Driver code
int main()
{
    vector<int> vect{ 3, 5, 7, 2, 2, 5, 7, 7 };
    removeDups(vect);
    for (int i = 0; i < vect.size(); i++)
        cout << vect[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Naive approach to
// remove duplicates.
import java.util.*;

class GFG {

    static void removeDups(Vector<Integer> vect)
    {

        // Create a set from vector elements
        Set<Integer> set = new HashSet<Integer>(vect);

        // Take elements from set and put back in
        // vect[]
        vect.clear();
        vect.addAll(set);
    }

    // Driver code
    public static void main(String[] args)
    {
        Integer arr[] = { 3, 5, 7, 2, 2, 5, 7, 7 };
        Vector<Integer> vect
            = new Vector<Integer>(
                Arrays.asList(arr));
        removeDups(vect);
        for (int i = 0; i < vect.size(); i++) {
            System.out.print(vect.get(i) + " ");
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to remove duplicates using Hashing
def removeDups():
    global vect

    # Create a set from vector elements
    s = set(vect)

    # Take elements from set and put back in
    # vect[]
    vect = s

# Driver code
vect = [3, 5, 7, 2, 2, 5, 7, 7]
removeDups()
for i in vect:
    print(i, end = " ")

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to implement Naive approach to
// remove duplicates.
using System;
using System.Collections.Generic;
using System.Linq;

class GFG {

    static List<int> removeDups(List<int> vect)
    {

        // Create a set from vector elements
        HashSet<int> set = new HashSet<int>(vect);

        // Take elements from set and put back in
        // vect[]
        vect.Clear();
        vect = set.ToList();
        return vect;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 3, 5, 7, 2, 2, 5, 7, 7 };
        List<int> vect = new List<int>(arr);
        vect = removeDups(vect);
        for (int i = 0; i < vect.Count; i++) {
            Console.Write(vect[i] + " ");
        }
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to implement Naive approach to
// remove duplicates.

function removeDups(vect)
{
    // Create a set from vector elements
        letset = new Set(vect);

        // Take elements from set and put back in
        // vect[]
        vect=[];
        vect=Array.from(letset);
        return vect;
}

// Driver code
let vect=[3, 5, 7, 2, 2, 5, 7, 7 ];
vect=removeDups(vect);
for (let i = 0; i < vect.length; i++) {
    document.write(vect[i] + " ");
}

// This code is contributed by rag2127

</script>
```

**输出:**

```
2 7 5 3
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    由于需要单次遍历才能进入 hashmap 中的所有元素，因此时间复杂度为 *O(n)* 。
*   **辅助空间:** O(n)。
    为了在 HashSet 或 hashmap 中存储元素 *O(n)* 需要空间复杂度。

**<u>方法 4</u> :** 这专注于时间复杂度为 0(n)的小范围值。

**方法:**该方法仅在所有不同素数的乘积小于 **10^18** 并且数组中的所有数字都应该是素数时有效。素数除了 1 之外没有除数的性质或这个数本身被用来得出解。当数组元素从数组中移除时，它们会保留一个值(乘积)，该值将包含数组中以前找到的所有不同素数的乘积，因此，如果元素对乘积进行除法运算，它们可以确定证明该元素以前曾出现在数组中，因此该数字将被拒绝。

**算法:**

1.  最初，保留一个变量(p = 1)。
2.  从头到尾遍历数组。
3.  遍历时，检查 p 是否能被第 I 个元素整除。如果为真，则删除该元素。
4.  否则保留该元素，并通过将该元素乘以乘积(p = p * arr[i])来更新乘积

## C++

```
// Removes duplicates using multiplication of
// distinct primes in array
#include <bits/stdc++.h>
using namespace std;

int removeDups(vector<int>& vect)
{
    long long int prod = vect[0];
    int res_ind = 1;
    for (int i = 1; i < vect.size(); i++) {
        if (prod % vect[i] != 0) {
            vect[res_ind++] = vect[i];
            prod *= vect[i];
        }
    }
    vect.erase(vect.begin() + res_ind, vect.end());
}

// Driver code
int main()
{
    vector<int> vect{ 3, 5, 7, 2, 2, 5, 7, 7 };
    removeDups(vect);
    for (int i = 0; i < vect.size(); i++)
        cout << vect[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Removes duplicates using multiplication of
// distinct primes in array
import java.util.*;

class GFG {

    static int[] removeDups(int[] vect)
    {

        int prod = vect[0];
        int res_ind = 1;
        for (int i = 1; i < vect.length; i++) {
            if (prod % vect[i] != 0) {
                vect[res_ind++] = vect[i];
                prod *= vect[i];
            }
        }
        return Arrays.copyOf(vect, res_ind);
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] vect = { 3, 5, 7, 2, 2, 5, 7, 7 };
        vect = removeDups(vect);
        for (int i = 0; i < vect.length; i++)
            System.out.print(vect[i] + " ");
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Removes duplicates using multiplication of
# distinct primes in array
def removeDups(vect):
    prod = vect[0]
    res_ind = 1
    i = 1
    while (i < len(vect)):
        if (prod % vect[i] != 0):
            vect[res_ind] = vect[i]
            res_ind += 1
            prod *= vect[i]
        vect = vect[:res_ind + 2]
        i += 1
    return vect

# Driver code
vect = [3, 5, 7, 2, 2, 5, 7, 7]
vect = removeDups(vect)
for i in range(len(vect)):
    print(vect[i], end =" ")

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// Removes duplicates using multiplication of
// distinct primes in array
using System;

class GFG {

    static int[] removeDups(int[] vect)
    {

        int prod = vect[0];
        int res_ind = 1;
        for (int i = 1; i < vect.Length; i++) {
            if (prod % vect[i] != 0) {
                vect[res_ind++] = vect[i];
                prod *= vect[i];
            }
        }
        int[] temp = new int[vect.Length - res_ind];
        Array.Copy(vect, 0, temp, 0, temp.Length);
        return temp;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] vect = { 3, 5, 7, 2, 2, 5, 7, 7 };
        vect = removeDups(vect);
        for (int i = 0; i < vect.Length; i++)
            Console.Write(vect[i] + " ");
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Removes duplicates using multiplication of
// distinct primes in array

function removeDups(vect)
{
    let prod = vect[0];
        let res_ind = 1;
        for (let i = 1; i < vect.length; i++) {
            if (prod % vect[i] != 0) {
                vect[res_ind++] = vect[i];
                prod *= vect[i];
                vect=vect.slice(0,res_ind + 2);
            }
        }
        return vect;
}

// Driver code
let vect=[3, 5, 7, 2, 2, 5, 7, 7];
vect = removeDups(vect);
document.write(vect.join(" "));

// This code is contributed by rag2127
</script>
```

**输出:**

```
3 5 7 2
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    遍历阵只需一次，所需时间为 **O(n)** 。
*   **辅助空间:** O(1)。
    需要一个变量 p，所以空间复杂度不变。

**注意:**如果阵列中有任何复合物，该解决方案将不起作用。

本文由**希瓦姆·米塔尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息