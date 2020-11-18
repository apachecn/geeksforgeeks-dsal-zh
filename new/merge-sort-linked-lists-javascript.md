# 合并 JavaScript

> 原文：[https://www.geeksforgeeks.org/merge-sort-linked-lists-javascript/](https://www.geeksforgeeks.org/merge-sort-linked-lists-javascript/)

中链表的排序

先决条件：[合并链接列表的排序](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)

合并排序通常是对链表进行排序的首选。 链表的随机访问性能较慢，使得其他一些算法（例如 quicksort）的性能较差，而其他算法（例如堆排序）则完全不可能。

![sorting image](img/cc3d3ac699ac03f5792746b3e3e54865.png)

在本文中，使用 JavaScript 实现了链接列表的合并排序。

例子：

> 输入：5-> 4-> 3-> 2-> 1
> 输出：1-> 2-> 3-> 4-> 5
> 
> 输入：10-> 20-> 3-> 2-> 1
> 输出：1-> 2-> 3-> 10-> 20

```

<script> 

// Create Node of LinkedList 
function Node(data) { 
        this.node = data; 
        this.next = null; 
} 

// To initialize a linkedlist 
function LinkedList(list) { 
    this.head = list || null
} 

// Function to insert The new Node into the linkedList 
LinkedList.prototype.insert = function(data) { 

          // Check if the linked list is empty 
          // so insert first node and lead head 
          // points to generic node 
          if (this.head === null) 
              this.head = new Node(data); 

          else { 

              // If linked list is not empty, insert the node 
              // at the end of the linked list 
              let list = this.head; 
              while (list.next) { 
                  list = list.next; 
              } 

              // Now here list pointer points to last 
              // node let’s insert out new node in it 
              list.next = new Node(data) 
          } 
} 

// Function to print linkedList 
LinkedList.prototype.iterate = function() { 

          // First we will check whether out 
          // linked list is empty or node 
          if (this.head === null) 
              return null; 

          // If linked list is not empty we will 
          // iterate from each Node and prints 
          // it’s value store in “data” property 

          let list = this.head; 

          // we will iterate until our list variable 
          // contains the “Next” value of the last Node 
          // i.e-> null 
          while (list) { 
              document.write(list.node)  
              if (list.next) 
                  document.write(' -> ') 
              list = list.next 
          } 
} 

// Function to mergesort a linked list 
LinkedList.prototype.mergeSort = function(list) { 

          if (list.next === null) 
              return list; 

          let count = 0; 
          let countList = list 
          let leftPart = list; 
          let leftPointer = list; 
          let rightPart = null; 
          let rightPointer = null; 

          // Counting the nodes in the received linkedlist 
          while (countList.next !== null) { 
              count++; 
              countList = countList.next; 
          } 

          // counting the mid of the linked list 
          let mid = Math.floor(count / 2) 
          let count2 = 0; 

          // separating the left and right part with 
          // respect to mid node in tke linked list 
          while (count2 < mid) { 
              count2++; 
              leftPointer = leftPointer.next; 
          } 

          rightPart = new LinkedList(leftPointer.next); 
          leftPointer.next = null; 

          // Here are two linked list which 
          // contains the left most nodes and right 
          // most nodes of the mid node 
          return this._mergeSort(this.mergeSort(leftPart), 
                                 this.mergeSort(rightPart.head)) 
} 

// Merging both lists in sorted manner 
LinkedList.prototype._mergeSort = function(left, right) { 

          // Create a new empty linked list 
          let result = new LinkedList() 

          let resultPointer = result.head; 
          let pointerLeft = left; 
          let pointerRight = right; 

          // If true then add left most node value in result, 
          // increment left pointer else do the same in 
          // right linked list. 
          // This loop will be executed until pointer's of 
         // a left node or right node reached null 
          while (pointerLeft && pointerRight) { 
              let tempNode = null; 

             // Check if the right node's value is greater than 
             // left node's value 
              if (pointerLeft.node > pointerRight.node) { 
                  tempNode = pointerRight.node 
                  pointerRight = pointerRight.next; 
              } 
              else { 
                  tempNode = pointerLeft.node 
                  pointerLeft = pointerLeft.next; 
              } 

              if (result.head == null) { 
                  result.head = new Node(tempNode) 
                  resultPointer = result.head 
              } 
              else { 
                  resultPointer.next = new Node(tempNode) 
                  resultPointer = resultPointer.next 
              } 
          } 

          // Add the remaining elements in the last of resultant 
          // linked list 
          resultPointer.next = pointerLeft; 
          while (resultPointer.next) 
              resultPointer = resultPointer.next 

              resultPointer.next = pointerRight 

          // Result is  the new sorted linked list 
           return result.head; 
} 

// Initialize the object 
let l = new LinkedList(); 
l.insert(10) 
l.insert(20) 
l.insert(3) 
l.insert(2) 
l.insert(1) 
// Print the linked list 
l.iterate() 

// Sort the linked list 
l.head = LinkedList.prototype.mergeSort(l.head) 

document.write('<br> After sorting : '); 

// Print the sorted linked list 
l.iterate() 
</script> 

```

**输出**

```
10 -> 20 -> 3 -> 2 -> 1
After sorting : 1 -> 2 -> 3 -> 10 -> 20 

```

[![full-stack-img](img/1e356a15f348bce3fafac1fccfa8fbd6.png)](https://practice.geeksforgeeks.org/courses/full-stack-node?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_fullstack)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。