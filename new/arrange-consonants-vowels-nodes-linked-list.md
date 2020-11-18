# 在链接列表中排列辅音和元音节点

给定一个单链列表，我们需要以这样的方式排列它的辅音和元音节点：所有元音节点都在辅音之前出现，同时保持其到达的顺序。

例子：

```
Input : a -> b -> c -> e -> d -> 
        o -> x -> i
Output : a -> e -> o -> i -> b -> 
         c -> d -> x 

```

**解决方案：**
这个想法是在遍历列表时保留我们发现的最新元音的标记。 如果找到另一个元音，则将其从链中取出并放在现有的最新元音之后。 示例：对于链表：

```
a -> b -> c -> e -> d -> o -> x -> i

```

说我们的最新 Vowel 参考引用了“ a”节点，并且我们目前已到达“ e”节点。 我们的确是：

```
a -> e -> b -> c -> d -> o -> x -> i

```

因此，删除“ a”节点之后的位置现在是“ e”节点之后的位置，并将“ a”直接链接到“ e”之后。

要正确删除和添加链接，最好先使用要检查的节点。 因此，如果您有*信号*，则将检查节点-下一个节点的>，以查看它是否是元音。 如果是这样，我们需要将其添加到 lastVowel 节点之后，然后很容易地通过将其 next 分配给 curr next 来将其从链中删除。 另外，如果列表仅包含辅音，我们只需返回 head。

## C++

```cpp

/* C++ program to arrange consonants and 
   vowels nodes in a linked list */
#include<bits/stdc++.h> 
using namespace std; 

/* A linked list node */
struct Node 
{ 
    char data; 
    struct Node *next; 
}; 

/* Function to add new node to the List */
Node *newNode(char key) 
{ 
    Node *temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

// utility function to print linked list 
void printlist(Node *head) 
{ 
    if (! head) 
    { 
        cout << "Empty List\n"; 
        return; 
    } 
    while (head != NULL) 
    { 
        cout << head->data << " "; 
        if (head->next) 
           cout << "-> "; 
        head = head->next; 
    } 
    cout << endl; 
} 

// utility function for checking vowel 
bool isVowel(char x) 
{ 
    return (x == 'a' || x == 'e' || x == 'i' || 
            x == 'o' || x == 'u'); 
} 

/* function to arrange consonants and 
   vowels nodes */
Node *arrange(Node *head) 
{ 
    Node *newHead = head; 

    // for keep track of vowel 
    Node *latestVowel; 

    Node *curr = head; 

    // list is empty 
    if (head == NULL) 
        return NULL; 

    // We need to discover the first vowel 
    // in the list. It is going to be the 
    // returned head, and also the initial 
    // latestVowel. 
    if (isVowel(head->data)) 

        // first element is a vowel. It will 
        // also be the new head and the initial 
        // latestVowel; 
        latestVowel = head; 

    else
    { 

        // First element is not a vowel. Iterate 
        // through the list until we find a vowel. 
        // Note that curr points to the element 
        // *before* the element with the vowel. 
        while (curr->next != NULL && 
               !isVowel(curr->next->data)) 
            curr = curr->next; 

        // This is an edge case where there are 
        // only consonants in the list. 
        if (curr->next == NULL) 
            return head; 

        // Set the initial latestVowel and the 
        // new head to the vowel item that we found. 
        // Relink the chain of consonants after 
        // that vowel item: 
        // old_head_consonant->consonant1->consonant2-> 
        // vowel->rest_of_list becomes 
        // vowel->old_head_consonant->consonant1-> 
        // consonant2->rest_of_list 
        latestVowel = newHead = curr->next; 
        curr->next = curr->next->next; 
        latestVowel->next = head; 
    } 

    // Now traverse the list. Curr is always the item 
    // *before* the one we are checking, so that we 
    // can use it to re-link. 
    while (curr != NULL && curr->next != NULL) 
    { 
        if (isVowel(curr->next->data)) 
        { 
            // The next discovered item is a vowel 
            if (curr == latestVowel) 
            { 
                // If it comes directly after the 
                // previous vowel, we don't need to 
                // move items around, just mark the 
                // new latestVowel and advance curr. 
                latestVowel = curr = curr->next; 
            } 
            else
            { 

                // But if it comes after an intervening 
                // chain of consonants, we need to chain 
                // the newly discovered vowel right after 
                // the old vowel. Curr is not changed as 
                // after the re-linking it will have a 
                // new next, that has not been checked yet, 
                // and we always keep curr at one before 
                // the next to check. 
                Node *temp = latestVowel->next; 

                // Chain in new vowel 
                latestVowel->next = curr->next; 

                // Advance latestVowel 
                latestVowel = latestVowel->next; 

                // Remove found vowel from previous place 
                curr->next = curr->next->next; 

                // Re-link chain of consonants after latestVowel 
                latestVowel->next = temp; 
            } 
        } 
        else
        { 

            // No vowel in the next element, advance curr. 
            curr = curr->next; 
        } 
    } 
    return newHead; 
} 

// Driver code 
int main() 
{ 
    Node *head = newNode('a'); 
    head->next = newNode('b'); 
    head->next->next = newNode('c'); 
    head->next->next->next = newNode('e'); 
    head->next->next->next->next = newNode('d'); 
    head->next->next->next->next->next = newNode('o'); 
    head->next->next->next->next->next->next = newNode('x'); 
    head->next->next->next->next->next->next->next = newNode('i'); 

    printf("Linked list before :\n"); 
    printlist(head); 

    head = arrange(head); 

    printf("Linked list after :\n"); 
    printlist(head); 

    return 0; 
} 

```

