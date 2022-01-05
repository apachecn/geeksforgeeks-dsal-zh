# 求解各查询后以最小绝对差配对

> 原文:[https://www . geeksforgeeks . org/求解每个查询后的最小绝对差配对/](https://www.geeksforgeeks.org/pair-with-minimum-absolute-difference-after-solving-each-query/)

给定 Q 个查询和一个空列表。
查询可以有两种类型:

1.  添加到列表(x):将 x 添加到您的列表中。
2.  移除列表(x):从列表中移除 x。

任务是，每次查询后，你都要打印 abs 的最小值(list[i]-list[j])其中，0 <=i<=n, 0<=j<=n and i ≠ j and n is the total number of elements present in the list. 
**例** :

> **输入** : Q = 4
> 添加到列表(1)，在我们的集合中插入 1
> 添加到列表(5)，在我们的集合中插入 5
> 添加到列表(3)，在我们的集合中插入 3
> 从列表(3)中删除，在我们的集合中删除 3
> **输出** :
> 0，因为我们的集合中只有一个元素{1}。
> 4，因为我们有{1，5}所有可能对之间的最小差异是 4 (5-1)
> 2，因为我们有{1，3，5}所有可能对之间的最小差异是 2 (3-1)
> 4，因为我们有{1，5}所有可能对之间的最小差异是 4 (5-1)

**方法 1:** 思路是用 C++中的 set 来存储所有的元素，这样就可以在 O(log(n))中进行插入或删除，同时保持元素的排序顺序。现在，为了找到最小差异，我们必须迭代整个集合，并且当元素按排序顺序排列时，只找到相邻元素之间的差异，即最小差异总是由相邻元素贡献的。这可以在 O(n)时间复杂度内完成。因此，这种方法的总时间复杂度为(q*log(n)+q*n)。
**方法二:**
我们可以使用 multiset 来存储和维护所有元素，map 以排序的顺序存储相邻元素之间的差异，其中，map 的 key 表示相邻元素之间的差异，对应 map 的值表示这种差异的出现频率。
下面是完整的**算法:**
首先，在多集中插入两个哨点值。假设(-10^9+7 和 10^9+7)用这个哨兵值的差初始化地图，即 2*10^7+7，并将其频率设置为 1。
现在我们有两种类型的查询:

1.  **插入查询:**对于插入查询，首先插入*值*插图。插入元素后，我们还必须更新地图中相邻元素的差异。为此，在集合中找到新插入元素的*左*和*右*值。早先当这个新值没有被插入到集合中时，abs(右-左)对地图中的不同术语起作用。要在插入新元素后更新地图，首先，删除之前的差异 abs(右-左)，因为新值会插入左右元素之间，并向地图添加两个差异。即腹肌(右 x)和腹肌(左 x)。
2.  **删除查询:**从集合中删除值的情况。首先找到需要删除的元素的*左*和*右*元素，比如 x，然后按照上面的算法，降低 abs(右-x)和 abs(左-x)的频率，增加 abs(右-左)的频率。

因此，每个查询都可以用 log(n)时间复杂度来求解。因此，整体复杂度将为 O(q*log(n))。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of above approach
#include <bits/stdc++.h>
#define ll long long int
const ll MOD = 1e9 + 7;
using namespace std;

// Function to add an element into the list
void addToList(int x, multiset<ll>& s, map<ll, ll>& mp)
{
    // firstly insert value in set
    s.insert(x);

    // find left and right value of inserted value.
    ll left, right;

    // now here is logic explained below
    left = *(--s.find(x));
    right = *(++s.find(x));
    mp[abs(left - x)]++;
    mp[abs(right - x)]++;
    mp[abs(left - right)]--;
    if (mp[abs(left - right)] == 0)
        mp.erase(abs(left - right));
}

// Function to remove an element from the list
void removeFromList(int x, multiset<ll>& s, map<ll, ll>& mp)
{
    ll left, right;

    // Find left element of number that we want to delete.
    left = *(--s.find(x));

    // Find right element of number that we want to delete.
    right = *(++s.find(x));

    // remove x from set
    s.erase(s.find(x));

    // Again this will explain below in article.
    mp[abs(left - x)]--;
    if (mp[abs(left - x)] == 0)
        mp.erase(abs(left - x));
    mp[abs(right - x)]--;
    if (mp[abs(right - x)] == 0)
        mp.erase(abs(right - x));

    mp[abs(left - right)]++;
}

// Driver code
int main()
{

    int q = 4;

    // define set to store all values.
    multiset<ll> s;

    // define map to store difference in sorted
    map<ll, ll> mp;

    // initialize set with sentinel values
    s.insert(-MOD);
    s.insert(MOD);

    // maintain freq of difference in map so, here initially
    // difference b/w sentinel value and its freq is one.
    mp[2 * MOD] = 1;

    // 1st query 1 1 i.e, include 1 in our set
    addToList(1, s, mp);

    // As now we have only one element {-10^9+7, 1, 10^9+7}
    // (except two are sentinel values)
    // so minimum among all pair is zero
    cout << 0 << endl;

    // 2nd query 1 5 i.e, include 5 in our set.
    addToList(5, s, mp);

    // find smallest difference possible
    // as it should be in beginning of map
    cout << mp.begin()->first << endl;

    // 3rd query 1 3 i.e, include 3 in our set.
    addToList(3, s, mp);

    // find smallest difference possible
    // as it should be in beginning of map
    cout << mp.begin()->first << endl;

    // 4th query 2 3 i.e, remove 3 from our list
    removeFromList(3, s, mp);

    cout << mp.begin()->first << endl;

 return 0;
}
```

**Output:** 

```
0
4
2
4
```

**各查询解释:**

1.  ***addToList(1):*** 因为现在我们只有一个元素{-10^9+7、1、10^9+7}(除了两个是哨兵值)，所以所有对中的最小值为零。
2.  ***添加到列表(5):*** 在集合中插入 1 和 5 后，集合变为{-10^9+7、1、5、10^9+7}和地图:mp[5-1]=1，其中 key 表示差异，其值表示频率。
3.  ***添加到列表(3):*** 这里我们插入 3。所以，首先，我们找到插入后集合中 3 的左右元素，即 left = 1，right = 5。由于 3 出现在 1 和 5 之间，因此我们移除了地图[5-1]–。(由于 3 出现在 1 和 5 之间，因此 **5-1** 将不再是最小值)并且我们包括这些差异 map[3-1]++和 map[5-3]++(因为 3 出现在 1 和 5 之间，所以可能的最小值有两种情况)。
4.  ***removeFromList(3):***类似于上面的查询，这里我们删除元素。所以，首先，找到 3 的左右元素，即左= 1，右= 5。由于我们将删除 1 & 5 之间的 3，因此最小差异仅受 3 和 5 的影响，

```
before deleting ==>{1, 3, 5}, 
after deleting ==> {1, 5}. 
So, map[3-1]--, map[5-3]-- and add map[5-1]++.
```

**时间复杂度:** O(qlogN)，其中‘q’为查询总数。
**辅助空间:** O(q)。