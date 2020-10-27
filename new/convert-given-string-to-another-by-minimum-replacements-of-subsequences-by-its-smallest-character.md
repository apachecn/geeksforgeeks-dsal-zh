# 通过最小替换子序列的最小字符

将给定的字符串转换为另一个字符串

给定两个字符串 **A** 和 **B** ，任务是计算将字符串 **A** 转换​​为 **B** 所需的最小操作数。 在一个操作中，从字符串 **A** 中选择一个子序列，并将该子序列的每个字符转换为其中的最小字符。 如果无法进行转换，则打印**“ -1”** 。
**范例**：

> **输入**：A =“ abcab”，B =“ aabab”
> **输出**：2
> **说明**：
> 操作 1：替换字符 从索引{2，1}中删除那些索引中最小的字符（即“ b”），将 A 转换为“ abbab”。
> 操作 2：将索引{1，0}中的字符替换为这些索引中的最小字符（即“ a”），将 A 转换为“ aabab”。
> 因此，将字符串 A 转换为 B 所需的操作数为 2。
> 
> **输入**：A =“ aaa”，B =“ aab”。
> **输出**：-1
> **说明**：。
> 将 **A** 转换为 **B** 作为字符串 **A** 不含**'b'**的方法。

**方法**：该方法基于以下思想：如果字符串 A 的索引 i 处的任何字符小于字符串 B 的索引 i 处的字符，则不可能将 A 更改为 B，因为更改了字符 字符不能小于自身。 步骤如下：

