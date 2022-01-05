# Python 中异或链表的实现

> 原文:[https://www . geesforgeks . org/python 中 xor 链表的实现/](https://www.geeksforgeeks.org/implementation-of-xor-linked-list-in-python/)

**先决条件:** [异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)

一个普通的双向链表需要两个地址字段的空间来存储上一个和下一个节点的地址。对于每个节点的地址字段，只需使用一个空间就可以创建一个内存高效的版本的双向链表。这种内存高效的双链表称为异或链表或内存高效链表，因为该链表使用按位异或运算来节省一个地址的空间。在异或链表中，不是存储实际的内存地址，而是每个节点存储上一个和下一个节点地址的异或。

Python 中的异或链表实现用处不大，因为 Python 垃圾收集器不允许保存地址被异或的节点。

#### 以下程序中实现的功能有:

*   **InsertAtStart():** 在开始处插入节点的方法。
*   **InsertAtEnd():** 方法在末尾插入一个节点。
*   **DeleteAtStart():** 删除开头节点的方法。
*   **DeleteAtEnd():** 方法删除末尾的节点。
*   **Print():** 从头到尾遍历链表的方法。
*   **ReversePrint():** 从头到尾遍历链表的方法。
*   **Length():** 返回链表大小的方法。
*   **PrintByIndex():** 返回特定索引指定的链表节点的数据值的方法。
*   **isEmpty():** 检查链表是否为空的方法。
*   **__type_cast():** 方法到返回一个指向同一个内存块的 *类型* 的新实例。

**下面是用上述方法实现 XOR 链表的完整 Python 程序:**

## Python 3

```
# import required module
import ctypes

# create node class
class Node:
    def __init__(self, value):
        self.value = value
        self.npx = 0

# create linked list class
class XorLinkedList:

    # constructor
    def __init__(self):
        self.head = None
        self.tail = None
        self.__nodes = []

    # method to insert node at beginning
    def InsertAtStart(self, value):
        node = Node(value)
        if self.head is None:  # If list is empty
            self.head = node
            self.tail = node
        else:
            self.head.npx = id(node) ^ self.head.npx
            node.npx = id(self.head)
            self.head = node
        self.__nodes.append(node)

    # method to insert node at end
    def InsertAtEnd(self, value):
        node = Node(value)
        if self.head is None:  # If list is empty
            self.head = node
            self.tail = node
        else:
            self.tail.npx = id(node) ^ self.tail.npx
            node.npx = id(self.tail)
            self.tail = node
        self.__nodes.append(node)

    # method to remove node at beginning
    def DeleteAtStart(self):
        if self.isEmpty():  # If list is empty
            return "List is empty !"
        elif self.head == self.tail:  # If list has 1 node
            self.head = self.tail = None
        elif (0 ^ self.head.npx) == id(self.tail):  # If list has 2 nodes
            self.head = self.tail
            self.head.npx = self.tail.npx = 0
        else:  # If list has more than 2 nodes
            res = self.head.value
            x = self.__type_cast(0 ^ self.head.npx)  # Address of next node
            y = (id(self.head) ^ x.npx)  # Address of next of next node
            self.head = x
            self.head.npx = 0 ^ y
            return res

    # method to remove node at end
    def DeleteAtEnd(self):
        if self.isEmpty():  # If list is empty
            return "List is empty !"
        elif self.head == self.tail:  # If list has 1 node
            self.head = self.tail = None
        elif self.__type_cast(0 ^ self.head.npx) == (self.tail):  # If list has 2 nodes
            self.tail = self.head
            self.head.npx = self.tail.npx = 0
        else:  # If list has more than 2 nodes
            prev_id = 0
            node = self.head
            next_id = 1
            while next_id:
                next_id = prev_id ^ node.npx
                if next_id:
                    prev_id = id(node)
                    node = self.__type_cast(next_id)
            res = node.value
            x = self.__type_cast(prev_id).npx ^ id(node)
            y = self.__type_cast(prev_id)
            y.npx = x ^ 0
            self.tail = y
            return res

    # method to traverse linked list
    def Print(self):
        """We are printing values rather than returning it bacause
        for returning we have to append all values in a list
        and it takes extra memory to save all values in a list."""

        if self.head != None:
            prev_id = 0
            node = self.head
            next_id = 1
            print(node.value, end=' ')
            while next_id:
                next_id = prev_id ^ node.npx
                if next_id:
                    prev_id = id(node)
                    node = self.__type_cast(next_id)
                    print(node.value, end=' ')
                else:
                    return
        else:
            print("List is empty !")

    # method to traverse linked list in reverse order
    def ReversePrint(self):

        # Print Values is reverse order.
        """We are printing values rather than returning it bacause
        for returning we have to append all values in a list
        and it takes extra memory to save all values in a list."""

        if self.head != None:
            prev_id = 0
            node = self.tail
            next_id = 1
            print(node.value, end=' ')
            while next_id:
                next_id = prev_id ^ node.npx
                if next_id:
                    prev_id = id(node)
                    node = self.__type_cast(next_id)
                    print(node.value, end=' ')
                else:
                    return
        else:
            print("List is empty !")

    # method to get length of linked list
    def Length(self):
        if not self.isEmpty():
            prev_id = 0
            node = self.head
            next_id = 1
            count = 1
            while next_id:
                next_id = prev_id ^ node.npx
                if next_id:
                    prev_id = id(node)
                    node = self.__type_cast(next_id)
                    count += 1
                else:
                    return count
        else:
            return 0

    # method to get node data value by index
    def PrintByIndex(self, index):
        prev_id = 0
        node = self.head
        for i in range(index):
            next_id = prev_id ^ node.npx

            if next_id:
                prev_id = id(node)
                node = self.__type_cast(next_id)
            else:
                return "Value dosn't found index out of range."
        return node.value

    # method to check if the liked list is empty or not
    def isEmpty(self):
        if self.head is None:
            return True
        return False

    # method to return a new instance of type
    def __type_cast(self, id):
        return ctypes.cast(id, ctypes.py_object).value

# Driver Code

# create object
obj = XorLinkedList()

# insert nodes
obj.InsertAtEnd(2)
obj.InsertAtEnd(3)
obj.InsertAtEnd(4)
obj.InsertAtStart(0)
obj.InsertAtStart(6)
obj.InsertAtEnd(55)

# display length
print("\nLength:", obj.Length())

# traverse
print("\nTraverse linked list:")
obj.Print()

print("\nTraverse in reverse order:")
obj.ReversePrint()

# display data values by index
print('\nNodes:')
for i in range(obj.Length()):
    print("Data value at index", i, 'is', obj.PrintByIndex(i))

# removing nodes
print("\nDelete Last Node: ", obj.DeleteAtEnd())
print("\nDelete First Node: ", obj.DeleteAtStart())

# new length
print("\nUpdated length:", obj.Length())

# display data values by index
print('\nNodes:')
for i in range(obj.Length()):
    print("Data value at index", i, 'is', obj.PrintByIndex(i))

# traverse
print("\nTraverse linked list:")
obj.Print()

print("\nTraverse in reverse order:")
obj.ReversePrint()
```

**输出:**

```
Length: 6

Traverse linked list:
6 0 2 3 4 55 
Traverse in reverse order:
55 4 3 2 0 6 
Nodes:
Data value at index 0 is 6
Data value at index 1 is 0
Data value at index 2 is 2
Data value at index 3 is 3
Data value at index 4 is 4
Data value at index 5 is 55

Delete Last Node:  55

Delete First Node:  6

Updated length: 4

Nodes:
Data value at index 0 is 0
Data value at index 1 is 2
Data value at index 2 is 3
Data value at index 3 is 4

Traverse linked list:
0 2 3 4 
Traverse in reverse order:
4 3 2 0

```

在 Python 垃圾收集器中，当节点的对象为 XORed 时，收集节点并减少节点对象的引用计数，Python 认为没有办法访问节点，所以我们使用 _ _ 来存储节点的对象，只是为了防止它成为垃圾。