## Java

```java

/* Java program to arrange consonants and  
vowels nodes in a linked list */
class GfG 
{  

/* A linked list node */
static class Node  
{  
    char data;  
    Node next;  
} 

/* Function to add new node to the List */
static Node newNode(char key)  
{  
    Node temp = new Node();  
    temp.data = key;  
    temp.next = null;  
    return temp;  
}  

// utility function to print linked list  
static void printlist(Node head)  
{  
    if (head == null)  
    {  
        System.out.println("Empty List");  
        return;  
    }  
    while (head != null)  
    {  
        System.out.print(head.data +" ");  
        if (head.next != null)  
        System.out.print("-> ");  
        head = head.next;  
    }  
    System.out.println(); 
}  

// utility function for checking vowel  
static boolean isVowel(char x)  
{  
    return (x == 'a' || x == 'e' || x == 'i' ||  
            x == 'o' || x == 'u');  
}  

/* function to arrange consonants and  
vowels nodes */
static Node arrange(Node head)  
{  
    Node newHead = head;  

    // for keep track of vowel  
    Node latestVowel;  

    Node curr = head;  

    // list is empty  
    if (head == null)  
        return null;  

    // We need to discover the first vowel  
    // in the list. It is going to be the  
    // returned head, and also the initial  
    // latestVowel.  
    if (isVowel(head.data) == true)  

        // first element is a vowel. It will  
        // also be the new head and the initial  
        // latestVowel;  
        latestVowel = head;  

    else
    {  

        // First element is not a vowel. Iterate  
        // through the list until we find a vowel.  
        // Note that curr points to the element  
        // *before* the element with the vowel.  
        while (curr.next != null &&  
            !isVowel(curr.next.data))  
            curr = curr.next;  

        // This is an edge case where there are  
        // only consonants in the list.  
        if (curr.next == null)  
            return head;  

        // Set the initial latestVowel and the  
        // new head to the vowel item that we found.  
        // Relink the chain of consonants after  
        // that vowel item:  
        // old_head_consonant->consonant1->consonant2->  
        // vowel->rest_of_list becomes  
        // vowel->old_head_consonant->consonant1->  
        // consonant2->rest_of_list  
        latestVowel = newHead = curr.next;  
        curr.next = curr.next.next;  
        latestVowel.next = head;  
    }  

    // Now traverse the list. Curr is always the item  
    // *before* the one we are checking, so that we  
    // can use it to re-link.  
    while (curr != null && curr.next != null)  
    {  
        if (isVowel(curr.next.data) == true)  
        {  
            // The next discovered item is a vowel  
            if (curr == latestVowel)  
            {  
                // If it comes directly after the  
                // previous vowel, we don't need to  
                // move items around, just mark the  
                // new latestVowel and advance curr.  
                latestVowel = curr = curr.next;  
            }  
            else
            {  

                // But if it comes after an intervening  
                // chain of consonants, we need to chain  
                // the newly discovered vowel right after  
                // the old vowel. Curr is not changed as  
                // after the re-linking it will have a  
                // new next, that has not been checked yet,  
                // and we always keep curr at one before  
                // the next to check.  
                Node temp = latestVowel.next;  

                // Chain in new vowel  
                latestVowel.next = curr.next;  

                // Advance latestVowel  
                latestVowel = latestVowel.next;  

                // Remove found vowel from previous place  
                curr.next = curr.next.next;  

                // Re-link chain of consonants after latestVowel  
                latestVowel.next = temp;  
            }  
        }  
        else
        {  

            // No vowel in the next element, advance curr.  
            curr = curr.next;  
        }  
    }  
    return newHead;  
}  

// Driver code  
public static void main(String[] args)  
{  
    Node head = newNode('a');  
    head.next = newNode('b');  
    head.next.next = newNode('c');  
    head.next.next.next = newNode('e');  
    head.next.next.next.next = newNode('d');  
    head.next.next.next.next.next = newNode('o');  
    head.next.next.next.next.next.next = newNode('x');  
    head.next.next.next.next.next.next.next = newNode('i');  

    System.out.println("Linked list before : ");  
    printlist(head);  

    head = arrange(head);  

    System.out.println("Linked list after :");  
    printlist(head);  
} 
}  

// This code is contributed by Prerna Saini. 

```

