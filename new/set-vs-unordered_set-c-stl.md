# C++ STL 中的

# set vs unordered_set

先决条件：在 C++中设置 [](https://www.geeksforgeeks.org/set-in-cpp-stl/) ，在 C++中设置 [unordered_set](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)

**差异**：

```
                |     set             | unordered_set
---------------------------------------------------------
Ordering        | increasing  order   | no ordering
                | (by default)        |

Implementation  | Self balancing BST  | Hash Table
                | like Red-Black Tree |  

search time     | log(n)              | O(1) -> Average 
                |                     | O(n) -> Worst Case

Insertion time  | log(n) + Rebalance  | Same as search

Deletion time   | log(n) + Rebalance  | Same as search

```

**设置为**时使用

*   我们需要有序的数据。

*   我们将不得不打印/访问数据（按排序顺序）。

*   我们需要元素的前任/后继。

*   由于 set 是有序的，因此我们可以在 set 元素上使用 [binary_search（），lower_bound（）和 upper_bound（）](https://www.geeksforgeeks.org/binary-search-functions-in-c-stl-binary_search-lower_bound-and-upper_bound/)之类的函数。 这些函数不能在 unordered_set（）上使用。

*   有关更多情况，请参见 BST 相对于哈希表 e 的[优势。](https://www.geeksforgeeks.org/advantages-of-bst-over-hash-table/)

**当**时使用 unordered_set

*   我们需要保留一组不同的元素，并且不需要排序。

*   我们需要单元素访问，即无遍历。

例子：

```
set:
Input  :  1, 8, 2, 5, 3, 9
Output :  1, 2, 3, 5, 8, 9

Unordered_set:
Input  : 1, 8, 2, 5, 3, 9
Output : 9 3 1 8 2 5 

```

如果要查看 C++ STL 中 set 和 unordered_set 的实现细节，请参见 [Set Vs Map](https://www.geeksforgeeks.org/set-vs-map-c-stl/) 。 Set 允许按排序顺序遍历元素，而 Unordered_set 不允许按排序顺序遍历元素。

```
// Program to print elements of set
#include <bits/stdc++.h>
using namespace std;
int main()
{
set< int > s;
s.insert(5);
s.insert(1);
s.insert(6);
s.insert(3);
s.insert(7);
s.insert(2);
cout << "Elements of set in sorted order: \n" ;
for ( auto it : s)
cout << it << " " ;
return 0;
[ }
```

**Output:**

```
Elements of set in sorted order: 
1 2 3 5 6 7

```

```
// Program to print elements of set
#include <bits/stdc++.h>
using namespace std;
int main()
{
unordered_set< int > s;
s.insert(5);
s.insert(1);
s.insert(6);
s.insert(3);
s.insert(7);
s.insert(2);
cout << "Elements of unordered_set: \n" ;
for ( auto it : s)
cout << it << " " ;
return 0;
[ }
```

**Output:**

```
Elements of unordered_set: 
2 7 5 1 6 3

```

***集合中的前任/后继者*** ：

可以修改集合以查找前任或后继者，而 Unordered_set 不允许查找前任/后继者。

```
// Program to print inorder predecessor and inorder successor
#include <bits/stdc++.h>
using namespace std;
set< int > s;
void inorderPredecessor( int key)
{
if (s.find(key) == s.end()) {
cout << "Key doesn't exist\n" ;
return ;
}
set< int >::iterator it;
it = s.find(key); // get iterator of key
[
// If iterator is at first position
// Then, it doesn't have predecessor
if (it == s.begin()) {
cout << "No predecessor\n" ;
return ;
}
--it; // get previous element
cout << "predecessor of " << key << " is=" ;
cout << *(it) << "\n" ;
}
void inorderSuccessor( int key)
{
if (s.find(key) == s.end()) {
cout << "Key doesn't exist\n" ;
return ;
}
set< int >::iterator it;
it = s.find(key); // get iterator of key
++it; // get next element
// Iterator points to NULL (Element does
// not exist)
if (it == s.end())
{
cout << "No successor\n" ;
return ;
[HTG2 49]      }
cout << "successor of " << key << " is=" ;
cout << *(it) << "\n" ;
}
int main()
{
s.insert(1); ]
s.insert(5);
s.insert(2);
s.insert(9);
s.insert(8);
inorderPredecessor(5);
inorderPredecessor(1);
inorderPredecessor(8);
inorderSuccessor(5);
inorderSuccessor(2);
inorderSuccessor(9);
return ] 0;
}
```

**Output:**

```
predecessor of 5 is=2
No predecessor
predecessor of 8 is=5
successor of 5 is=8
successor of 2 is=5
No successor

```



* * *

* * *



