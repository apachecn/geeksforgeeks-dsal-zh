# 允许进行重排的最小等回文切割

给定一个长度为 n 的字符串。 重新排列字符串后，找到最小可能的切口数（如果需要），以使每个切口都是回文，并且每个切口的长度相等。 也就是说，如果在分割之前允许重新排列字符串，则找到可以通过分割给定字符串而获得的等长回文数的最小数目。

例子：

```
Input : string = "aabaac"
Output : 2
Explanation : Rearrange the string as "abaaca"
              and cut into "aba" and "aca"

Input : string = "aabbccdd"
Output : 1
Explanation : Rearrange the string as "abcddcba"
              This is a palindrome and cannot be 
              cut further.

```

如果我们仔细观察，我们的问题将减少到计算具有偶数和偶数的字符。 以下是可能的情况，

1.  如果字符串中存在的字符只有偶数，则答案将为 1，因为我们可以重新排列整个字符串以形成回文。
2.  如果只有一个具有奇数的字符，那么答案也将为 1，因为我们可以
    重新排列整个字符串以形成回文。
3.  如果有一个以上带有奇数的字符，那么我们将创建两个单独的字符列表–一个用于奇数字符，一个用于偶数字符。 现在，如果我们注意到如果一个字符的计数为奇数，那么如果从中减去 1，该计数将变为偶数。 因此，我们将在奇数列表中仅插入一次具有奇数的元素。 我们将以偶数（evenCount / 2）次插入元素，即将元素计数的一半插入偶数列表。 现在，我们的问题是将偶数元素均匀分布在奇数元素之间，以形成等长的回文。 假设偶数字符列表为*偶数*，奇数字符列表为*奇数*。 如果 even.size（）可被 odd.size（）整除，我们的答案将是 odd.size（），否则我们会将元素从偶数列表传输到奇数列表，直到 even.size（）被 odd.size（）整除。

下面是上述想法的实现：

```
// CPP program to find minimum number of palindromic
// cuts of equal length
#include<bits/stdc++.h>
using namespace std;
// function to find minimum number of
// palindromic cuts of equal length
int minPalindromeCuts(string str)
{
// map to store count of characters
unordered_map< char , int > m;
// store count of characters in a map
for ( int i=0;i<str.length();i++)
{
if (m.find(str[i])==m.end())
m.insert(make_pair(str[i],1));
else
m[str[i]]++;
}
// list to store even count characters
vector< char > even;
// list to store odd count characters
[HTG2 22]      vector< char > odd;
for ( auto itr = m.begin(); itr!=m.end(); itr++)
{
// add odd count characters only once and
// decrement count by 1
if (itr->second%2!=0)
{
odd.push_back(itr->first);
itr->second--;
}
[      }
for ( auto itr = m.begin(); itr!=m.end(); itr++)
{
if (itr->second%2==0)
{
// add even count characters half of their
// count to the even list so that we can
// simply repeat the even list on both
// sides of an odd char to generate a
// palindrome
for ( [ int i=0;i<(itr->second)/2;i++)             [H TG267]
even.push_back(itr->first);
}
}
// if there is no odd count characters or
// only 1 odd count character, return 1
if (odd.size() <= 1)
return 1;
else
{
// Move some characters from even list over
// to odd list to make palindrome work
while (odd.size() > 0 && even.size() > 0 &&
even.size() % odd.size() != 0)
{
odd.push_back(even.back());
odd.push_back(even.back());
even.pop_back();
}
return odd.size();
}
}
// driver code
int main()
{
string str = "aabaac" ] ;
cout << minPalindromeCuts(str);
return 0;
}
```

输出：

```
2

```



* * *

* * *



