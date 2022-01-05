# 添加元素开始排序数组|斯大林排序的变体

> 原文:[https://www . geesforgeks . org/add-elements-in-start-to-sort-the-array-variation-of-Stalin-sort/](https://www.geeksforgeeks.org/add-elements-in-start-to-sort-the-array-variation-of-stalin-sort/)

[Stalin sort](https://www.geeksforgeeks.org/remove-elements-to-make-array-sorted/) (也称“**独裁者排序**”和“ **trump sort** ”)是一种无意义的“排序”算法，其中每个顺序不正确的元素都被简单地从列表中删除。
这种排序算法是斯大林排序的一种破坏性较小的变体，它实际上会对列表进行排序:在这种情况下，不按顺序的元素会按照它们在原始列表中出现的顺序移动到列表的开头。然后重复该过程，直到列表被排序。

**示例:**

> **输入:** arr[] = {2，1，4，3，6，5，8，7，10，9}
> **输出:** 1 2 3 4 5 6 7 8 9 10
> **解释:**
> 移动到列表开头的那些元素标为粗体:
> 【2，1，4，3，6，5，8，7，10，9】
> 【**1，3，5，7，9 8** 、1、3、5、7、9、10】
> 【**1、3、5、7、** 2、4、6、8、9、10】
> 【**2、4、6、** 1、3、5、7、8、9、10】
> 【**1、3、5、** 2、4、6、7、8、9、10】
> 【
> 10]
> 【**2、** 1、3、4、5、6、7、8、9、10】
> 【**1、** 2、3、4、5、6、7、8、9、10】
> 
> **输入:**【9、10、7、8、5、6、3、4、1、2】
> **输出:**【1、2、3、4、5、6、7、8、9、10】
> **解释:**
> 【9、10、7、8、5、6、3、4、1、2】
> 【**7、8、5、6、3、4、1、2** 、 5、6、7、8、9、10]
> [ **1、2** 、3、4、5、6、7、8、9、10]

**方法:**想法是每当数组的元素少于前一个元素时，就在数组的开始处推送元素。重复此步骤，直到没有顺序不正确的元素。

下面是上述方法的实现:

## C++

```
// C++ implementation to sort the
// array by using the variation
// of the Stalin sort
#include<bits/stdc++.h>
using namespace std;

// Function to sort the array
void variationStalinsort(vector<int> arr)
{
    int j = 0;

    while(true)
    {
        int moved = 0;

        for(int i = 0;
                i < (arr.size() - 1 - j); i++)
        {
            if (arr[i] > arr[i + 1])
            {
                vector<int>::iterator index;
                int temp;
                index = arr.begin() + i + 1;
                temp = arr[i + 1];
                arr.erase(index);
                arr.insert(arr.begin() + moved, temp);
                moved++;
            }
        }

        j++;

        if (moved == 0)
        {
            break;
        }
    }
    for(int i = 0; i < arr.size(); i++)
    {
        cout << arr[i] << ", ";
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 2, 1, 4, 3, 6,
                        5, 8, 7, 10, 9 };

    // Function call
    variationStalinsort(arr);
}

// This code is contributed by avanitrachhadiya2155
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to sort the
// array by using the variation
// of the Stalin sort
import java.util.*;
class GFG
{

  // Function to sort the array
  static void variationStalinsort(Vector<Integer> arr)
  {
    int j = 0;
    while(true)
    {
      int moved = 0; 
      for(int i = 0;
          i < (arr.size() - 1 - j); i++)
      {
        if (arr.get(i) > arr.get(i+1))
        {
          //Iterator<Integer> index = arr.iterator();
          int index;
          int temp;
          index = arr.get(i);
          temp = arr.get(i + 1);
          arr.removeElement(index);
          arr.add( i, temp);
          arr.removeElement(temp);
          arr.add(i+1, index);
          moved++;
        }
      }  
      j++;    
      if (moved == 0)
      {
        break;
      }
    }
    System.out.print(arr);

  }

  // Driver Code
  public static void main(String[] args)
  {
    int[] arr = { 2, 1, 4, 3, 6,
                 5, 8, 7, 10, 9 };
    Vector<Integer> arr1 = new Vector<>();
    for(int i = 0; i < arr.length; i++)
      arr1.add(arr[i]);

    // Function call
    variationStalinsort(arr1);
  }
}

// This code is contributed by aashish1995
```

## 蟒蛇 3

```
# Python3 implementation to sort
# the array by using the variation
# of the Stalin sort

# Function to sort the array
def variationStalinsort(arr):
    j = 0
    while True:
        moved = 0
        for i in range(len(arr) - 1 - j):
            if arr[i] > arr[i + 1]:
                arr.insert(moved, arr.pop(i + 1))
                moved += 1
        j += 1
        if moved == 0:
            break
    return arr

# Driver Code
if __name__ == "__main__":
    arr = [2, 1, 4, 3, 6, 5, 8, 7, 10, 9]

    # Function Call
    print(variationStalinsort(arr))
```

## C#

```
// C# implementation to sort the
// array by using the variation
// of the Stalin sort
using System;
using System.Collections.Generic;
using System.Linq;
class GFG
{

  // Function to sort the array
  static void variationStalinsort(List<int> arr)
  {
    int j = 0;
    while(true)
    {
      int moved = 0; 
      for(int i = 0;
          i < (arr.Count - 1 - j); i++)
      {
        if (arr[i] > arr[i+1])
        {

          //Iterator<Integer> index = arr.iterator();
          int index;
          int temp;
          index = arr[i];
          temp = arr[i + 1];
          arr.Remove(index);
          arr.Insert(i , temp);
          arr.Remove(temp);
          arr.Insert(i + 1 ,index);
          moved++;
        }
      }  
      j++;    
      if (moved == 0)
      {
        break;
      }
    }
    foreach(int i in arr)
    Console.Write(i + " ");

  }

  // Driver Code
  public static void Main(string[] args)
  {
    int[] arr = { 2, 1, 4, 3, 6,
                 5, 8, 7, 10, 9 };
    List<int> arr1 = new List<int>();
    for(int i = 0; i < arr.Length; i++)
      arr1.Add(arr[i]);

    // Function call
    variationStalinsort(arr1);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript implementation to sort the
// array by using the variation
// of the Stalin sort

// Function to sort the array
function variationStalinsort(arr)
{
    let j = 0;
    while(true)
    {
        let moved = 0;
        for(let i = 0;
                i < (arr.length - 1 - j);
                i++)
        {
            if (arr[i] > arr[i+1])
            {

                // Iterator<Integer> index = arr.iterator();
                let index;
                let temp;
                index = arr[i];
                temp = arr[i + 1];
                arr.splice(i, 1);
                arr.splice(i, 0, temp);
                arr[i] = temp;
                arr.splice(i + 1, 1);
                arr.splice(i + 1, 0, index)
                arr[i + 1] = index;
                moved++;
            }
        } 
        j++;   
        if (moved == 0)
        {
            break;
        }
    }
    document.write("[" + arr + "]");
}

// Driver Code
let arr = [ 2, 1, 4, 3, 6,
            5, 8, 7, 10, 9 ];
let arr1 = [];
for(let i = 0; i < arr.length; i++)
    arr1.push(arr[i]);

// Function call
variationStalinsort(arr1);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

***最差时间复杂度:**O(N<sup>2</sup>)*
***最佳时间复杂度:** O(N)*