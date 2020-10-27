# 组移弦

给定一个字符串数组（所有小写字母），任务是对它们进行分组，以使组中的所有字符串彼此移位。 如果两个字符串 S 和 T 称为移位，

```
S.length = T.length 
and
S[i] = T[i] + K for 
1 <= i <= S.length  for a constant integer K

```

例如，字符串{acd，dfg，wyz，yab，mop}是彼此移位的版本。

```
Input  : str[] = {"acd", "dfg", "wyz", "yab", "mop",
                 "bdfh", "a", "x", "moqs"};

Output : a x
         acd dfg wyz yab mop
         bdfh moqs
All shifted strings are grouped together.

```

我们可以看到一组字符串之间的模式，字符串中所有字符的连续字符之间的差是相等的。 如上例所示，取 acd，dfg 和拖把
acd-> 2 1
dfg-> 2 1
mop-> 2 1
，我们可以使用它来识别属于同一组的字符串。 想法是形成一串差异作为关键。 如果找到具有相同差异字符串的字符串，则该字符串也属于同一组。 例如，上述三个字符串具有相同的差异字符串，即“ 21”。
在以下实现中，我们为每个差异添加“ a”，并将 21 存储为“ ba”。

## C++

```cpp

/* C/C++ program to print groups of shifted strings
   together. */
#include <bits/stdc++.h>
using namespace std;
const int ALPHA = 26;   // Total lowercase letter

// Method to a difference string for a given string.
// If string is "adf" then difference string will be
// "cb" (first difference 3 then difference 2)
string getDiffString(string str)
{
    string shift = "";
    for (int i = 1; i < str.length(); i++)
    {
        int dif = str[i] - str[i-1];
        if (dif < 0)
            dif += ALPHA;

        // Representing the difference as char
        shift += (dif + 'a');
    }

    // This string will be 1 less length than str
    return shift;
}

// Method for grouping shifted string
void groupShiftedString(string str[], int n)
{
    // map for storing indices of string which are
    // in same group
    map< string, vector<int> > groupMap;
    for (int i = 0; i < n; i++)
    {
        string diffStr = getDiffString(str[i]);
        groupMap[diffStr].push_back(i);
    }

    // iterating through map to print group
    for (auto it=groupMap.begin(); it!=groupMap.end();
                                                it++)
    {
        vector<int> v = it->second;
        for (int i = 0; i < v.size(); i++)
            cout << str[v[i]] << " ";
        cout << endl;
    }
}

// Driver method to test above methods
int main()
{
    string str[] = {"acd", "dfg", "wyz", "yab", "mop",
                    "bdfh", "a", "x", "moqs"
                   };
    int n = sizeof(str)/sizeof(str[0]);
    groupShiftedString(str, n);
    return 0;
}

```

## Python3

```py

# Python3 program to print groups 
# of shifted strings together.

# Total lowercase letter 
ALPHA = 26

# Method to a difference string 
# for a given string. If string 
# is "adf" then difference string 
# will be "cb" (first difference 
# 3 then difference 2) 
def getDiffString(str):

    shift=""

    for i in range(1, len(str)):
        dif = (ord(str[i]) -
              ord(str[i - 1]))

        if(dif < 0):
            dif += ALPHA

        # Representing the difference 
        # as char 
        shift += chr(dif + ord('a'))

    # This string will be 1 less 
    # length than str 
    return shift

# Method for grouping 
# shifted string 
def groupShiftedString(str,n):

    # map for storing indices 
    # of string which are 
    # in same group
    groupMap = {}

    for i in range(n):
        diffStr = getDiffString(str[i])
        if diffStr not in groupMap:
            groupMap[diffStr] = [i]
        else:
            groupMap[diffStr].append(i)

    # Iterating through map 
    # to print group 
    for it in groupMap:
        v = groupMap[it]
        for i in range(len(v)):
            print(str[v[i]], end = " ")
        print()

# Driver code
str = ["acd", "dfg", "wyz", 
       "yab", "mop","bdfh", 
       "a", "x", "moqs"]
n = len(str)
groupShiftedString(str, n)

# This code is contributed by avanitrachhadiya2155

```

**输出：**

```
a x
acd dfg wyz yab mop
bdfh moqs

```

本文由 **Utkarsh Trivedi** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。
如果发现任何不正确的内容，或者您​​想分享有关上述主题的更多信息，请发表评论。

