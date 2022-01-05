# 查找由映射到数字的字符构成的所有字符串

> 原文:[https://www . geesforgeks . org/find-strings-formed-characters-mapped-digits-number/](https://www.geeksforgeeks.org/find-strings-formed-characters-mapped-digits-number/)

考虑下面的列表，其中从 1 到 9 的每个数字映射到几个字符。

```
1 -> ['A', 'B', 'C']
2 -> ['D', 'E', 'F']
3 -> ['G', 'H', 'I']
4 -> ['J', 'K', 'L']
5 -> ['M', 'N', 'O']
6 -> ['P', 'Q', 'R']
7 -> ['S', 'T', 'U']
8 -> ['V', 'W', 'X']
9 -> ['Y', 'Z'] 
```

给定一个数字，用给定列表中的相应字符替换它的数字，并打印所有可能的字符串。数字中每出现一个数字都应考虑相同的字符。输入数字为正数，不包含 0。

示例:

```
Input : 121
Output : ADA BDB CDC AEA BEB CEC AFA BFB CFC

Input : 22
Output : DD EE FF 

```

其思想是，对于输入数字中的每个数字，我们考虑由前一个数字形成的字符串，并将映射到当前数字的字符附加到它们上面。如果这不是该数字的第一次出现，我们会附加与其第一次出现时相同的字符。

## C++

```
// C++ program to find all strings formed from a given
// number where each digit maps to given characters.
#include <bits/stdc++.h>
using namespace std;

// Function to find all strings formed from a given
// number where each digit maps to given characters.
vector<string> findCombinations(vector<int> input,
                                vector<char> table[])
{
    // vector of strings to store output
    vector<string> out, temp;

    // stores index of first occurrence
    // of the digits in input
    unordered_map<int, int> mp;

    // maintains index of current digit considered
    int index = 0;

    // for each digit
    for (int d: input)
    {
        // store index of first occurrence
        // of the digit in the map
        if (mp.find(d) == mp.end())
            mp[d] = index;

        // clear vector contents for future use
        temp.clear();

        // do for each character thats maps to the digit
        for (int i = 0; i < table[d - 1].size(); i++)
        {
            // for first digit, simply push all its
            // mapped characters in the output list
            if (index == 0)
            {
                string s(1, table[d - 1].at(i));
                out.push_back(s);
            }

            // from second digit onwards
            if (index > 0)
            {
                // for each string in output list
                // append current character to it.
                for(string str: out)
                {
                    // convert current character to string
                    string s(1, table[d - 1].at(i));

                    // Imp - If this is not the first occurrence
                    // of the digit, use same character as used
                    // in its first occurrence
                    if(mp[d] != index)
                        s = str[mp[d]];

                    str = str + s;

                    // store strings formed by current digit
                    temp.push_back(str);
                }

                // nothing more needed to be done if this
                // is not the first occurrence of the digit
                if(mp[d] != index)
                    break;
            }
        }

        // replace contents of output list with temp list
        if(index > 0)
            out = temp;
        index++;
    }

    return out;
}

// Driver program
int main()
{
    // vector to store the mappings
    vector<char> table[] =
    {
        { 'A', 'B', 'C' },
        { 'D', 'E', 'F' },
        { 'G', 'H', 'I' },
        { 'J', 'K', 'L' },
        { 'M', 'N', 'O' },
        { 'P', 'Q', 'R' },
        { 'S', 'T', 'U' },
        { 'V', 'W', 'X' },
        { 'Y', 'Z' }
    };

    // vector to store input number
    vector<int> input = { 1, 2, 1};

    vector<string> out = findCombinations(input, table);

    // print all possible strings
    for (string it: out)
        cout << it << " ";

    return 0;
}
```