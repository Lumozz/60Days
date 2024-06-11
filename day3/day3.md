# 203.移除链表元素

链表基础题，当当前节点值为目标值时，将上一节点指针指向下一节点

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode dummy(0, head);
        ListNode* newHead = &dummy;
        ListNode* cur = &dummy;

        while(cur -> next != nullptr){
            if(cur -> next -> val == val){
                ListNode* tmp = cur -> next;
                cur -> next = cur -> next -> next;
                delete tmp;
            } else {
                cur = cur -> next;
            }
        }

        return newHead -> next;
    }
};
```

思路很简单，但是有些细节需要注意：

- 为防止内存泄漏，需要手动销毁链表中被删除的点。这里默认列表中的点是动态分配的，在堆区的。至于为什么在堆区，为什么是动态分配的，只能说是惯例。

- 当声明一个哑节点时，先声明一个节点变量，再声明一个指向该节点的指针，此时节点是分配在堆上的。也可以用`ListNode* newHead = new ListNode()`来分配一个需要手动释放的动态内存变量。



# 707.设计链表

这题的重点在于实现一个完整的类，可以复习语法。算法倒是很简单，没什么难度。

```c++
class MyLinkedList {
public:
    struct Node{
        int val;
        Node* next;
        Node():val(0), next(nullptr){};
        Node(int val): val(val), next(nullptr){};
        Node(int val, Node* next): val(val), next(next){};
    };


    int nodeNum;
    Node* nodeHead = nullptr;


    MyLinkedList() {
        nodeNum = 0;
    }
    
    int get(int index) {
        if(index < 0 || index >= nodeNum || nodeHead == nullptr){
            return -1;
        } 
        Node* curr = nodeHead;
        for(int i=0; i<index; ++i){
            curr = curr -> next;
        }
        return curr -> val;
        
    }
    
    void addAtHead(int val) {
        if(nodeHead == nullptr){
            nodeHead = new Node(val);
        } else {
            Node* newHead = new Node(val, nodeHead);
            nodeHead = newHead;
        }
        ++nodeNum;
    }
    
    void addAtTail(int val) {
        if(nodeHead == nullptr){
            nodeHead = new Node(val);
            ++nodeNum;
            return;
        }
        Node* curr = nodeHead;
        while(curr -> next != nullptr){
            curr = curr -> next;
        }
        Node* trail = new Node(val);
        curr -> next = trail;

        ++nodeNum;

        return;
    }
    
    void addAtIndex(int index, int val) {
        if(index > nodeNum ){
            return;
        }

        if (index == 0){
            this -> addAtHead(val);
        } else if (index == nodeNum){
            this -> addAtTail(val);

        } else{
            Node* curr = nodeHead;
            
            for(int i=0; i<index-1; ++i){
                curr = curr -> next;
            }
            if(curr != nullptr) { // 添加检查
                curr -> next = new Node(val, curr -> next);
                ++nodeNum;
            }

        }
    }
    
    void deleteAtIndex(int index) {
        if(index >= nodeNum || nodeHead == nullptr){
            return;
        } else {
            Node* curr = nodeHead;
            if(index == 0){
                nodeHead = nodeHead -> next;
                delete curr; 
                --nodeNum;
                return;
            }
            for(int i=0; i<index-1; ++i){
                curr = curr -> next;
            }
        
            Node* tmp = curr -> next;
            curr -> next = curr -> next -> next;
            delete tmp;
            --nodeNum;
            return;
                   
        }

    }
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList* obj = new MyLinkedList();
 * int param_1 = obj->get(index);
 * obj->addAtHead(val);
 * obj->addAtTail(val);
 * obj->addAtIndex(index,val);
 * obj->deleteAtIndex(index);
 */teAtIndex(index);
 */leteAtIndex(index);
 */(index);
 */dAtIndex(index,val);
 * obj->deleteAtIndex(index);
 */
```

# 206. 反转链表

```
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = nullptr;
        ListNode* curr = head;

        while(curr != nullptr){
            ListNode* next = curr -> next;
            curr -> next = prev;
            prev = curr;
            curr = next;
        }

        return prev;

    }
};
```




