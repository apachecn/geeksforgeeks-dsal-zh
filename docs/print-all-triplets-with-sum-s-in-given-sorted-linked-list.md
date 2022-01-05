# 打印给定排序链表中所有总和为 S 的三元组

> 原文:[https://www . geeksforgeeks . org/print-all-triples-with-sum-s-in-given-sorted-link-list/](https://www.geeksforgeeks.org/print-all-triplets-with-sum-s-in-given-sorted-linked-list/)

给定排序后的 [**单链表**](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/) 作为 **N** 个不同节点的(没有两个节点有相同的数据)和一个整数 **S** 。任务是在列表中找到所有**不同的三元组**，它们加起来就是给定的整数 s。

**示例:**

> **输入:**列表= 1->2->4->5->6->8->9，S = 15
> **输出:** [(1，5，9)，(1，6，8)，(2，4，9)，(2，5，8)，(4，5，6)]
> **解释:**这是仅有的总和等于 S 即 e 15 的不同三元组。请注意，(2，4，9)和(9，4，2)两个三元组的总和都是 15，但它们并不明显，因为三元组的所有元素都是相同的。
> 
> **输入:**列表= 1->2->4->5->6->8->9，S = 17
> T3】输出: [(2，6，9)，(4，5，8)]

**天真方法:**使用三个嵌套循环。生成所有三元组，找到总和等于 S.
**的不同三元组时间复杂度:** O(N <sup>3</sup> )
**辅助空间:** O(N <sup>3</sup> )

**高效方法:**利用 [**哈希**](http://www.geeksforgeeks.org/hashing-data-structure/) 的概念高效解决问题。遵循下面提到的步骤

1.  创建一个**散列数组**来存储扫描的节点数据。
2.  将头节点值插入哈希数组。
3.  现在开始使用**嵌套循环**遍历链表，在每次迭代中:
    *   从给定的整数“S”中减去两个节点的数据，得到组成三元组的值。
    *   现在在散列数组中找到那个值。
    *   如果该值存在于散列数组中(即找到三元组)，则将三元组存储在列表中作为可能的答案。
4.  退回清单。

下面是上述方法的实现:

## C++

```
// C++ code to find
// all distinct triplets having sum S
#include <bits/stdc++.h>
using namespace std;

// Structure of node of singly linked list
struct Node {
    int data;
    Node* next;
    Node(int x)
    {
        data = x;
        next = NULL;
    }
};

// Inserting new node
// at the  beginning of the linked list
void push(struct Node** head_ref,
          int new_data)
{
    // Create a new node with the given data.
    struct Node* new_node
      = new Node(new_data);

    // Make the new node point to the head.
    new_node->next = (*head_ref);

    // Make the new node as the head node.
    (*head_ref) = new_node;
}

// Function to print triplets
// in a sorted singly linked list
// whose sum is equal to given value 'S'
vector<vector<int>>
  printTriplets(struct Node* head, int S)
{
    // Declare unordered map
    // to store the scanned value
    unordered_map<int, bool> mp;

    // Vector to store the triplets
    vector<vector<int>> v;

    // Declare two pointers 'p' and 'q'
    // for traversing singly linked list
    struct Node* p;
    struct Node* q;

    // Insert 1st node data into map
    // and start traversing from next node
    mp[head->data] = true;

    // Outer loop terminates
    // when last node reached
    for (p = head->next; p->next != NULL;
         p = p->next) {

        // Inner loop terminates
        // when second pointer become NULL
        for (q = p->next; q != NULL;
             q = q->next) {

            // Temporary vector
            // to store the current triplet
            vector<int> temp;
            int second = p->data;
            int third = q->data;

            // find the number required
            // to make triplet by subtracting
            // node1 and node2 data from S
            // and store it.
            int first = S - second - third;

            // Search if that value
            // is present in the map or not
            if (mp.find(first)
                != mp.end()) {

                // If 'first' is present
                // in map, make a triplet of
                // first,second & third
                temp.push_back(mp.find(first)->first);
                temp.push_back(second);
                temp.push_back(third);

                // Push current triplet
                // stored in 'temp' to
                // vector 'v'
                v.push_back(temp);
            }
        }

        // Insert current node data into map
        mp[p->data] = true;
    }

    // Return a vector of triplets.
    return v;
}

// Driver code
int main()
{
    int S = 15;

    // Create an empty singly linked list
    struct Node* head = NULL;
    vector<vector<int> > ans;

    // Insert values in sorted order
    push(&head, 9);
    push(&head, 8);
    push(&head, 6);
    push(&head, 5);
    push(&head, 4);
    push(&head, 2);
    push(&head, 1);

    // Call printTriplets function
    // to find all triplets in
    // the linked list
    ans = printTriplets(head, S);

    // Sort and  display
    // all possible triplets
    sort(ans.begin(), ans.end());
    for (int i = 0; i < ans.size(); i++) {
        for (int j = 0;
             j < ans[i].size(); j++) {
            cout << ans[i][j] << " ";
        }
        cout << "\n";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find
// all distinct triplets having sum S
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.HashMap;

class GFG
{

    // Structure of node of singly linked list
    static class Node {
        int data;
        Node next;

        public Node(int x) {
            data = x;
            next = null;
        }
    };

    // Function to print triplets
    // in a sorted singly linked list
    // whose sum is equal to given value 'S'
    public static ArrayList<ArrayList<Integer>> printTriplets(Node head, int S) {
        // Declare unordered map
        // to store the scanned value
        HashMap<Integer, Boolean> mp = new HashMap<Integer, Boolean>();

        // Vector to store the triplets
        ArrayList<ArrayList<Integer>> v = new ArrayList<ArrayList<Integer>>();

        // Declare two pointers 'p' and 'q'
        // for traversing singly linked list
        Node p;
        Node q;

        // Insert 1st node data into map
        // and start traversing from next node
        mp.put(head.data, true);

        // Outer loop terminates
        // when last node reached
        for (p = head.next; p.next != null; p = p.next) {

            // Inner loop terminates
            // when second pointer become null
            for (q = p.next; q != null; q = q.next) {

                // Temporary vector
                // to store the current triplet
                ArrayList<Integer> temp = new ArrayList<Integer>();
                int second = p.data;
                int third = q.data;

                // find the number required
                // to make triplet by subtracting
                // node1 and node2 data from S
                // and store it.
                int first = S - second - third;

                // Search if that value
                // is present in the map or not
                if (mp.containsKey(first)) {

                    // If 'first' is present
                    // in map, make a triplet of
                    // first,second & third
                    temp.add(first);
                    temp.add(second);
                    temp.add(third);

                    // Push current triplet
                    // stored in 'temp' to
                    // vector 'v'
                    v.add(temp);
                }
            }

            // Insert current node data into map
            mp.put(p.data, true);
        }

        // Return a vector of triplets.
        return v;
    }

    // Driver code
    public static void main(String args[]) {
        int S = 15;

        // Create an empty singly linked list
        Node head = null;
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();

        // Insert values in sorted order
        head = new Node(9);
        head.next = new Node(8);
        head.next.next = new Node(6);
        head.next.next.next = new Node(5);
        head.next.next.next.next = new Node(4);
        head.next.next.next.next.next = new Node(2);
        head.next.next.next.next.next.next = new Node(1);

        // Call printTriplets function
        // to find all triplets in
        // the linked list
        ans = printTriplets(head, S);

        // Sort and display
        // all possible triplets
        for (ArrayList<Integer> x : ans) {
            Collections.sort(x);
        }

        Collections.sort(ans, new Comparator<ArrayList<Integer>>() {
            @Override
            public int compare(ArrayList<Integer> o1, ArrayList<Integer> o2) {
                return o2.get(0) - (o1.get(0));
            }
        });
        Collections.reverse(ans);

        for (int i = 0; i < ans.size(); i++) {
            for (int j = 0; j < ans.get(i).size(); j++) {
                System.out.print(ans.get(i).get(j) + " ");
            }
            System.out.println("");
        }
    }
}

// This code is contributed by gfgking.
```

## java 描述语言

```
<script>

      // JavaScript Program to implement
      // the above approach

      // Structure of node of singly linked list
      class Node {

          constructor(x) {
              this.data = x;
              this.next = null;
          }
      };

      // Function to print triplets
      // in a sorted singly linked list
      // whose sum is equal to given value 'S'
      function printTriplets(head, S)
      {

          // Declare unordered map
          // to store the scanned value
          let mp = new Map();

          // Vector to store the triplets
          let v = [];

          // Declare two pointers 'p' and 'q'
          // for traversing singly linked list
          let p;
          let q;

          // Insert 1st node data into map
          // and start traversing from next node
          mp.set(head.data, true);

          // Outer loop terminates
          // when last node reached
          for (p = head.next; p.next != null;
              p = p.next) {

              // Inner loop terminates
              // when second pointer become null
              for (q = p.next; q != null;
                  q = q.next) {

                  // Temporary vector
                  // to store the current triplet
                  let temp = [];
                  let second = p.data;
                  let third = q.data;

                  // find the number required
                  // to make triplet by subtracting
                  // node1 and node2 data from S
                  // and store it.
                  let first = S - second - third;

                  // Search if that value
                  // is present in the map or not
                  if (mp.has(first)) {

                      // If 'first' is present
                      // in map, make a triplet of
                      // first,second & third
                      temp.push(first);
                      temp.push(second);
                      temp.push(third);

                      // Push current triplet
                      // stored in 'temp' to
                      // vector 'v'
                      v.push(temp);
                  }
              }

              // Insert current node data into map
              mp.set(p.data, true);
          }

          // Return a vector of triplets.
          return v;
      }

      // Driver code
      let S = 15;

      // Create an empty singly linked list
      let head = null;
      let ans = [];

      // Insert values in sorted order
      head = new Node(9)
      head.next = new Node(8)
      head.next.next = new Node(6)
      head.next.next.next = new Node(5)
      head.next.next.next.next = new Node(4)
      head.next.next.next.next.next = new Node(2)
      head.next.next.next.next.next.next = new Node(1)

      // Call printTriplets function
      // to find all triplets in
      // the linked list
      ans = printTriplets(head, S);

      // Sort and  display
      // all possible triplets
      for (let i = 0; i < ans.length; i++) {

          ans[i].sort(function (a, b) { return a - b })
      }
      ans.sort()
      for (let i = 0; i < ans.length; i++) {
          for (let j = 0;
              j < ans[i].length; j++) {
              document.write(ans[i][j] + " ");
          }
          document.write('<br>')
      }

  // This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
1 5 9 
1 6 8 
2 4 9 
2 5 8 
4 5 6 
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)