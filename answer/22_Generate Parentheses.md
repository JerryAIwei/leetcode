Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]


source:LeetCode https://leetcode-cn.com/problems/generate-parentheses/
***

DP, use hash_map to store the sub result

time complex: O(4^n/sqrt(n))  

space complex: O(4^n/sqrt(n))

```
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> results; 
        std::unordered_map<int, vector<string>> subs;
        if(n==0)
            results.push_back("");
        else{
            vector<string> temp1;
            vector<string> temp2;
            for(int i =0;i < n;++i){
                if(subs.find(i)==subs.end()) subs[i] = generateParenthesis(i);
                if(subs.find(n-i-1)==subs.end()) subs[n-i-1] = generateParenthesis(n-i-1);
                temp1 = subs[i];
                temp2 = subs[n-i-1];
                for(auto str1 = temp1.begin();str1<temp1.end();++str1)
                    for(auto str2 = temp2.begin();str2<temp2.end();++str2){
                        
                        results.push_back("("+*str1+")"+*str2);
                    }
            }
        }
        return results;
    }
};
```