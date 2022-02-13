# [15. 3Sum (Medium)](https://leetcode.com/problems/3sum/)

<p>Given an integer array nums, return all the triplets <code>[nums[i], nums[j], nums[k]]</code> such that <code>i != j</code>, <code>i != k</code>, and <code>j != k</code>, and <code>nums[i] + nums[j] + nums[k] == 0</code>.</p>

<p>Notice that the solution set must not contain duplicate triplets.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [-1,0,1,2,-1,-4]
<strong>Output:</strong> [[-1,-1,2],[-1,0,1]]
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> nums = []
<strong>Output:</strong> []
</pre><p><strong>Example 3:</strong></p>
<pre><strong>Input:</strong> nums = [0]
<strong>Output:</strong> []
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= nums.length &lt;= 3000</code></li>
	<li><code>-10<sup>5</sup> &lt;= nums[i] &lt;= 10<sup>5</sup></code></li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Facebook](https://leetcode.com/company/facebook), [Microsoft](https://leetcode.com/company/microsoft), [Apple](https://leetcode.com/company/apple), [Bloomberg](https://leetcode.com/company/bloomberg), [Uber](https://leetcode.com/company/uber), [Google](https://leetcode.com/company/google), [Yahoo](https://leetcode.com/company/yahoo), [VMware](https://leetcode.com/company/vmware), [Walmart Labs](https://leetcode.com/company/walmart-labs), [Cisco](https://leetcode.com/company/cisco), [Rubrik](https://leetcode.com/company/rubrik), [Salesforce](https://leetcode.com/company/salesforce), [eBay](https://leetcode.com/company/ebay), [Adobe](https://leetcode.com/company/adobe)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Two Pointers](https://leetcode.com/tag/two-pointers/)

**Similar Questions**:
* [Two Sum (Easy)](https://leetcode.com/problems/two-sum/)
* [3Sum Closest (Medium)](https://leetcode.com/problems/3sum-closest/)
* [4Sum (Medium)](https://leetcode.com/problems/4sum/)
* [3Sum Smaller (Medium)](https://leetcode.com/problems/3sum-smaller/)

## Solution 1.
the key idea is the same as the TwoSum problem. When we fix the 1st number, the 2nd and 3rd number can be found following the same reasoning as TwoSum.

The only difference is that, the TwoSum problem of LEETCODE has a unique solution. However, in ThreeSum, we have multiple duplicate solutions that can be found. Most of the OLE errors happened here because you could've ended up with a solution with so many duplicates.

Sort the array in ascending order.

Pin the first number as `A[i]`. For the other two numbers, apply the same rules as TwoSum problem,


HashMap Approach:

In this approach, firstly, we will hash the indices of all elements in a hashMap. In case of repeated elements, the last occurence index would be stored in hashMap.

Here also we fix a number (num[i]), by traversing the loop. But the loop traversal here for fixing numbers would leave last two indices. These last two indices would be covered by the nested loop.

If number fixed is (+) positive, break there because we can't make it zero by searching after it. (cuz we've already sorted the array)

Make a nested loop to fix a number after the first fixed number. (num[curr])

To make sum 0, we would require the -ve sum of both fixed numbers. Let us say this required.

Now, we will find the this required number in hashMap. 

<b>**Notice: If it exists in hashmap and its last occurrence index > 2nd fixed index, we found our triplet.
  
  Push it in answer vector.
  
  Update j to last occurence of 2nd fixed number to avoid duplicate triplets.
  
  Update i to last occurence of 1st fixed number to avoid duplicate triplets.

</b>
Return answer vector.




```cpp

// Time: O(N^2)
// Space: O(1)
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums){
        sort(nums.begin(),nums.end());
        int n = nums.size();
        
        if(n < 3)           //Base case 1
            return {};
        
        // Base case 2: cuz we've already sorted the array so the 1st must < 0, or else we cannot find any element after to + = 0    
        if(nums[0] > 0)     
            return {};
        
        
        //In this approach, firstly, we will hash the indices of all elements in a hashMap. In case of repeated elements, the last occurence index would be stored in hashMap.
        unordered_map<int,int> map; 
        for(int i = 0; i < n; i++)
            map[nums[i]] = i;
        
        vector<vector<int>> res;
        
        // Cuz we will deal with the current, and 2 next element so we just need to traverse to n-3 position and we will be left with n-2 and n-1 elemet to consider if its matched
        for(int curr = 0; curr < n - 2; curr++){
            if(nums[curr] > 0) //If number fixed is POSITIVE (+), stop there because we can't make it zero by searching after it.
                break;
            else {
                
                
                for(int start = curr+1; start < n-1; start++){
                    int target = -(nums[curr] + nums[start]);   //To make sum 0, we would require the NEGATIVE(-) sum of both fixed numbers (nums[curr]+nums[left] . Let us say this 'target'.

            //Now, we will find the this required number in hashMap. If it exists in hashmap and its last occurrence index > 2nd fixed index, we found our triplet. Push it in answer vector.
                    if(map.count(target) && map[target] > start){
                        res.push_back({nums[curr], nums[start], target});
                    }
                    
                    //Now, update 'start' to last occurence of 2nd fixed number to avoid duplicate triplets.
                    start = map[nums[start]];
                }
                
                
                //Update 'curr' to last occurence of 1st fixed number to avoid duplicate triplets.
                curr = map[nums[curr]];
            }
        }
        return res;   
    }
    
};
```
