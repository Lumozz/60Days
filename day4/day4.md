# 

# 24. 两两交换链表中的节点

```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummy = new ListNode(0, head);
        ListNode* prev = dummy;

        ListNode* first;
        ListNode* second;

        while(prev -> next != nullptr && prev -> next -> next != nullptr){
            first = prev -> next;
            second = prev -> next -> next;

            first -> next = first -> next -> next;
            second -> next = first;

            prev -> next = second;
            prev = first;
        }

        return dummy -> next;
    }
};
```

# 19.删除链表的倒数第N个节点

好记性不如烂笔头，在纸上多画画！

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode(0, head);
        ListNode* fast = dummy;
        ListNode* slow = dummy;

        for(int i=0; i<=n; ++i){
            fast = fast -> next;
        }

        while(fast != nullptr){
            fast = fast -> next;
            slow = slow -> next;
        }

        slow -> next  = slow -> next -> next;

        return dummy -> next;
    }
};
```



# 面试题 02.07. 链表相交

双指针法更加精妙，但这一题用哈希表来做更加常规。熟练使用常规做法更加重要

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        unordered_set<ListNode*> visited;
        ListNode* tmp = headA;
        while(tmp != nullptr){
            visited.insert(tmp);
            tmp = tmp -> next;
        }

        tmp = headB;
        while(tmp != nullptr){
            if(visited.count(tmp)){
                return tmp;
            }
            tmp = tmp -> next;
        }
        return nullptr;
    }
};
```

# 142.环形链表II

与上一题相同，首先考虑使用哈希表解决此问题。遍历节点，将节点地址插入表中，如果表中已有该节点，则表示已经找到入环点。

```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        unordered_set<ListNode*> listSet;

        while(head != nullptr){
            if(listSet.count(head)){
                return head;
            } else {
                listSet.insert(head);
                head = head -> next;
            }
        }
        return NULL;
    }
};
```

- 方法2 快慢指针
  
  为什么快慢指针在环内一定会相遇？因为快指针每次只比慢指针块一步，快指针相对于慢指针每次只走一步，因此二者一定会相遇。下面是网站代码：
  
  ```
  class Solution {
  public:
      ListNode *detectCycle(ListNode *head) {
          ListNode* fast = head;
          ListNode* slow = head;
          while(fast != NULL && fast->next != NULL) {
              slow = slow->next;
              fast = fast->next->next;
              // 快慢指针相遇，此时从head 和 相遇点，同时查找直至相遇
              if (slow == fast) {
                  ListNode* index1 = fast;
                  ListNode* index2 = head;
                  while (index1 != index2) {
                      index1 = index1->next;
                      index2 = index2->next;
                  }
                  return index2; // 返回环的入口
              }
          }
          return NULL;
      }
  };
  ```