1.  初始化两个大小为 26 的向量 **convChar** 和 **str1array** 的[数组。这些数组的每个索引对应一个字符。](https://www.geeksforgeeks.org/array-of-vectors-in-c-stl/)
2.  **convChar** 的第<sup>个索引</sup>包含字符串 **A** 的索引，该字符串应转换为第<sup>个</sup>字母和 **str1array [** 包含字符串 A 的所有字符的索引。
3.  初始化一个[哈希映射](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) **convertMap** ，它指示字符串 **A** 的索引 i 处的字符应转换成的特定字符。
4.  同时遍历两个字符串，可能发生三种情况：
    *   如果字符串 **A** 的第<sup>个第</sup>个字符小于字符串 **B** 的第<sup>个第</sup>个字符，则无法更改 **A** 至 **B** 。 因此，打印**“ -1”** 。
    *   如果当前索引上的两个字符相同，则无需更改。
    *   否则，将此索引 i 插入与字符串 **B** 的第 i <sup>个字符</sup>对应的索引的 **convChar** 数组中，并插入第 i 个<sup>的字符值 Hashmap **convertMap** 中字符串 **B** 中的</sup>字符，键值为 i。
5.  初始化计算所需最小操作数的变量 **ret** 和矢量 **retV** ，以存储操作的[集](https://www.geeksforgeeks.org/set-in-cpp-stl/)。
6.  现在，以相反的顺序遍历所有字母。 在每个迭代中执行以下步骤：
    *   检查每个字母，是否至少有一个索引应转换为当前字母。
    *   将**撤消**加 1，以计算所需的步数。 令 **v** 为索引的向量，应将其转换为具有索引 i 的当前字母，而 **v1** 为包含字符串 **A** 的所有索引的向量。 然后可能发生两种情况：
        1.  如果 **v1** 没有元素，则字符串 **A** 中不存在当前字母。 因此，不可能将 A 更改为 B。
        2.  否则，请继续下一步。
    *   对向量 **v1** 的每个索引 **j** 进行迭代。 在此迭代中，搜索要包含在集合 **S** 中的最小索引。
        1.  如果在 **convertMap** 中存在向量 v1 的第<sup>个第</sup>个字母，则表示该字母已被转换或将在操作中转换为另一个字符。 如果已通过以前的操作之一进行了转换，则继续进行 **v1** 的下一次迭代。
        2.  否则将此索引添加到集合中。 跳出循环
    *   如果在向量 **v1** 中找不到任何这样的索引 **j** ，则无法将字符串 **A** 转换​​为 **B** 。 因此打印“ -1”

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach  

#include <bits/stdc++.h>  
using namespace std;  

// Function to return the minimum number  
// of operation  
void transformString(string str1,  
                    string str2)  
{  
    // Storing data  
    int N = str1.length();  

    vector<int> convChar[26];  
    vector<int> str1array[26];  

    // Initialize both arrays  
    for (int i = 0; i < 26; i++) {  
        vector<int> v;  
        convChar[i] = v;  
        str1array[i] = v;  
    }  

    // Stores the index of character  
    map<int, char> convertMap;  

    // Filling str1array, convChar  
    // and hashmap convertMap.  
    for (int i = 0; i < N; i++) {  
        str1array[str1[i] - 'a'].push_back(i);  
    }  

    for (int i = 0; i < N; i++) {  

        // Not possible to convert  
        if (str1[i] < str2[i]) {  
            cout << -1 << endl;  
            return;  
        }  
        else if (str1[i] == str2[i])  
            continue;  
        else {  
            convChar[str2[i] - 'a'].push_back(i);  
            convertMap[i] = str2[i];  
        }  
    }  

    // Calculate result  
    // Initializing return values  
    int ret = 0;  
    vector<vector<int> > retv;  

    // Iterating the character from  
    // the end  
    for (int i = 25; i >= 0; i--) {  

        vector<int> v = convChar[i];  

        if (v.size() == 0)  
            continue;  

        // Increment the number of  
        // operations  
        ret++;  
        vector<int> v1 = str1array[i];  

        // Not possible to convert  
        if (v1.size() == 0) {  
            cout << -1 << endl;  
            return;  
        }  

        // to check whether the final  
        // element has been added  
        // in set S or not.  
        bool isScompleted = false;  

        for (int j = 0; j < v1.size(); j++) {  

            // Check if v1[j] is present  
            // in hashmap or not  
            if (convertMap.find(v1[j])  
                != convertMap.end()) {  

                char a = convertMap[v1[j]];  

                // Already converted then  
                // then continue  
                if (a > i + 'a')  
                    continue;  
                else {  
                    v.push_back(v1[j]);  
                    isScompleted = true;  
                    retv.push_back(v);  
                    break;  
                }  
            }  
            else {  
                v.push_back(v1[j]);  
                isScompleted = true;  
                retv.push_back(v);  
                break;  
            }  
        }  

        // Not possible to convert  
        if (!isScompleted) {  
            cout << -1 << endl;  
            return;  
        }  
    }  

    // Print the result  
    cout << ret << endl;  
}  

// Driver Code  
int main()  
{  
    // Given strings  
    string A = "abcab";  
    string B = "aabab";  

    // Function Call  
    transformString(A, B);  
    return 0;  
}  

```

## Java

```java

// Java program for the above approach  
import java.util.*;  
import java.lang.*;  

class GFG{  

// Function to return the minimum number  
// of operation  
static void transformString(String str1,  
                            String str2)  
{  
    // Storing data  
    int N = str1.length();  
    ArrayList<  
    ArrayList<Integer>> convChar = new ArrayList<>();  
    ArrayList<  
    ArrayList<Integer>> str1array = new ArrayList<>();  

    // Initialize both arrays  
    for(int i = 0; i < 26; i++)  
    {  
        convChar.add(new ArrayList<>());  
        str1array.add(new ArrayList<>());  
    }  

    // Stores the index of character  
    Map<Integer,  
        Character> convertMap = new HashMap<>();  

    // Filling str1array, convChar  
    // and hashmap convertMap.  
    for(int i = 0; i < N; i++)  
    {  
        str1array.get(str1.charAt(i) - 'a').add(i);  
    }  

    for(int i = 0; i < N; i++)  
    {  

        // Not possible to convert  
        if (str1.charAt(i) < str2.charAt(i))  
        {  
            System.out.println(-1);  
            return;  
        }  
        else if (str1.charAt(i) == str2.charAt(i))  
            continue;  
        else
        {  
            convChar.get(str2.charAt(i) - 'a').add(i);  
            convertMap.put(i,str2.charAt(i));  
        }  
    }  

    // Calculate result  
    // Initializing return values  
    int ret = 0;  
    ArrayList<  
    ArrayList<Integer>> retv = new ArrayList<>();  

    // Iterating the character from  
    // the end  
    for(int i = 25; i >= 0; i--)  
    {  
        ArrayList<Integer> v = convChar.get(i);  

        if (v.size() == 0)  
            continue;  

        // Increment the number of  
        // operations  
        ret++;  
        ArrayList<Integer> v1 = str1array.get(i);  

        // Not possible to convert  
        if (v1.size() == 0)  
        {  
            System.out.println(-1);  
            return;  
        }  

        // To check whether the final  
        // element has been added  
        // in set S or not.  
        boolean isScompleted = false;  

        for(int j = 0; j < v1.size(); j++)  
        {  

            // Check if v1[j] is present  
            // in hashmap or not  
            if (convertMap.containsKey(v1.get(j)))  
            {  
                char a = convertMap.get(v1.get(j));  

                // Already converted then  
                // then continue  
                if (a > i + 'a')  
                    continue;  
                else
                {  
                    v.add(v1.get(j));  
                    isScompleted = true;  
                    retv.add(v);  
                    break;  
                }  
            }  
            else
            {  
                v.add(v1.get(j));  
                isScompleted = true;  
                retv.add(v);  
                break;  
            }  
        }  

        // Not possible to convert  
        if (!isScompleted)  
        {  
            System.out.println(-1);  
            return;  
        }  
    }  

    // Print the result  
    System.out.println(ret);  
}  

// Driver Code  
public static void main (String[] args)  
{  

    // Given strings  
    String A = "abcab";  
    String B = "aabab";  

    // Function call  
    transformString(A, B);  
}  
}  

// This code is contributed by offbeat  

```

## Python3

```py

# Python3 program for the above approach 

# Function to return the minimum number 
# of operation 
def transformString(str1, str2): 

    # Storing data 
    N = len(str1) 
    convChar = [] 
    str1array = [] 

    # Initialize both arrays 
    for i in range(26): 
        convChar.append([]) 
        str1array.append([]) 

    # Stores the index of character 
    convertMap = {} 

    # Filling str1array, convChar  
    # and hashmap convertMap. 
    for i in range(N): 
        str1array[ord(str1[i]) -
                  ord('a')].append(i) 

    for i in range(N): 

        # Not possible to convert 
        if (str1[i] < str2[i]): 
            print(-1) 
            return
        elif (str1[i] == str2[i]): 
            continue
        else: 
            convChar[ord(str2[i]) -
                     ord('a')].append(i) 
            convertMap[i] = str2[i] 

    # Calculate result  
    # Initializing return values  
    ret = 0
    retv = [] 

    # Iterating the character from  
    # the end 
    for i in range(25, -1, -1): 
        v = convChar[i] 

        if (len(v) == 0): 
            continue

        # Increment the number of  
        # operations  
        ret += 1; 
        v1 = str1array[i] 

        # Not possible to convert 
        if (len(v1) == 0): 
            print(-1) 
            return

        # To check whether the final  
        # element has been added  
        # in set S or not. 
        isScompleted = False

        for j in range(len(v1)): 

            # Check if v1[j] is present  
            # in hashmap or not  
            if (v1[j] in convertMap): 
                a = v1[j] 

                # Already converted then  
                # then continue  
                if (a > i + ord('a')): 
                    continue
                else: 
                    v.append(v1[j]) 
                    isScompleted = True
                    retv.append(v) 
                    break
            else: 
                v.append(v1[j]) 
                isScompleted = True
                retv.append(v) 
                break

        # Not possible to convert  
        if (isScompleted == False): 
            print(-1) 
            return

    # Print the result 
    print(ret) 

# Driver Code 
A = "abcab"
B = "aabab"

# Function call 
transformString(A, B) 

# This code is contributed by dadi madhav 

```

**Output:** 

```
2

```

***时间复杂度**：O（N）*
***辅助空间**：O（N）*



* * *

* * *



