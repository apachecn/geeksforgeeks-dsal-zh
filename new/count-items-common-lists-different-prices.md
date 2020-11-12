# 计算两个清单共有但价格不同的商品

> 原文：[https://www.geeksforgeeks.org/count-items-common-lists-different-prices/](https://www.geeksforgeeks.org/count-items-common-lists-different-prices/)

给定两个列表，分别包含`m`和`n`个项目的`list1`和`list2`。 每个项目都与两个字段关联：名称和价格。 问题是要计算两个列表中价格不同的商品。

**示例**：

```
Input : list1[] = {{"apple", 60}, {"bread", 20}, 
                   {"wheat", 50}, {"oil", 30}}
    list2[] = {{"milk", 20}, {"bread", 15}, 
                   {"wheat", 40}, {"apple", 60}}
Output : 2
bread and wheat are the two items common to both the
lists but with different prices.

```

**来源**：[Cognizant 面试经验 | 系列 5](https://www.geeksforgeeks.org/cognizant-interview-experience-set-5-campus-associate/)

**方法 1（朴素方法）**：使用两个嵌套循环将`list1`的每个项目与`list2`的所有项目进行比较。 如果找到价格不同的匹配项，则增加`count`。

## C++

```cpp

// C++ implementation to count items common to both 
// the lists but with different prices
#include <bits/stdc++.h>

using namespace std;

// details of an item
struct item
{
    string name;
    int price;
};

// function to count items common to both 
// the lists but with different prices
int countItems(item list1[], int m,
               item list2[], int n)
{
    int count = 0;

    // for each item of 'list1' check if it is in 'list2'
    // but with a different price
    for (int i = 0; i < m; i++)    
        for (int j = 0; j < n; j++) 

            if ((list1[i].name.compare(list2[j].name) == 0) &&
                 (list1[i].price != list2[j].price))
                count++;        

    // required count of items
    return count;
}

// Driver program to test above
int main()
{
    item list1[] = {{"apple", 60}, {"bread", 20},
                    {"wheat", 50}, {"oil", 30}};
    item list2[] = {{"milk", 20}, {"bread", 15},
                   {"wheat", 40}, {"apple", 60}};

    int m = sizeof(list1) / sizeof(list1[0]);
    int n = sizeof(list2) / sizeof(list2[0]);    

    cout << "Count = "   
         << countItems(list1, m, list2, n);

    return 0;     
} 

```

## Java

```java

// Java implementation to count items common to both 
// the lists but with different prices
class GFG{

// details of an item
static class item
{
    String name;
    int price;
    public item(String name, int price) {
        this.name = name;
        this.price = price;
    }
};

// function to count items common to both 
// the lists but with different prices
static int countItems(item list1[], int m,
            item list2[], int n)
{
    int count = 0;

    // for each item of 'list1' check if it is in 'list2'
    // but with a different price
    for (int i = 0; i < m; i++) 
        for (int j = 0; j < n; j++) 

            if ((list1[i].name.compareTo(list2[j].name) == 0) &&
                (list1[i].price != list2[j].price))
                count++;     

    // required count of items
    return count;
}

// Driver code
public static void main(String[] args)
{
    item list1[] = {new item("apple", 60), new item("bread", 20),
                new item("wheat", 50), new item("oil", 30)};
        item list2[] = {new item("milk", 20), new item("bread", 15),
                new item("wheat", 40), new item("apple", 60)};

    int m = list1.length;
    int n = list2.length; 

    System.out.print("Count = "
        + countItems(list1, m, list2, n));

}     
} 

// This code is contributed by 29AjayKumar

```

## Python3

```py

# Python implementation to
# count items common to both 
# the lists but with different
# prices

# function to count items
# common to both 
# the lists but with different prices
def countItems(list1, list2):
    count = 0

    # for each item of 'list1'
    # check if it is in 'list2'
    # but with a different price
    for i in list1:
        for j in list2:

            if i[0] == j[0] and i[1] != j[1]:
                count += 1

    # required count of items
    return count

# Driver program to test above
list1 = [("apple", 60), ("bread", 20),
            ("wheat", 50), ("oil", 30)]
list2 = [("milk", 20), ("bread", 15),
            ("wheat", 40), ("apple", 60)]

print("Count = ", countItems(list1, list2))

# This code is contributed by Ansu Kumari.

```

## C#

```cs

// C# implementation to count items common to both 
// the lists but with different prices
using System;

class GFG{

// details of an item
class item
{
    public String name;
    public int price;
    public item(String name, int price) {
        this.name = name;
        this.price = price;
    }
};

// function to count items common to both 
// the lists but with different prices
static int countItems(item []list1, int m,
            item []list2, int n)
{
    int count = 0;

    // for each item of 'list1' check if it is in 'list2'
    // but with a different price
    for (int i = 0; i < m; i++) 
        for (int j = 0; j < n; j++) 

            if ((list1[i].name.CompareTo(list2[j].name) == 0) &&
                (list1[i].price != list2[j].price))
                count++;     

    // required count of items
    return count;
}

// Driver code
public static void Main(String[] args)
{
    item []list1 = {new item("apple", 60), new item("bread", 20),
                new item("wheat", 50), new item("oil", 30)};
        item []list2 = {new item("milk", 20), new item("bread", 15),
                new item("wheat", 40), new item("apple", 60)};

    int m = list1.Length;
    int n = list2.Length; 

    Console.Write("Count = "
        + countItems(list1, m, list2, n));

}     
}
// This code is contributed by PrinciRaj1992

```

输出：

```
Count = 2

```

时间复杂度：`O(m * n)`。

辅助空间：`O(1)`。

**方法 2（二分搜索）**：按项目名称的字母顺序对`list2`排序。 现在，使用二分搜索技术针对`list1`的每个项目检查其是否存在于`list2`中，并从`list2`获得价格。 如果价格不同，则增加`count`。

## CPP

```

// C++ implementation to count items common to both 
// the lists but with different prices
#include <bits/stdc++.h>

using namespace std;

// details of an item
struct item
{
    string name;
    int price;
};

// comparator function used for sorting
bool compare(struct item a, struct item b) 
{
    return (a.name.compare(b.name) <= 0);        
}

// function to search 'str' in 'list2[]'. If it exists then
// price associated with 'str' in 'list2[]' is being
// returned else -1 is returned. Here binary serach 
// trechnique is being applied for searching
int binary_search(item list2[], int low, int high, string str)
{
    while (low <= high)
    {
        int mid = (low + high) / 2;

        // if true the item 'str' is in 'list2'         
        if (list2[mid].name.compare(str) == 0)
            return list2[mid].price;

        else if (list2[mid].name.compare(str) < 0)    
            low = mid + 1;

        else
            high = mid - 1;    
    }

    // item 'str' is not in 'list2'         
    return -1;
}

// function to count items common to both 
// the lists but with different prices
int countItems(item list1[], int m,
               item list2[], int n)
{
    // sort 'list2' in alphabetcal order of
    // items name
    sort(list2, list2 + n, compare);

    // initial count
    int count = 0;

    for (int i = 0; i < m; i++) {

        // get the price of item 'list1[i]' from 'list2'
        // if item in not present in second list then
        // -1 is being obtained
        int r = binary_search(list2, 0, n-1, list1[i].name);

        // if item is present in list2 with a 
        // different price
        if ((r != -1) && (r != list1[i].price))
            count++;
    }

    // required count of items
    return count;
}

// Driver program to test above
int main()
{
    item list1[] = {{"apple", 60}, {"bread", 20}, 
                     {"wheat", 50}, {"oil", 30}};
    item list2[] = {{"milk", 20}, {"bread", 15},
                   {"wheat", 40}, {"apple", 60}};

    int m = sizeof(list1) / sizeof(list1[0]);
    int n = sizeof(list2) / sizeof(list2[0]);    

    cout << "Count = "   
         << countItems(list1, m, list2, n);

    return 0;     
}

```

输出：

```
Count = 2

```

时间复杂度：`(m * log2(n))`。

辅助空间：`O(1)`。

为了提高效率，应对元素数量最大的列表排序，并将其用于二分搜索。

**方法 3（有效方法）**：使用（项目名称，价格）元组作为（键，值）创建哈希表。 在哈希表中插入`list1`的元素。 现在，对于`list2`的每个元素，检查它是否是哈希表。 如果存在，则检查其价格是否与哈希表中的值不同。 如果是这样，则增加`count`。
## C++

```cpp

// C++ implementation to count items common to both 
// the lists but with different prices
#include <bits/stdc++.h>

using namespace std;

// details of an item
struct item
{
    string name;
    int price;
};

// function to count items common to both 
// the lists but with different prices
int countItems(item list1[], int m,
               item list2[], int n)
{
    // 'um' implemented as hash table that contains
    // item name as the key and price as the value
    // associated with the key
    unordered_map<string, int> um;
    int count = 0;

    // insert elements of 'list1' in 'um'
    for (int i = 0; i < m; i++)
        um[list1[i].name] = list1[i].price;

    // for each element of 'list2' check if it is 
    // present in 'um' with a different price
    // value
    for (int i = 0; i < n; i++)    
        if ((um.find(list2[i].name) != um.end()) &&
            (um[list2[i].name] != list2[i].price))
            count++;

    // required count of items        
    return count;        
}

// Driver program to test above
int main()
{
    item list1[] = {{"apple", 60}, {"bread", 20}, 
                    {"wheat", 50}, {"oil", 30}};
    item list2[] = {{"milk", 20}, {"bread", 15}, 
                    {"wheat", 40}, {"apple", 60}};

    int m = sizeof(list1) / sizeof(list1[0]);
    int n = sizeof(list2) / sizeof(list2[0]);    

    cout << "Count = "   
         << countItems(list1, m, list2, n);

    return 0;     
}

```

## Java

```java

// Java implementation to count
// items common to both the lists
// but with different prices
import java.util.*;
class GFG{

// details of an item
static class item
{
  String name;
  int price;
  public item(String name, int price) 
  {
    this.name = name;
    this.price = price;
  }
};

// function to count items common to both 
// the lists but with different prices
static int countItems(item list1[], int m,
                      item list2[], int n)
{
  // 'um' implemented as hash table that contains
  // item name as the key and price as the value
  // associated with the key
  HashMap<String, 
          Integer> um = new HashMap<>();
  int count = 0;

  // insert elements of 'list1' in 'um'
  for (int i = 0; i < m; i++)
    um.put(list1[i].name, list1[i].price);

  // for each element of 'list2' check if it is 
  // present in 'um' with a different price
  // value
  for (int i = 0; i < n; i++)    
    if ((um.containsKey(list2[i].name)) &&
        (um.get(list2[i].name) != list2[i].price))
      count++;

  // required count of items        
  return count;        
}

// Driver program to test above
public static void main(String[] args)
{
  item list1[] = {new item("apple", 60), 
                  new item("bread", 20),
                  new item("wheat", 50), 
                  new item("oil", 30)};
  item list2[] = {new item("milk", 20), 
                  new item("bread", 15),
                  new item("wheat", 40), 
                  new item("apple", 60)};

  int m = list1.length;
  int n = list2.length; 

  System.out.print("Count = " + 
                    countItems(list1, m, 
                              clist2, n));
}     
}

// This code is contributed by gauravrajput1

```

## C#

```cs

// C# implementation to count
// items common to both the lists
// but with different prices
using System;
using System.Collections.Generic;
class GFG{

// Details of an item
public class item
{
  public String name;
  public int price;
  public item(String name, 
              int price) 
  {
    this.name = name;
    this.price = price;
  }
};

// Function to count items common to 
// both the lists but with different prices
static int countItems(item []list1, int m,
                      item []list2, int n)
{
  // 'um' implemented as hash table 
  // that contains item name as the 
  // key and price as the value
  // associated with the key
  Dictionary<String, 
             int> um = new Dictionary<String, 
                                      int>();
  int count = 0;

  // Insert elements of 'list1' 
  // in 'um'
  for (int i = 0; i < m; i++)
    um.Add(list1[i].name, 
           list1[i].price);

  // For each element of 'list2' 
  // check if it is present in 
  // 'um' with a different price
  // value
  for (int i = 0; i < n; i++)    
    if ((um.ContainsKey(list2[i].name)) &&
        (um[list2[i].name] != list2[i].price))
      count++;

  // Required count of items        
  return count;        
}

// Driver code
public static void Main(String[] args)
{
  item []list1 = {new item("apple", 60), 
                  new item("bread", 20),
                  new item("wheat", 50), 
                  new item("oil", 30)};
  item []list2 = {new item("milk", 20), 
                  new item("bread", 15),
                  new item("wheat", 40), 
                  new item("apple", 60)};
  int m = list1.Length;
  int n = list2.Length; 
  Console.Write("Count = " + 
                countItems(list1, m,  
                           list2, n));
}     
}

// This code is contributed by shikhasingrajput

```

**输出**：

```
Count = 2

```

时间复杂度：`O(m + n)`。

辅助空间：`O(m)`。

为了提高效率，应在哈希表中插入元素数量最少的列表。



* * *

* * *



