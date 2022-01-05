# 用给定的字符串包装给定单词的每个连续实例

> 原文:[https://www . geesforgeks . org/用给定字符串包装给定单词的每个连续实例/](https://www.geeksforgeeks.org/wrap-every-continuous-instance-of-given-word-with-some-given-string/)

给两串 **S1** 和 **S2** 。任务是用绳子把每一根绳子 **S2** 缠绕在绳子 **S1** 的两边。
**注意:**这里我们将使用**下划线(_)** 作为包裹部分。根据需要可以是任何东西，比如一些 [HTML 标签](https://www.geeksforgeeks.org/most-commonly-used-tags-in-html/)，空格等。
**举例:**

> **输入:**S1 =“exam will a exam 考试”，S2 =“exam”
> **输出:**“_ exam _ will a _ exam 考试 _”
> **解释:**
> 字符串 S2 是“**考试**，所以用下划线将出现的 S2 括起来。因为最后两个出现重叠(在字符串**示例**中)，所以通过将下划线放在合并子字符串的更左和更右来合并出现和换行。
> **输入:**str = " abcbabc ABC "，substr = "abc"
> **输出:**" _ abcbabc ABC _ "

**方法:**想法是简单地获取字符串 **S2** 在 **S1** 中的所有实例的位置，并在出现的任一端添加下划线，如果两个或更多的 **S2** 实例重叠，则在合并的子字符串的任一端添加下划线。以下是步骤:

1.  获取主字符串 **S1** 中字符串 **S2** 的所有实例的位置。对于遍历字符串 **S1** 一次一个字符，调用子串匹配函数，[查找()](https://www.geeksforgeeks.org/string-find-in-cpp/)。
2.  创建一个位置的 2D 数组(比如说 **arr[][]** )，其中每个子数组保存字符串 **S2** 在字符串 **S1** 中的特定实例的开始和结束索引。
3.  [合并存储在 arr[][]中的重叠开始和结束索引间隔](https://www.geeksforgeeks.org/merging-intervals/)。
4.  在上述步骤之后，所有重叠的索引被合并。现在同时遍历给定的字符串和间隔，并通过换行下划线创建一个新的字符串。
5.  在上述步骤之后打印新字符串。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function Definitions
vector<vector<int> > getLocations(string str,
                                  string subStr);

vector<vector<int> > collapse(
    vector<vector<int> > locations);

string underscorify(string str,
                    vector<vector<int> > locations);

// Function that creates the string by
// wrapping the underscore
string underscorifySubstring(string str,
                             string subStr)
{

    // Function Call to intervals of
    // starting and ending index
    vector<vector<int> > locations
        = collapse(getLocations(str, subStr));

    // Function Call
    return underscorify(str, locations);
}

// Function finds all starting and ending
// index of the substring in given string
vector<vector<int> > getLocations(string str,
                                  string subStr)
{
    vector<vector<int> > locations{};
    int startIdx = 0;

    int L = subStr.length();

    // Traverse string str
    while (startIdx < str.length()) {

        // Find substr
        int nextIdx = str.find(subStr,
                               startIdx);

        // If location found, then insert
        // pair int location[]
        if (nextIdx != string::npos) {

            locations.push_back({ nextIdx,
                                  (nextIdx + L) });

            // Update the start index
            startIdx = nextIdx + 1;
        }
        else {
            break;
        }
    }
    return locations;
}

// Function to merge the locations
// of substrings that overlap each
// other or sit next to each other
vector<vector<int> > collapse(
    vector<vector<int> > locations)
{
    if (locations.empty()) {
        return locations;
    }

    // 2D vector to store the merged
    // location of substrings
    vector<vector<int> > newLocations{ locations[0] };

    vector<int>* previous = &newLocations[0];

    for (int i = 1; i < locations.size(); i++) {

        vector<int>* current = &locations[i];

        // Condition to check if the
        // substring overlaps
        if (current->at(0) <= previous->at(1)) {
            previous->at(1) = current->at(1);
        }
        else {
            newLocations.push_back(*current);
            previous
                = &newLocations[newLocations.size() - 1];
        }
    }
    return newLocations;
}

// Function creates a new string with
// underscores added at correct positions
string underscorify(string str,
                    vector<vector<int> > locations)
{
    int locationsIdx = 0;
    int stringIdx = 0;
    bool inBetweenUnderscores = false;
    vector<string> finalChars{};
    int i = 0;

    // Traverse the string and check
    // in locations[] to append _
    while (stringIdx < str.length()
           && locationsIdx < locations.size()) {

        if (stringIdx
            == locations[locationsIdx][i]) {

            // Insert underscore
            finalChars.push_back("_");
            inBetweenUnderscores
                = !inBetweenUnderscores;

            // Increment location index
            if (!inBetweenUnderscores) {
                locationsIdx++;
            }
            i = i == 1 ? 0 : 1;
        }

        // Create string s
        string s(1, str[stringIdx]);

        // Push the created string
        finalChars.push_back(s);
        stringIdx++;
    }

    if (locationsIdx < locations.size()) {
        finalChars.push_back("_");
    }
    else if (stringIdx < str.length()) {
        finalChars.push_back(str.substr(stringIdx));
    }

    // Return the resultant string
    return accumulate(finalChars.begin(),
                      finalChars.end(), string());
}

// Driver Code
int main()
{
    // Given string S1 and S2
    string S1 = "examwill be a examexam";
    string S2 = "exam";

    // Function Call
    cout << underscorifySubstring(S1, S2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG
{

    // Function that creates the string by
    // wrapping the underscore
    static String underscorifySubstring(String str,
                                        String subStr)
    {

        // Function Call to intervals of
        // starting and ending index
        List<List<Integer> > locations
            = collapse(getLocations(str, subStr));

        // Function Call
        return underscorify(str, locations);
    }

    // Function finds all starting and ending
    // index of the substring in given string
    static List<List<Integer> > getLocations(String str,
                                             String subStr)
    {
        @SuppressWarnings("unchecked")
        List<List<Integer> > locations = new ArrayList();
        int startIdx = 0;

        int L = subStr.length();

        // Traverse string str
        while (startIdx < str.length())
        {

            // Find substr
            int nextIdx = str.indexOf(subStr, startIdx);

            // If location found, then insert
            // pair int location[]
            if (nextIdx != -1)
            {

                locations.add(Arrays.asList(new Integer[] {
                    nextIdx, nextIdx + L }));

                // Update the start index
                startIdx = nextIdx + 1;
            }
            else
            {
                break;
            }
        }
        return locations;
    }

    // Function to merge the locations
    // of substrings that overlap each
    // other or sit next to each other
    static List<List<Integer> >
    collapse(List<List<Integer> > locations)
    {
        if (locations.size() == 0)
        {
            return locations;
        }

        // 2D vector to store the merged
        // location of substrings
        @SuppressWarnings("unchecked")
        List<List<Integer> > newLocations = new ArrayList();
        newLocations.add(locations.get(0));

        List<Integer> previous = locations.get(0);

        for (int i = 1; i < locations.size(); i++)
        {

            List<Integer> current = locations.get(i);

            // Condition to check if the
            // substring overlaps
            if (current.get(0) <= previous.get(1))
            {
                previous.set(1, current.get(1));
            }
            else
            {
                newLocations.add(current);
                previous = newLocations.get(
                    newLocations.size() - 1);
            }
        }
        return newLocations;
    }

    // Function creates a new string with
    // underscores added at correct positions
    static String
    underscorify(String str, List<List<Integer> > locations)
    {
        int locationsIdx = 0;
        int stringIdx = 0;
        boolean inBetweenUnderscores = false;
        StringBuilder finalChars = new StringBuilder();
        int i = 0;

        // Traverse the string and check
        // in locations[] to append _
        while (stringIdx < str.length()
               && locationsIdx < locations.size()) {

            if (stringIdx
                == locations.get(locationsIdx).get(i)) {

                // Insert underscore
                finalChars.append("_");
                inBetweenUnderscores
                    = !inBetweenUnderscores;

                // Increment location index
                if (!inBetweenUnderscores)
                {
                    locationsIdx++;
                }
                i = i == 1 ? 0 : 1;
            }

            // Push the string
            finalChars.append(str.charAt(stringIdx));
            stringIdx++;
        }

        if (locationsIdx < locations.size()) {
            finalChars.append("_");
        }
        else if (stringIdx < str.length()) {
            finalChars.append(str.substring(stringIdx));
        }

        // Return the resultant string
        return finalChars.toString();
    }

    public static void main(String[] args)
    {
        // Given string S1 and S2
        String S1 = "examwill be a examexam";
        String S2 = "exam";

        // Function Call
        System.out.print(underscorifySubstring(S1, S2));
    }
}

// This code is contributed by jithin
```

**Output:** 

```
_exam_will be a _examexam_
```

***时间复杂度:** O(N * M)，其中 N 和 M 分别是字符串 S1 和 S2 的长度。*
***辅助空间:** O(N)，其中 N 为弦 S1 的长度*