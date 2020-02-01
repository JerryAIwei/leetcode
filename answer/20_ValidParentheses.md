Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

    Open brackets must be closed by the same type of brackets.
    Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

Example 1:

Input: "()"
Output: true

source:LeetCode https://leetcode-cn.com/problems/valid-parentheses/
***

Use stack

time complex: O(n)  

space complex: O(n)

```
class Solution {
public:
    bool isValid(string s) {
        if(s.size()==0) return true;
        else if(s.size()==1)return false;
        else{
            stack<char>last;
            if(*s.begin()==')'||*s.begin()=='}'||*s.begin()==']') return false;
            else last.push(*s.begin());
            for(auto p = s.begin()+1;p!=s.end();++p){
                if(*p==')'||*p=='}'||*p==']'){
                    if(last.empty()) return false;
                    else{
                        char cTop = last.top(); last.pop();
                        if(cTop=='{' && *p == '}' || cTop=='(' && *p == ')' || cTop=='[' && *p == ']'){}
                        else return false;
                    }
                }
                else last.push(*p); 
            }
            if(last.empty()) return true;
            else return false;
        }
    }
};
```
