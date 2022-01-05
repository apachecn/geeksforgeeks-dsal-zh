# 根据每个字符串中出现的整数对给定句子进行排序

> 原文:[https://www . geesforgeks . org/基于每个字符串中存在的整数对给定句子进行排序/](https://www.geeksforgeeks.org/sort-given-sentence-on-the-basis-of-integer-present-in-every-string/)

给定一个[冗杂的句子](https://www.geeksforgeeks.org/custom-jumble-word-game/)作为字符串的**列表，任务是根据每个字符串中是否存在单个整数来打印字符串的排序句子。如果两个字符串具有相同的整数，则按字典顺序对它们进行排序。**

**示例:**

> **输入:**{“2a”、“grea3t”、“L3 learning”、“geesfor0 geeks”、“p10latform”、“is1”}
> **输出:**geesfor0 geeks is 1 2a grea3t L3 learning p10 latform
> **说明:**由于整数部分的顺序为:0、1、2、3、3、10
> 因此字符串的顺序必须为:
> geesfor0 geeks、is1、2a、grea3t、L3 learning
> 
> **输入:**{“love 9”、“i8s”、“In5dia”}
> 输出: In5dia i8s love9

**方法:**使用 [**贪婪算法**](https://www.geeksforgeeks.org/greedy-algorithms/) **可以解决问题。**我们将创建一个**对列表**，对的第一个值将保持字符串的整数部分，对的第二个值将保持字符串不变，然后我们将按照 [**升序**](https://www.geeksforgeeks.org/sort-even-numbers-ascending-order-sort-odd-numbers-descending-order/) 对这个对列表进行排序，这样具有较低值整数的字符串将在列表中出现得更早。按照以下步骤解决问题:

*   创建一个配对列表，比如说 **A** ，在配对中**第一个**值将是字符串形式的整数，**第二个**值将是字符串形式。
*   [**按递增顺序排序**](https://www.geeksforgeeks.org/python-program-to-sort-a-list-of-tuples-in-increasing-order-by-the-last-element-in-each-tuple/) 。
*   迭代每对 **A** 并打印第二对的**值。**

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

void sortJumbledList(string jumbled[], int size)
{

    // Initializing a list to store pairs
    multimap<int, string> ans;

    // Iterating over JumbledList
    for (int i = 0; i < size; i++) {
        string temp = jumbled[i];

       // Finding integer part
        int number = 0;
        for (int j = 0; j < temp.size(); j++) {
            if (temp[j] >= '0' && temp[j] <= '9') {
                number *= 10;
                number += (temp[j] - '0');
            }
        }

        // Appending pairs
        ans.insert(pair<int, string>(number, jumbled[i]));
    }

   // Printing sorted word of the string.
    for (auto i : ans) {
        cout << i.second << " ";
    }
}

// Driver code
int main()
{
    string JumbledList[] = { "2a",        "grea3t",
                             "l3earning", "geeksfor0geeks",
                             "p5latform", "is1" };

    sortJumbledList(JumbledList, 6);
    return 0;
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python program for above approach
def SortJumbledList(JumbledList):

    # Initializing a list to store pairs
    A = []

    # Iterating over JumbledList
    for string in JumbledList:

        # Finding integer part
        integer = []
        for j in string:
            if j in {'0', '1', '2', '3', \
                         '4', '5', '6', \
                         '7', '8', '9'}:
                integer.append(j)
        integer = ''.join(integer)

        # Appending pairs
        A.append((integer, string))

    # Sorting the list of pairs   
    A.sort()

    # Printing sorted word of the string.
    for integer, string in A:
        print(string, end =' ')

# Driver Code
JumbledList = [ "2a", "grea3t", \
                "l3earning", \
                "geeksfor0geeks", \
                "p5latform", "is1" ]

# Function Call
SortJumbledList(JumbledList)
```

**Output**

```
geeksfor0geeks is1 2a grea3t l3earning p5latform 
```

***时间复杂度:*** O(N*M)，其中 N 为冗杂列表的长度，M 为字符串的长度。
***辅助空间:*** O(N*M)