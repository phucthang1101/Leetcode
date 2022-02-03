# [1. Two Sum (Easy)](https://leetcode.com/problems/two-sum/)

<p>Given an array of integers <code>nums</code>&nbsp;and an integer <code>target</code>, return <em>indices of the two numbers such that they add up to <code>target</code></em>.</p>

<p>You may assume that each input would have <strong><em>exactly</em> one solution</strong>, and you may not use the <em>same</em> element twice.</p>

<p>You can return the answer in any order.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [2,7,11,15], target = 9
<strong>Output:</strong> [0,1]
<strong>Output:</strong> Because nums[0] + nums[1] == 9, we return [0, 1].
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [3,2,4], target = 6
<strong>Output:</strong> [1,2]
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> nums = [3,3], target = 6
<strong>Output:</strong> [0,1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= target &lt;= 10<sup>9</sup></code></li>
	<li><strong>Only one valid answer exists.</strong></li>
</ul>

<p>&nbsp;</p>
<strong>Follow-up:&nbsp;</strong>Can you come up with an algorithm that is less than&nbsp;<code>O(n<sup>2</sup>)&nbsp;</code>time complexity?

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/)

**Similar Questions**:
* [3Sum (Medium)](https://leetcode.com/problems/3sum/)
* [4Sum (Medium)](https://leetcode.com/problems/4sum/)
* [Two Sum II - Input array is sorted (Easy)](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
* [Two Sum III - Data structure design (Easy)](https://leetcode.com/problems/two-sum-iii-data-structure-design/)
* [Subarray Sum Equals K (Medium)](https://leetcode.com/problems/subarray-sum-equals-k/)
* [Two Sum IV - Input is a BST (Easy)](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/)
* [Two Sum Less Than K (Easy)](https://leetcode.com/problems/two-sum-less-than-k/)
* [Max Number of K-Sum Pairs (Medium)](https://leetcode.com/problems/max-number-of-k-sum-pairs/)
* [Count Good Meals (Medium)](https://leetcode.com/problems/count-good-meals/)


## Solution 1.

```cpp
// Time: O(NlogN)
// Space: O(N)
class Solution {
public:
    /* Sliding Window Technique, but it takes up to O(N^2) time complexity, hence we need another data structure to reduce time complexity*/
    vector<int> twoSum(vector<int>& nums, int target){
        int n = nums.size();
        
        for(int left=0;left < n-1;left++)
        {
            for(int right=n-1; right>left; right--)
            {
                if(nums[left] + nums[right] == target)
                    return vector<int>{left, right};
            }
        }
       
        
       return vector<int>{0, 0};
    }
};
```

## Solution 2.

```cpp
// Time: O(N)
// Space: O(N)
class Solution {
public:
    // Increase Space Complexity | Reduce Time Complexity
    vector<int> twoSum(vector<int>& nums, int target) 
    {
        //Key is the number and value is its index in the vector.
        unordered_map<int, int> map;
        
        for(int i=0;i<nums.size();i++)
        {
            int numberToFind = target - nums[i];
            if(map.count(numberToFind))
            {
              // Return Index of numberToFind and currentIndex (i)
                return vector<int>{map[numberToFind],i};
            }
            
            //number was not found. Put it in the map.
            map[nums[i]] = i; 
        }
        
        return vector<int>{0, 0};
    }
};
```
