# 竞争性编程的频率测量技术

> 原文:[https://www . geeksforgeeks . org/frequency-measurement-technologies-for-competitive-programming/](https://www.geeksforgeeks.org/frequency-measurement-techniques-for-competitive-programming/)

测量数组中元素的频率是一项非常方便的技能，并且需要许多竞争性的编码问题。在许多问题中，我们需要测量各种元素的频率，如数字、字母、符号等。作为我们问题的一部分。

**天真法**

**示例:**

```
Input :  arr[] = {10, 20, 20, 10, 10, 20, 5, 20}
Output : 10 3
         20 4
         5  1

Input : arr[] = {10, 20, 20}
Output : 10 2
         20 1
```

我们运行两个循环。对于每个项目计数的次数。为了避免重复打印，请跟踪已处理的项目。

## C++

```
// C++ program to count frequencies of array items
#include <bits/stdc++.h>
using namespace std;

void countFreq(int arr[], int n)
{
    // Mark all array elements as not visited
    vector<int> visited(n, false);

    // Traverse through array elements and
    // count frequencies
    for (int i = 0; i < n; i++) {

        // Skip this element if already processed
        if (visited[i] == true)
            continue;

        // Count frequency
        int count = 1;
        for (int j = i + 1; j < n; j++) {
            if (arr[i] == arr[j]) {
                visited[j] = true;
                count++;
            }
        }
        cout << arr[i] << " " << count << endl;
    }
}

int main()
{
    int arr[] = { 10, 20, 20, 10, 10, 20, 5, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);
    countFreq(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count frequencies
// of array items
import java.util.*;

class GFG
{
static void countFreq(int arr[], int n)
{
    // Mark all array elements as not visited
    boolean []visited = new boolean[n];

    // Traverse through array elements and
    // count frequencies
    for (int i = 0; i < n; i++)
    {

        // Skip this element if already processed
        if (visited[i] == true)
            continue;

        // Count frequency
        int count = 1;
        for (int j = i + 1; j < n; j++)
        {
            if (arr[i] == arr[j])
            {
                visited[j] = true;
                count++;
            }
        }
        System.out.println(arr[i] + " " + count);
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 10, 20, 20, 10, 10, 20, 5, 20 };
    int n = arr.length;
    countFreq(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to count frequencies
# of array items
def countFreq(arr, n):

    # mark all array elements as not visited
    visited = [False for i in range(n)]

    # Traverse through array elements
    # and count frequencies
    for i in range(n):

        # Skip this element if already processed
        if visited[i] == True:
            continue

        # count frequency
        count = 1

        for j in range(i + 1, n):
            if arr[i] == arr[j]:
                visited[j] = True
                count += 1
        print(arr[i], count)

# Driver code
a = [10, 20, 20, 10, 10, 20, 5, 20]

n = len(a)

countFreq(a, n)

# This code is contributed
# by Mohit kumar 29
```

## C#

```
// C# program to count frequencies
// of array items
using System;

class GFG
{
static void countFreq(int []arr, int n)
{
    // Mark all array elements as not visited
    Boolean []visited = new Boolean[n];

    // Traverse through array elements and
    // count frequencies
    for (int i = 0; i < n; i++)
    {

        // Skip this element if already processed
        if (visited[i] == true)
            continue;

        // Count frequency
        int count = 1;
        for (int j = i + 1; j < n; j++)
        {
            if (arr[i] == arr[j])
            {
                visited[j] = true;
                count++;
            }
        }
        Console.WriteLine(arr[i] + " " + count);
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 10, 20, 20, 10,
                  10, 20, 5, 20 };
    int n = arr.Length;
    countFreq(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to count frequencies of array items

    function countFreq(arr, n)
    {
        // Mark all array elements as not visited
        let visited = new Array(n);
        visited.fill(false);

        // Traverse through array elements and
        // count frequencies
        for (let i = 0; i < n; i++) {

            // Skip this element if already processed
            if (visited[i] == true)
                continue;

            // Count frequency
            let count = 1;
            for (let j = i + 1; j < n; j++) {
                if (arr[i] == arr[j]) {
                    visited[j] = true;
                    count++;
                }
            }
            document.write(arr[i] + " " + count + "</br>");
        }
    }

    let arr = [ 10, 20, 20, 10, 10, 20, 5, 20 ];
    let n = arr.length;
    countFreq(arr, n);

    // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
10 3
20 4
5 1
```

**优化方法:**

**测量元素受值限制时的频率**
如果我们的输入数组有小值，我们可以使用数组元素作为计数数组中的索引，并增加计数。在下面的示例中，元素最多为 10 个。

```
Input :  arr[] = {5, 5, 6, 6, 5, 6, 1, 2, 3, 10, 10}
         limit = 10
Output : 1 1
         2 1
         3 1
         5 3
         6 3
         10 2
```

## C++

```
// C++ program to count frequencies of array items
// having small values.
#include <bits/stdc++.h>
using namespace std;

void countFreq(int arr[], int n, int limit)
{
    // Create an array to store counts. The size
    // of array is limit+1 and all values are
    // initially 0
    vector<int> count(limit+1, 0);

    // Traverse through array elements and
    // count frequencies (assuming that elements
    // are limited by limit)
    for (int i = 0; i < n; i++)
        count[arr[i]]++;

    for (int i = 0; i <= limit; i++)
       if (count[i] > 0)
        cout << i << " " << count[i] << endl;

}

int main()
{
    int arr[] = {5, 5, 6, 6, 5, 6, 1, 2, 3, 10, 10};
    int n = sizeof(arr) / sizeof(arr[0]);
    int limit = 10;
    countFreq(arr, n, limit);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count frequencies of array items
// having small values.
class GFG
{

static void countFreq(int arr[], int n, int limit)
{
    // Create an array to store counts. The size
    // of array is limit+1 and all values are
    // initially 0
    int []count = new int[limit + 1];

    // Traverse through array elements and
    // count frequencies (assuming that elements
    // are limited by limit)
    for (int i = 0; i < n; i++)
        count[arr[i]]++;

    for (int i = 0; i <= limit; i++)
    if (count[i] > 0)
            System.out.println(i + " " + count[i]);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = {5, 5, 6, 6, 5, 6, 1, 2, 3, 10, 10};
    int n = arr.length;
    int limit = 10;
    countFreq(arr, n, limit);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to count frequencies of
# array items having small values.
def countFreq(arr, n, limit):

    # Create an array to store counts.
    # The size of array is limit+1 and
    # all values are initially 0
    count = [0 for i in range(limit + 1)]

    # Traverse through array elements and
    # count frequencies (assuming that
    # elements are limited by limit)
    for i in range(n):
        count[arr[i]] += 1

    for i in range(limit + 1):
        if (count[i] > 0):
            print(i, count[i])

# Driver Code
arr = [ 5, 5, 6, 6, 5, 6,
        1, 2, 3, 10, 10 ]
n = len(arr)
limit = 10

countFreq(arr, n, limit)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to count frequencies of
// array items having small values.
using System;

class GFG
{

static void countFreq(int []arr,
                      int n, int limit)
{
    // Create an array to store counts.
    // The size of array is limit+1 and
    // all values are initially 0
    int []count = new int[limit + 1];

    // Traverse through array elements and
    // count frequencies (assuming that
    // elements are limited by limit)
    for (int i = 0; i < n; i++)
        count[arr[i]]++;

    for (int i = 0; i <= limit; i++)
    if (count[i] > 0)
            Console.WriteLine(i + " " +
                              count[i]);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {5, 5, 6, 6, 5, 6,
                 1, 2, 3, 10, 10};
    int n = arr.Length;
    int limit = 10;
    countFreq(arr, n, limit);
}
}

// This code is contributed
// by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to count frequencies
// of array items having small values.
function countFreq(arr, n, limit)
{

    // Create an array to store counts.
    // The size of array is limit+1 and
    // all values are initially 0
    let count = new Array(limit + 1);
    count.fill(0);

    // Traverse through array elements and
    // count frequencies (assuming that
    // elements are limited by limit)
    for(let i = 0; i < n; i++)
        count[arr[i]]++;

    for(let i = 0; i <= limit; i++)
        if (count[i] > 0)
            document.write(i + " " +
                           count[i] + "</br>");
}

// Driver code
let arr = [ 5, 5, 6, 6, 5, 6,
            1, 2, 3, 10, 10 ];
let n = arr.length;
let limit = 10;

countFreq(arr, n, limit);

// This code is contributed by rameshtravel07  

</script>
```

**Output:** 

```
1 1
2 1
3 1
5 3
6 3
10 2
```

## C++

```
// C++ program to count frequencies of array items
#include <bits/stdc++.h>
using namespace std;

const int limit = 255;

void countFreq(string str)
{
    // Create an array to store counts. The size
    // of array is limit+1 and all values are
    // initially 0
    vector<int> count(limit+1, 0);

    // Traverse through string characters and
    // count frequencies
    for (int i = 0; i < str.length(); i++)
        count[str[i]]++;

    for (int i = 0; i <= limit; i++)
       if (count[i] > 0)
        cout << (char)i << " " << count[i] << endl;

}

int main()
{
    string str = "GeeksforGeeks";
    countFreq(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count frequencies of array items
class GFG
{
static int limit = 255;

static void countFreq(String str)
{
    // Create an array to store counts. The size
    // of array is limit+1 and all values are
    // initially 0
    int []count= new int[limit + 1];

    // Traverse through string characters and
    // count frequencies
    for (int i = 0; i < str.length(); i++)
        count[str.charAt(i)]++;

    for (int i = 0; i <= limit; i++)
    if (count[i] > 0)
        System.out.println((char)i + " " + count[i]);
}

// Driver Code
public static void main(String[] args)
{
    String str = "GeeksforGeeks";
    countFreq(str);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to count frequencies of array items
limit = 255
def countFreq(Str) :

    # Create an array to store counts. The size
    # of array is limit+1 and all values are
    # initially 0
    count = [0] * (limit + 1)

    # Traverse through string characters and
    # count frequencies
    for i in range(len(Str)) :
        count[ord(Str[i])] += 1

    for i in range(limit + 1) :
       if (count[i] > 0) :
        print(chr(i), count[i])

Str = "GeeksforGeeks"
countFreq(Str)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to count frequencies
// of array items
using System;

class GFG
{
static int limit = 25;

static void countFreq(String str)
{
    // Create an array to store counts.
    // The size of array is limit+1 and
    // all values are initially 0
    int []count = new int[limit + 1];

    // Traverse through string characters
    // and count frequencies
    for (int i = 0; i < str.Length; i++)
        count[str[i] - 'A']++;

    for (int i = 0; i <= limit; i++)
    if (count[i] > 0)
        Console.WriteLine((char)(i + 'A') +
                          " " + count[i]);
}

// Driver Code
public static void Main(String[] args)
{
    String str = "GEEKSFORGEEKS";
    countFreq(str);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to count frequencies of array items

    let limit = 255;

function countFreq(str)
{
        // Create an array to store counts. The size
    // of array is limit+1 and all values are
    // initially 0
    let count= new Array(limit + 1);
    for(let i=0;i<count.length;i++)
    {
        count[i]=0;
    }

    // Traverse through string characters and
    // count frequencies
    for (let i = 0; i < str.length; i++)
        count[str[i].charCodeAt(0)]++;

    for (let i = 0; i <= limit; i++)
    {    if (count[i] > 0)
            document.write(String.fromCharCode(i) + " " + count[i]+"<br>");
    }
}

// Driver Code
let str = "GeeksforGeeks";
countFreq(str);

    // This code is contributed by unknown2108
</script>
```

**Output:** 

```
G 2
e 4
f 1
k 2
o 1
r 1
s 2
```

**测量元素在有限范围内的频率**
例如，考虑一个只包含大写字母的字符串。字符串的元素限制在从“A”到“Z”的范围内。其思想是减去最小的元素(本例中为“A”)，得到元素的索引。

## C++

```
// C++ program to count frequencies of array items
#include <bits/stdc++.h>
using namespace std;

const int limit = 25;

void countFreq(string str)
{
    // Create an array to store counts. The size
    // of array is limit+1 and all values are
    // initially 0
    vector<int> count(limit+1, 0);

    // Traverse through string characters and
    // count frequencies
    for (int i = 0; i < str.length(); i++)
        count[str[i] - 'A']++;

    for (int i = 0; i <= limit; i++)
       if (count[i] > 0)
        cout << (char)(i + 'A') << " " << count[i] << endl;

}

int main()
{
    string str = "GEEKSFORGEEKS";
    countFreq(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count frequencies
// of array items
import java.util.*;

class GFG
{
static int limit = 25;

static void countFreq(String str)
{
    // Create an array to store counts.
    // The size of array is limit+1 and
    // all values are initially 0
    int []count = new int[limit + 1];

    // Traverse through string characters
    // and count frequencies
    for (int i = 0; i < str.length(); i++)
        count[str.charAt(i) - 'A']++;

    for (int i = 0; i <= limit; i++)
    if (count[i] > 0)
        System.out.println((char)(i + 'A') +
                           " " + count[i]);
}

// Driver Code
public static void main(String[] args)
{
    String str = "GEEKSFORGEEKS";
    countFreq(str);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to count frequencies of array items
limit = 25;
def countFreq(str):

    # Create an array to store counts. The size
    # of array is limit+1 and all values are
    # initially 0
    count = [0 for i in range(limit + 1)]

    # Traverse through string characters and
    # count frequencies
    for i in range(len(str)):  
        count[ord(str[i]) - ord('A')] += 1

    for i in range(limit + 1):
       if (count[i] > 0):
           print(chr(i + ord('A')), count[i])

# Driver code
if __name__=='__main__':

    str = "GEEKSFORGEEKS";
    countFreq(str);

# This code is contributed by Pratham76
```

## C#

```
// C# program to count frequencies
// of array items
using System;

class GFG
{
static int limit = 25;

static void countFreq(String str)
{
    // Create an array to store counts.
    // The size of array is limit+1 and
    // all values are initially 0
    int []count = new int[limit + 1];

    // Traverse through string characters
    // and count frequencies
    for (int i = 0; i < str.Length; i++)
        count[str[i] - 'A']++;

    for (int i = 0; i <= limit; i++)
    if (count[i] > 0)
        Console.WriteLine((char)(i + 'A') +
                           " " + count[i]);
}

// Driver Code
public static void Main(String[] args)
{
    String str = "GEEKSFORGEEKS";
    countFreq(str);
}
}

// This code contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to count frequencies
// of array items

let limit = 25;
function countFreq(str)
{
    // Create an array to store counts.
    // The size of array is limit+1 and
    // all values are initially 0
    let count = new Array(limit + 1);
    for(let i=0;i<limit+1;i++)
    {
        count[i]=0;
    }

    // Traverse through string characters
    // and count frequencies
    for (let i = 0; i < str.length; i++)
        count[str[i].charCodeAt(0) - 'A'.charCodeAt(0)]++;

    for (let i = 0; i <= limit; i++)
    if (count[i] > 0)
        document.write(String.fromCharCode(i + 'A'.charCodeAt(0)) +
                           " " + count[i]+"<br>");
}

// Driver Code
let str = "GEEKSFORGEEKS";
countFreq(str);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
E 4
F 1
G 2
K 2
O 1
R 1
S 2
```

**无范围无限制的情况下测量频率**
想法是用哈希法([c++中的无序 _ map](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)和[HashMap【Java 中的 T6】来获取频率。](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)

## C++

```
// C++ program to count frequencies of array items
#include <bits/stdc++.h>
using namespace std;

void countFreq(int arr[], int n)
{
    unordered_map<int, int> mp;

    // Traverse through array elements and
    // count frequencies
    for (int i = 0; i < n; i++)
        mp[arr[i]]++;

    // Traverse through map and print frequencies
    for (auto x : mp)
        cout << x.first << " " << x.second << endl;
}

int main()
{
    int arr[] = { 10, 20, 20, 10, 10, 20, 5, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);
    countFreq(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count frequencies of array items
import java.util.*;
class GFG
{
static void countFreq(int arr[], int n)
{
    HashMap<Integer,
            Integer>mp = new HashMap<Integer,
                                     Integer>();

    // Traverse through array elements and
    // count frequencies
    for (int i = 0 ; i < n; i++)
    {
        if(mp.containsKey(arr[i]))
        {
            mp.put(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.put(arr[i], 1);
        }
    }

    // Traverse through map and print frequencies
    for (Map.Entry<Integer,
                   Integer> entry : mp.entrySet())
        System.out.println(entry.getKey() + " " +
                           entry.getValue());
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 10, 20, 20, 10, 10, 20, 5, 20 };
    int n = arr.length;
    countFreq(arr, n);   
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to count frequencies of array items
def countFreq(arr, n):

    mp = {}

    # Traverse through array elements and
    # count frequencies
    for i in range(n):
        if arr[i] in mp:
            mp[arr[i]] += 1
        else:
            mp[arr[i]] = 1

    # Traverse through map and print frequencies
    for x in sorted(mp):
        print(x, mp[x])

# Driver Code
arr = [ 10, 20, 20, 10, 10, 20, 5, 20 ]
n = len(arr)

countFreq(arr, n)

# This code is contributed by divyesh072019
```

## C#

```
// C# program to count frequencies of array items
using System;
using System.Collections.Generic;

class GFG
{
static void countFreq(int []arr, int n)
{
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Traverse through array elements and
    // count frequencies
    for (int i = 0 ; i < n; i++)
    {
        if(mp.ContainsKey(arr[i]))
        {
            var val = mp[arr[i]];
            mp.Remove(arr[i]);
            mp.Add(arr[i], val + 1);
        }
        else
        {
            mp.Add(arr[i], 1);
        }
    }

    // Traverse through map and print frequencies
    foreach(KeyValuePair<int, int> entry in mp)
        Console.WriteLine(entry.Key + " " +
                          entry.Value);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 10, 20, 20, 10,
                  10, 20, 5, 20 };
    int n = arr.Length;
    countFreq(arr, n);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to count frequencies of array items
function  countFreq(arr, n)
{
    let mp = new Map();

    // Traverse through array elements and
    // count frequencies
    for (let i = 0 ; i < n; i++)
    {
        if(mp.has(arr[i]))
        {
            mp.set(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.set(arr[i], 1);
        }
    }

    // Traverse through map and print frequencies
    for (let [key, value] of mp.entries())
        document.write(key + " " +
                           value+"<br>");
}

// Driver Code
let arr=[10, 20, 20, 10, 10, 20, 5, 20];
let n = arr.length;
countFreq(arr, n);  

// This code is contributed by ab2127
</script>
```

**Output:** 

```
5 1
10 3
20 4
```

***时间复杂度:*** O(n)
***辅助空间:*** O(n)

**在上述高效解决方案中，如何按照元素在输入中出现的顺序打印元素？**

## C++

```
// C++ program to count frequencies of array items
#include <bits/stdc++.h>
using namespace std;

void countFreq(int arr[], int n)
{
    unordered_map<int, int> mp;

    // Traverse through array elements and
    // count frequencies
    for (int i = 0; i < n; i++)
        mp[arr[i]]++;

    // To print elements according to first
    // occurrence, traverse array one more time
    // print frequencies of elements and mark
    // frequencies as -1 so that same element
    // is not printed multiple times.
    for (int i = 0; i < n; i++) {
      if (mp[arr[i]] != -1)
      {
          cout << arr[i] << " " << mp[arr[i]] << endl;
          mp[arr[i]] = -1;
      }
    }
}

int main()
{
    int arr[] = { 10, 20, 20, 10, 10, 20, 5, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);
    countFreq(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count frequencies of array items
import java.util.*;

class GFG
{
static void countFreq(int arr[], int n)
{
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    // Traverse through array elements and
    // count frequencies
    for (int i = 0 ; i < n; i++)
    {
        if(mp.containsKey(arr[i]))
        {
            mp.put(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.put(arr[i], 1);
        }
    }

    // To print elements according to first
    // occurrence, traverse array one more time
    // print frequencies of elements and mark
    // frequencies as -1 so that same element
    // is not printed multiple times.
    for (int i = 0; i < n; i++)
    {
        if (mp.get(arr[i]) != -1)
        {
            System.out.println(arr[i] + " " +
                               mp.get(arr[i]));
            mp. put(arr[i], -1);
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 10, 20, 20, 10, 10, 20, 5, 20 };
    int n = arr.length;
    countFreq(arr, n);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to count frequencies of array items
def countFreq(arr, n):
    mp = {}

    # Traverse through array elements and
    # count frequencies
    for i in range(n):
        if arr[i] not in mp:
            mp[arr[i]] = 1
        else:
            mp[arr[i]] += 1

    # To print elements according to first
    # occurrence, traverse array one more time
    # print frequencies of elements and mark
    # frequencies as -1 so that same element
    # is not printed multiple times.
    for i in range(n):
        if(mp[arr[i]] != -1):
            print(arr[i], mp[arr[i]])
            mp[arr[i]] = -1

# Driver code
arr = [10, 20, 20, 10, 10, 20, 5, 20 ]
n = len(arr)
countFreq(arr, n)

# This code is contributed by rag2127
```

## C#

```
// C# program to count frequencies of array items
using System;
using System.Collections.Generic;

class GFG
{
static void countFreq(int []arr, int n)
{
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Traverse through array elements and
    // count frequencies
    for (int i = 0 ; i < n; i++)
    {
        if(mp.ContainsKey(arr[i]))
        {
            mp[arr[i]] = mp[arr[i]] + 1;
        }
        else
        {
            mp.Add(arr[i], 1);
        }
    }

    // To print elements according to first
    // occurrence, traverse array one more time
    // print frequencies of elements and mark
    // frequencies as -1 so that same element
    // is not printed multiple times.
    for (int i = 0; i < n; i++)
    {
        if (mp[arr[i]] != -1)
        {
            Console.WriteLine(arr[i] + " " +
                              mp[arr[i]]);
            mp[arr[i]] = - 1;
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 10, 20, 20, 10,
                  10, 20, 5, 20 };
    int n = arr.Length;
    countFreq(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to count
// frequencies of array items
function countFreq(arr, n)
{
    let mp = new Map();

    // Traverse through array elements and
    // count frequencies
    for(let i = 0 ; i < n; i++)
    {
        if (mp.has(arr[i]))
        {
            mp.set(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.set(arr[i], 1);
        }
    }

    // To print elements according to first
    // occurrence, traverse array one more time
    // print frequencies of elements and mark
    // frequencies as -1 so that same element
    // is not printed multiple times.
    for(let i = 0; i < n; i++)
    {
        if (mp.get(arr[i]) != -1)
        {
            document.write(arr[i] + " " +
                    mp.get(arr[i]) + "<br>");
            mp.set(arr[i], -1);
        }
    }
}

// Driver Code
let arr = [ 10, 20, 20, 10, 10, 20, 5, 20 ];
let n = arr.length;   

countFreq(arr, n);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
10 3
20 4
5 1
```

***时间复杂度:*** O(n)
***辅助空间:*** O(n)

在 Java 中，我们可以使用 [LinkedHashMap](https://www.geeksforgeeks.org/linkedhashmap-class-java-examples/) 以相同的顺序获取元素。因此，我们不需要额外的循环。
很多问题都是基于频率测量的，如果我们知道如何计算给定数组中各种元素的频率，那将是一个难题。例如，尝试下面给出的基于频率测量的问题:

1.  [**字谜**](https://practice.geeksforgeeks.org/problems/anagram-1587115620/1)
2.  [**按频率对数组元素进行排序**](https://practice.geeksforgeeks.org/problems/sorting-elements-of-an-array-by-frequency/0)
3.  [**单号**](https://practice.geeksforgeeks.org/problems/single-number1014/1)

本文由 [**阿迪蒂亚·古普塔**](https://auth.geeksforgeeks.org/profile.php?user=Aditya%2520Gupta%25204&list=practice) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。