## C#

```cs

/* C# program to arrange consonants and  
vowels nodes in a linked list */
using System;  

class GfG 
{  

    /* A linked list node */
    public class Node  
    {  
        public char data;  
        public Node next;  
    } 

    /* Function to add new node to the List */
    static Node newNode(char key)  
    {  
        Node temp = new Node();  
        temp.data = key;  
        temp.next = null;  
        return temp;  
    }  

    // utility function to print linked list  
    static void printlist(Node head)  
    {  
        if (head == null)  
        {  
            Console.WriteLine("Empty List");  
            return;  
        }  
        while (head != null)  
        {  
            Console.Write(head.data +" ");  
            if (head.next != null)  
                Console.Write("-> ");  
            head = head.next;  
        }  
        Console.WriteLine(); 
    }  

    // utility function for checking vowel  
    static bool isVowel(char x)  
    {  
        return (x == 'a' || x == 'e' || x == 'i' ||  
                x == 'o' || x == 'u');  
    }  

    /* function to arrange consonants and  
    vowels nodes */
    static Node arrange(Node head)  
    {  
        Node newHead = head;  

        // for keep track of vowel  
        Node latestVowel;  

        Node curr = head;  

        // list is empty  
        if (head == null)  
            return null;  

        // We need to discover the first vowel  
        // in the list. It is going to be the  
        // returned head, and also the initial  
        // latestVowel.  
        if (isVowel(head.data) == true)  

            // first element is a vowel. It will  
            // also be the new head and the initial  
            // latestVowel;  
            latestVowel = head;  

        else
        {  

            // First element is not a vowel. Iterate  
            // through the list until we find a vowel.  
            // Note that curr points to the element  
            // *before* the element with the vowel.  
            while (curr.next != null &&  
                !isVowel(curr.next.data))  
                curr = curr.next;  

            // This is an edge case where there are  
            // only consonants in the list.  
            if (curr.next == null)  
                return head;  

            // Set the initial latestVowel and the  
            // new head to the vowel item that we found.  
            // Relink the chain of consonants after  
            // that vowel item:  
            // old_head_consonant->consonant1->consonant2->  
            // vowel->rest_of_list becomes  
            // vowel->old_head_consonant->consonant1->  
            // consonant2->rest_of_list  
            latestVowel = newHead = curr.next;  
            curr.next = curr.next.next;  
            latestVowel.next = head;  
        }  

        // Now traverse the list. Curr is always the item  
        // *before* the one we are checking, so that we  
        // can use it to re-link.  
        while (curr != null && curr.next != null)  
        {  
            if (isVowel(curr.next.data) == true)  
            {  
                // The next discovered item is a vowel  
                if (curr == latestVowel)  
                {  
                    // If it comes directly after the  
                    // previous vowel, we don't need to  
                    // move items around, just mark the  
                    // new latestVowel and advance curr.  
                    latestVowel = curr = curr.next;  
                }  
                else
                {  

                    // But if it comes after an intervening  
                    // chain of consonants, we need to chain  
                    // the newly discovered vowel right after  
                    // the old vowel. Curr is not changed as  
                    // after the re-linking it will have a  
                    // new next, that has not been checked yet,  
                    // and we always keep curr at one before  
                    // the next to check.  
                    Node temp = latestVowel.next;  

                    // Chain in new vowel  
                    latestVowel.next = curr.next;  

                    // Advance latestVowel  
                    latestVowel = latestVowel.next;  

                    // Remove found vowel from previous place  
                    curr.next = curr.next.next;  

                    // Re-link chain of consonants after latestVowel  
                    latestVowel.next = temp;  
                }  
            }  
            else
            {  

                // No vowel in the next element, advance curr.  
                curr = curr.next;  
            }  
        }  
        return newHead;  
    }  

    // Driver code  
    public static void Main(String[] args)  
    {  
        Node head = newNode('a');  
        head.next = newNode('b');  
        head.next.next = newNode('c');  
        head.next.next.next = newNode('e');  
        head.next.next.next.next = newNode('d');  
        head.next.next.next.next.next = newNode('o');  
        head.next.next.next.next.next.next = newNode('x');  
        head.next.next.next.next.next.next.next = newNode('i');  

        Console.WriteLine("Linked list before : ");  
        printlist(head);  

        head = arrange(head);  

        Console.WriteLine("Linked list after :");  
        printlist(head);  
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
Linked list before :
a -> b -> c -> e -> d -> o -> x -> i 
Linked list after :
a -> e -> o -> i -> b -> c -> d -> x 

```

参考：
[Stackoverflow](https://stackoverflow.com/questions/31489675/seperatiing-vowels-and-consonents-of-linked-list-in-java)

本文由 **Gaurav Miglani** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

