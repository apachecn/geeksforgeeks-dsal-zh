# 列表中缺少排列

> 原文:[https://www.geeksforgeeks.org/missing-permutations-list/](https://www.geeksforgeeks.org/missing-permutations-list/)

给定任何单词的排列列表。从排列列表中找出缺失的排列。
 **例:**

```
Input : Permutation_given[] = {"ABCD", "CABD", "ACDB", 
              "DACB", "BCDA", "ACBD", "ADCB", "CDAB",
              "DABC", "BCAD", "CADB", "CDBA", "CBAD", 
              "ABDC", "ADBC", "BDCA", "DCBA", "BACD",
              "BADC", "BDAC", "CBDA", "DCAB"};
Output : DBAC DBCA

```

1)我们创建所有给定字符串的集合。
2)还有一组所有排列。
3)最终返回两套之间的差异。

```
#include <bits/stdc++.h>
using namespace std;

void find_missing_strings(string Permutation_given[], size_t Size_Permutation_given)
{
    // vector "permutation" containing all
    // the permutation of input string
    vector<string> permutations;

    // Here we can take any string
    // from the given list and do
    // the necessary permutation
    string input = Permutation_given[0];
    permutations.push_back(input);

    // In the loop we will store
    // all the permutations of the string
    // in the vector "permutation".
    while (true) {

        string p = permutations.back();

        // Getting next permutation of input string
        next_permutation(p.begin(), p.end());
        if (p == permutations.front())
            break;

        permutations.push_back(p);
    }

    // vector containing all the
    // missing strings in permutation
    vector<string> missing;

    // given_permutations contains the
    // permutation of the input string
    set<string> given_permutations(Permutation_given, 
         Permutation_given + Size_Permutation_given);

    // Through the set difference we will get 
    // the missing words in vector missing
    set_difference(permutations.begin(), permutations.end(),
                                 given_permutations.begin(),
                                 given_permutations.end(), 
                                  back_inserter(missing));

    // printing all the missing string
    for (auto i = missing.begin(); i != missing.end(); ++i)
        cout << *i << endl;
}

// Driver code
int main()
{
    string Permutation_given[] = {
        "ABCD", "CABD", "ACDB", "DACB",
        "BCDA", "ACBD", "ADCB", "CDAB",
        "DABC", "BCAD", "CADB", "CDBA",
        "CBAD", "ABDC", "ADBC", "BDCA",
        "DCBA", "BACD", "BADC", "BDAC",
        "CBDA", "DCAB"
    };

    // size of permutation list
    size_t Size_Permutation_given = 
                 sizeof(Permutation_given) / 
                 sizeof(*Permutation_given);

    find_missing_strings(Permutation_given, 
                    Size_Permutation_given);

    return 0;
}
```

输出:

```
DBAC
DBCA

```