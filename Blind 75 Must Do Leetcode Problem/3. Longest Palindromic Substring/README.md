# [5. Longest Palindromic Substring (Medium)](https://leetcode.com/problems/longest-palindromic-substring/)

<p>Given a string <code>s</code>, return&nbsp;<em>the longest palindromic substring</em> in <code>s</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "babad"
<strong>Output:</strong> "bab"
<strong>Note:</strong> "aba" is also a valid answer.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "cbbd"
<strong>Output:</strong> "bb"
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = "a"
<strong>Output:</strong> "a"
</pre>

<p><strong>Example 4:</strong></p>

<pre><strong>Input:</strong> s = "ac"
<strong>Output:</strong> "a"
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 1000</code></li>
	<li><code>s</code> consist of only digits and English letters.</li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Adobe](https://leetcode.com/company/adobe), [Apple](https://leetcode.com/company/apple), [Wayfair](https://leetcode.com/company/wayfair), [Facebook](https://leetcode.com/company/facebook), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Oracle](https://leetcode.com/company/oracle), [Yahoo](https://leetcode.com/company/yahoo), [Google](https://leetcode.com/company/google), [Docusign](https://leetcode.com/company/docusign), [eBay](https://leetcode.com/company/ebay), [Uber](https://leetcode.com/company/uber), [Walmart Labs](https://leetcode.com/company/walmart-labs), [Salesforce](https://leetcode.com/company/salesforce), [Zoho](https://leetcode.com/company/zoho), [HBO](https://leetcode.com/company/hbo), [Tesla](https://leetcode.com/company/tesla)

**Related Topics**:  
[String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

**Similar Questions**:
* [Shortest Palindrome (Hard)](https://leetcode.com/problems/shortest-palindrome/)
* [Palindrome Permutation (Easy)](https://leetcode.com/problems/palindrome-permutation/)
* [Palindrome Pairs (Hard)](https://leetcode.com/problems/palindrome-pairs/)
* [Longest Palindromic Subsequence (Medium)](https://leetcode.com/problems/longest-palindromic-subsequence/)
* [Palindromic Substrings (Medium)](https://leetcode.com/problems/palindromic-substrings/)

<br/>
<h2>Evolution from Recursion to Top Down DP to Bottoms Up DP and to Efficient method. </h2>

## Solution 1. Recursive
```
//Time Complexity: O(n^3)
//Space Complexity: O(n) -> recursive stack
class Solution {
public:
    string longestPalindrome(string s)
    {
        return longestPalindromeRecursive(s); 
    }
        
    string longestPalindromeRecursive(string s) {
        string res = "";
        
        for(int i=0;i<s.length();i++)
        {
            for(int j=i;j<s.length();j++)
            {
                // check every possible substr
                if(isPalindromeRecursive(s,i,j))
                {
                    res = res.length() > j-i+1 ? res : s.substr(i,j-i+1);
                }
            }
        }
        return res;
    }
    bool isPalindromeRecursive(string s, int i, int j)
    {
        if(i>=j)return true;
        if(s[i] == s[j])
            return isPalindromeRecursive(s,i+1,j-1);
        else
            return false;
            
    }
    
```


## Solution 2. Memoization way
```
//Time Complexity: O(n^2)
//Space Complexity: O(n^2) -> recursive stack + memo
class Solution {
public:
    string longestPalindrome(string s)
    {
        return longestPalindromeMemoization(s); 
    }
        
    string longestPalindromeMemoization(string s)
    {
        string res;
        vector<vector<bool>> memo(s.length(), vector<bool>(s.length(),0));
        for(int i=0;i<s.length();i++)
        {
            for(int j=i;j<s.length();j++)
            {
                if(isPalindromeMemoization(s,i,j,memo))
                {
                    //cout << s.substr(i,j-i+1) << " ";
                    res = res.length() > j-i+1 ? res : s.substr(i,j-i+1);
                }
            }
        }
        return res;
    }
    bool isPalindromeMemoization(string s, int i, int j, vector<vector<bool>>& memo)
    {
        if(i>=j)memo[i][j]=true;
        if(memo[i][j])return memo[i][j];
        if(s[i] == s[j])
            return isPalindromeMemoization(s, i+1, j-1, memo);
        else
            return false;
    }    
```


## Solution 3. Tabulation way (DP)
```
//Time Complexity: O(n^2)
//Space Complexity: O(n^2) -> dp
class Solution {
public:
    string longestPalindrome(string s)
    {
        return longestPalindromeTabulation(s); 
    }
        
    string longestPalindromeTabulation(string s)
    {
        int length = s.length();
        vector<vector<int>> dp(length, vector<int>(length,0));
        string res = "";
        int maxLen = 0, maxPos = 0;
      
        for(int i=length-1;i>=0;i--)
        {
            for(int j=i;j<length;j++)
            {
                if(i==j)
                    dp[i][j] = 1;
                else if(i+1==j)
                    dp[i][j] = s[i] == s[j] ? 2:0;
                else
                {
                    dp[i][j] = s[i] == s[j] && dp[i+1][j-1] ? 2+dp[i+1][j-1] : 0;
                }
               
                if(maxLen < dp[i][j])
                {
                    
                    maxLen = dp[i][j];
                    maxPos = i;
                }
              
            }
        }
        return s.substr(maxPos, maxLen);
    } 
```


## Solution 4. DP way
Since `dp[i][j]` only depends on `dp[i + 1][j - 1]`, we can reduce the space complexity from `O(N^2)` to `O(N)`.

```cpp
// OJ: https://leetcode.com/problems/longest-palindromic-substring/
// Author: github.com/lzl124631x
// Time: O(N^2)
// Space: O(N)
class Solution {
public:
    string longestPalindrome(string s) {
        int N = s.size(), start = 0, len = 0;
        bool dp[1001] = {};
        for (int i = N - 1; i >= 0; --i) {
            for (int j = N - 1; j >= i; --j) {
                if (i == j) dp[j] = true;
                else dp[j] = s[i] == s[j] && (i + 1 > j - 1 || dp[j - 1]);
                if (dp[j] && j - i + 1 > len) {
                    start = i;
                    len = j - i + 1;
                }
            }
        }
        return s.substr(start, len);
    }
};
```


## Solution 5. Expanding from Middle
```
// Time: O(N^2)
// Space: O(1)
//4th: Normally, we will check if a substring is a Palindrome or not by checking its inside-string is a Palindrome or. But in this way, we will check by starting at the currPos and expand to the left and right of its to see if str[left, right] is a Palindrome.
    
    string longestPalindromeEfficientRewrite(string s)
    {
        int length = s.length(), maxLen = 0, maxPos = 0;
        if (length < 2) return s;
        
        for(int i = 0; i < length; i++)
        {
            // calculate Longest Palindromic Substring (LPS) with ODD length (1,3,5,7,...)
            expandPalindrome(s, i,i);
            
            // calculate Longest Palindromic Substring (LPS) with EVEN length  (2,4,6,...)
            expandPalindrome(s, i,i+1);
        }
        return s.substr(maxPos4th, maxLen4th);
    }
    
    void expandPalindrome(string s, int left, int right)
    {
        while(left >= 0 && right < s.length() && s[left]==s[right])
        {
            if(right - left + 1 > maxLen4th)
            {
                maxLen4th = right - left + 1;
                maxPos4th = left;
            }
            left--;
            right++;
        }
    }
```
