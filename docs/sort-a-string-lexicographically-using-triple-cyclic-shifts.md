# 使用三重循环移位对字符串进行字典排序

> 原文:[https://www . geeksforgeeks . org/sort-a-string-词典编纂-使用三重循环移位/](https://www.geeksforgeeks.org/sort-a-string-lexicographically-using-triple-cyclic-shifts/)

给定一个由前 **N** 个不同字母组成的字符串，任务是通过最多使用 **N/2** 个移动来对字符串进行排序。每一步都包括以下内容:

*   选择任意 3 个不同的索引。
*   在这些索引处对字母执行循环移位。

如果可以对字符串进行排序，则打印所需移动的计数。否则，打印**“不可能”**。

**示例:**

> **输入:** str = "cbda"
> **输出:**
> 可能的
> 1
> **解释:**
> 选择索引 0、2 和 3 并在其中执行单个循环移位，给定的字符串“cbda”被转换为“abcd”。
> 
> **输入:**str = " CBA "
> T3】输出:不可能

**进场:**
为了解决问题，按照以下步骤进行:

*   将表示字符串字符正确的整数存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中。
*   正确放置那些可以在一个周期内占据正确索引的元素。
*   遍历向量的一个元素
*   如果元素不在其排序的索引位置，请检查一个循环中是否可以将两个或多个数字放在正确的索引处。如果条件满足，执行循环，否则检查是否有不包含正确可用元素的不同索引。如果条件满足，选择此索引作为循环的第三个索引并执行循环。如果上述两个条件都不满足，排序将是不可能的。因此，打破循环，打印“不可能”。
*   一旦执行循环换档，存储换档中涉及的**索引**。
*   如果元素位于其排序位置，则移动到下一个索引。
*   对所有矢量元素重复上述两个步骤。
*   遍历完成后，如果整个数组是按排序顺序排列的，则打印所需的移位。否则打印“不可能”。

以下是上述方法的实现:

## C++

```
// C++ Program for sorting a
// string using cyclic shift
// of three indices
#include <bits/stdc++.h>
using namespace std;

void sortString(vector<int>& arr, int n,
                int moves)
{

    // Store the indices
    // which haven't attained
    // its correct position
    vector<int> pos;
    // Store the indices
    // undergoing cyclic shifts
    vector<vector<int> > indices;

    bool flag = false;

    for (int i = 0; i < n; i++) {

        // If the element is not at
        // it's correct position
        if (arr[i] != i) {

            // Check if all 3 indices can be
            // placed to respective correct
            // indices in a single move
            if (arr[arr[arr[i]]] == i
                && arr[arr[i]] != i) {

                int temp = arr[arr[i]];
                indices.push_back({ i, arr[i],
                                    arr[arr[i]] });
                swap(arr[i], arr[arr[i]]);
                swap(arr[i], arr[temp]);
            }
        }

        // If the i-th index is still
        // not present in its correct
        // position, store the index
        if (arr[i] != i) {
            pos.push_back(i);
        }
    }

    for (int i = 0; i < n; i++) {

        if (arr[i] != i) {

            int pos1 = i, pos2 = arr[i];
            int pos3 = arr[arr[i]];

            // To check if swapping two indices
            // places them in their correct
            // position
            if (pos3 != pos1) {

                indices.push_back({ pos1,
                                    pos2,
                                    pos3 });
                swap(arr[pos1], arr[pos2]);
                swap(arr[pos1], arr[pos3]);
                pos.erase(find(
                    pos.begin(),
                    pos.end(), pos2));
                pos.erase(find(
                    pos.begin(),
                    pos.end(), pos3));

                if (arr[pos1] == pos1) {
                    pos.erase(find(
                        pos.begin(),
                        pos.end(),
                        pos1));
                }
            }
            else {

                if (pos3
                    == *pos.begin()) {

                    if (*pos.begin()
                        != pos.back()) {
                        auto it
                            = ++pos.begin();
                        pos3 = *(it);

                        if (*it != pos.back()
                            && pos3 == pos2) {
                            pos3 = *(++it);
                        }
                        else if (*it == pos.back()
                                 && pos3 == pos2) {

                            flag = true;
                            break;
                        }
                    }
                    else {
                        flag = true;
                        break;
                    }
                }

                indices.push_back({ pos1, pos2,
                                    pos3 });
                swap(arr[pos1], arr[pos2]);
                swap(arr[pos1], arr[pos3]);
                pos.erase(find(
                    pos.begin(),
                    pos.end(),
                    pos2));
            }
        }

        if (arr[i] != i) {
            i--;
        }
    }

    if (flag == true
        || indices.size() > moves) {

        cout << "Not Possible" << endl;
    }
    else {
        cout << indices.size() << endl;

        // Inorder to see the indices that
        // were swapped in rotations,
        // uncomment the below code

        /*
        for (int i = 0; i < indices.size();
             i++) {

            cout << indices[i][0] << " "
                 << indices[i][1] << " "
                 << indices[i][2] << endl;
        }
       */
    }
}

// Driver Code
int main()
{

    string s = "adceb";
    vector<int> arr;

    for (int i = 0; i < s.size(); i++) {
        arr.push_back(s[i] - 'a');
    }

    sortString(arr, s.size(),
               floor(s.size() / 2));
}
```

## 蟒蛇 3

```
# Python3 program for sorting a
# string using cyclic shift
# of three indices
import math

def sortString(arr, n, moves):

    # Store the indices
    # which haven't attained
    # its correct position
    pos = []

    # Store the indices
    # undergoing cyclic shifts
    indices = []
    flag = False

    for i in range(n):

        # If the element is not at
        # it's correct position
        if (arr[i] != i):

            # Check if all 3 indices can be
            # placed to respective correct
            # indices in a single move
            if (arr[arr[arr[i]]] == i and
                arr[arr[i]] != i):
                temp = arr[arr[i]]

                indices.append([i, arr[i],
                               arr[arr[i]]])

                sw = arr[i]
                arr[i] = arr[arr[i]]
                arr[sw] = sw

                sw = arr[i]
                arr[i] = arr[temp]
                arr[temp] = sw

        # If the i-th index is still
        # not present in its correct
        # position, store the index
        if (arr[i] != i):
            pos.append(i)

    for i in range(n):
        if (arr[i] != i):
            pos1 = i
            pos2 = arr[i]
            pos3 = arr[arr[i]]

            # To check if swapping two indices
            # places them in their correct
            # position
            if (pos3 != pos1):
                indices.append([pos1, pos2, pos3])
                arr[pos1], arr[pos2] = arr[pos2], arr[pos1]
                arr[pos1], arr[pos3] = arr[pos3], arr[pos1]

                pos.remove(pos2)

                if pos3 in pos:
                    pos.remove(pos3)

                if (arr[pos1] == pos1):
                    pos.remove(pos1)

            else:
                if (pos3 == pos[0]):
                    it = 0

                    if (pos[0] != pos[-1]):
                        it = it + 1
                        pos3 = pos[it]

                        if (pos[it] != pos[-1] and
                               pos3 == pos2):
                            it = it + 1
                            pos3 = pos[it]

                        elif (pos[it] == pos[-1] and
                                 pos3 == pos2):
                            flag = True
                            break

                    else:
                        flag = True
                        break

                indices.append([pos1, pos2, pos3])
                arr[pos1], arr[pos2] = arr[pos2], arr[pos1]
                arr[pos1], arr[pos3] = arr[pos3], arr[pos1]
                pos.remove(pos2)

        if (arr[i] != i):
            i = i - 1

    if (flag == True or len(indices) > moves):
        print("Not Possible")
    else:

        # Inorder to see the indices that
        # were swapped in rotations,
        # uncomment the below code

        # for i in range len(indices):
        #    print (indices[i][0],
        #           indices[i][1], indices[i][2])
        print(len(indices))

# Driver code
s = "adceb"
arr = []

for i in s:
    arr.append(ord(i) - ord('a'))

sortString(arr, len(s), math.floor(len(s) / 2))

# This code is contributed by costheta_z
```

**Output:** 

```
1

```