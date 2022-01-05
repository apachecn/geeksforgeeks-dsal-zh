# 根据字符的出现频率对字符串进行排序

> 原文:[https://www . geesforgeks . org/sort-a-string-按字符频率排序/](https://www.geeksforgeeks.org/sort-a-string-according-to-the-frequency-of-characters/)

给定一个字符串 **str** ，任务是按照每个字符的频率，按照升序对字符串进行排序。如果两个元素具有相同的频率，那么它们将按照字典顺序进行排序。
**例:**

> **输入:** str = "geeksforgeeks"
> **输出:**for ggk seee
> **解释:**
> 字符出现频率:g2 e4 k2 s2 f1 o1 r1
> 按照出现频率对字符进行排序:f1 o1 r1 g2 k2 s2 e4
> f、o、r 出现一次，因此它们按照字典顺序排列，g、k 和 s 也是如此
> 因此最终输出为**for ggk seee【T13
> **输入:** str = "abc"
> **输出:** abc**

**逼近**思路是将每个字符及其频率存储在一个**向量对**中，然后[根据存储的频率对向量对](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)进行排序。最后，按顺序打印矢量。
**以下是上述方法的实施:**

## C++

```
// C++ implementation to Sort strings
// according to the frequency of
// characters in ascending order

#include <bits/stdc++.h>
using namespace std;

// Returns count of character in the string
int countFrequency(string str, char ch)
{
    int count = 0;

    for (int i = 0; i < str.length(); i++)

        // Check for vowel
        if (str[i] == ch)
            ++count;

    return count;
}

// Function to sort the string
// according to the frequency
void sortArr(string str)
{
    int n = str.length();

    // Vector to store the frequency of
    // characters with respective character
    vector<pair<int, char> > vp;

    // Inserting frequency
    // with respective character
    // in the vector pair
    for (int i = 0; i < n; i++) {

        vp.push_back(
            make_pair(
                countFrequency(str, str[i]),
                str[i]));
    }

    // Sort the vector, this will sort the pair
    // according to the number of characters
    sort(vp.begin(), vp.end());

    // Print the sorted vector content
    for (int i = 0; i < vp.size(); i++)
        cout << vp[i].second;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";

    sortArr(str);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation to Sort strings
# according to the frequency of
# characters in ascending order

# Returns count of character in the string
def countFrequency(string ,  ch) :

    count = 0;

    for i in range(len(string)) :

        # Check for vowel
        if (string[i] == ch) :
            count += 1;

    return count;

# Function to sort the string
# according to the frequency
def sortArr(string) :
    n = len(string);

    # Vector to store the frequency of
    # characters with respective character
    vp = [];

    # Inserting frequency
    # with respective character
    # in the vector pair
    for i in range(n) :

        vp.append((countFrequency(string, string[i]), string[i]));

    # Sort the vector, this will sort the pair
    # according to the number of characters
    vp.sort();

    # Print the sorted vector content
    for i in range(len(vp)) :
        print(vp[i][1],end="");

# Driver code
if __name__ == "__main__" :

    string = "geeksforgeeks";

    sortArr(string);

    # This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Returns count of character in the string
function countFrequency(str, ch)
{
    var count = 0;

    for (var i = 0; i < str.length; i++)

        // Check for vowel
        if (str[i] == ch)
            ++count;

    return count;
}

// Function to sort the string
// according to the frequency
function sortArr(str)
{
    var n = str.length;

    // Vector to store the frequency of
    // characters with respective character
    vp = new Array(n);

    // Inserting frequency
    // with respective character
    // in the vector pair
    for (var i = 0; i < n; i++) {

        vp[i] = [countFrequency(str, str[i]), str[i]];
    }

    // Sort the vector, this will sort the pair
    // according to the number of characters
    vp.sort();

    // Print the sorted vector content
    for (var i = 0; i < n; i++)
        document.write(vp[i][1]);
}

// Driver Code

// Array of points
let str = "geeksforgeeks";
sortArr(str);

</script>
```

**Output:** 

```
forggkksseeee
```

***时间复杂度:** O(n <sup>2</sup> )*

***辅助空间:** O(n)*