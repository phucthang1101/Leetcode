# [19. Remove Nth Node From End of List (Medium)](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

<p>Given the <code>head</code> of a linked list, remove the <code>n<sup>th</sup></code> node from the end of the list and return its head.</p>

<p><strong>Follow up:</strong>&nbsp;Could you do this in one pass?</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg" style="width: 542px; height: 222px;">
<pre><strong>Input:</strong> head = [1,2,3,4,5], n = 2
<strong>Output:</strong> [1,2,3,5]
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> head = [1], n = 1
<strong>Output:</strong> []
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> head = [1,2], n = 1
<strong>Output:</strong> [1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is <code>sz</code>.</li>
	<li><code>1 &lt;= sz &lt;= 30</code></li>
	<li><code>0 &lt;= Node.val &lt;= 100</code></li>
	<li><code>1 &lt;= n &lt;= sz</code></li>
</ul>


**Related Topics**:  
[Linked List](https://leetcode.com/tag/linked-list/), [Two Pointers](https://leetcode.com/tag/two-pointers/)

**Similar Questions**:
* [Swapping Nodes in a Linked List (Medium)](https://leetcode.com/problems/swapping-nodes-in-a-linked-list/)
* [Delete N Nodes After M Nodes of a Linked List (Easy)](https://leetcode.com/problems/delete-n-nodes-after-m-nodes-of-a-linked-list/)

## Solution 1.

```cpp
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
    /*
      The difference between the FINAL node and the TO_BE_DELETED node is N, so the method here is:
      Basically, we will first more FAST pointer ahead N nodes from the start, assign SLOW at the start
      So now we just need to move both FAST and SLOW toward UNTILL fast->next is NULL, then SLOW will stay exactly at the PREVIOUS of nth Node from the end of the list.
      At last, delete it by slow->next = slow->next->next;
      
      Why using while(fast->next)? Because if we use as normal while(fast), then we will end up with slow pointing at the TO_BE_DELETED node and we cannot delete it.
    */
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        
        ListNode *slow = head, *fast = head;
        
        for(int i = 0; i < n; i++){
            fast = fast->next;
        }
        
        if(fast == NULL)
            return head->next;
        
        while(fast->next != NULL){
            fast = fast->next;
            slow = slow->next;
        }
        slow->next = slow->next->next;
        return head;
    }
};
```
