# [21. Merge Two Sorted Lists (Easy)](https://leetcode.com/problems/merge-two-sorted-lists/)

<p>Merge two sorted linked lists and return it as a <strong>sorted</strong> list. The list should be made by splicing together the nodes of the first two lists.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg" style="width: 662px; height: 302px;">
<pre><strong>Input:</strong> l1 = [1,2,4], l2 = [1,3,4]
<strong>Output:</strong> [1,1,2,3,4,4]
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> l1 = [], l2 = []
<strong>Output:</strong> []
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> l1 = [], l2 = [0]
<strong>Output:</strong> [0]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in both lists is in the range <code>[0, 50]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
	<li>Both <code>l1</code> and <code>l2</code> are sorted in <strong>non-decreasing</strong> order.</li>
</ul>


**Related Topics**:  
[Linked List](https://leetcode.com/tag/linked-list/), [Recursion](https://leetcode.com/tag/recursion/)

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Facebook](https://leetcode.com/company/facebook), [Google](https://leetcode.com/company/google), [Adobe](https://leetcode.com/company/adobe), [Apple](https://leetcode.com/company/apple), [Bloomberg](https://leetcode.com/company/bloomberg), [Yahoo](https://leetcode.com/company/yahoo), [Arista Networks](https://leetcode.com/company/arista-networks), [Uber](https://leetcode.com/company/uber), [Indeed](https://leetcode.com/company/indeed), [Cisco](https://leetcode.com/company/cisco), [Tencent](https://leetcode.com/company/tencent), [Airbnb](https://leetcode.com/company/airbnb), [Oracle](https://leetcode.com/company/oracle), [IBM](https://leetcode.com/company/ibm), [Huawei](https://leetcode.com/company/huawei), [Paypal](https://leetcode.com/company/paypal), [Yandex](https://leetcode.com/company/yandex)

**Similar Questions**:
* [Merge k Sorted Lists (Hard)](https://leetcode.com/problems/merge-k-sorted-lists/)
* [Merge Sorted Array (Easy)](https://leetcode.com/problems/merge-sorted-array/)
* [Sort List (Medium)](https://leetcode.com/problems/sort-list/)
* [Shortest Word Distance II (Medium)](https://leetcode.com/problems/shortest-word-distance-ii/)
* [Add Two Polynomials Represented as Linked Lists (Medium)](https://leetcode.com/problems/add-two-polynomials-represented-as-linked-lists/)

## Solution 1: Iterative Approach
```cpp
// Time: O(A + B)
// Space: O(1)
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
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode *dummy = new ListNode(0);
        ListNode *res = dummy;
        
        while(list1 != nullptr && list2 != nullptr){
            if(list1->val < list2->val){
                res->next = list1;
                list1 = list1->next;
            }
            else {
                res->next = list2;
                list2 = list2->next;
            }
            res = res->next;
        }
        
        res->next = list1 ? list1 : list2;
        
        return dummy->next;
    }
};
```

## Solution 2. Recursive Approach

```cpp
// OJ: https://leetcode.com/problems/merge-two-sorted-lists/
// Author: github.com/lzl124631x
// Time: O(A + B)
// Space: O(1)
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2){
        if(l1 == NULL)return l2;
        if(l2 == NULL)return l1;
        // if value of l1 > l2 => so we take current l2 and make recursion with (l1, l2->next)
        if(l1->val >= l2->val)l2->next = mergeTwoLists(l1, l2->next);
        else{
            l1->next = mergeTwoLists(l1->next, l2);
            // after all return we assign current l1 to l2, to connect to current list
            l2 = l1;
        }
        return l2;
    }
};
```
