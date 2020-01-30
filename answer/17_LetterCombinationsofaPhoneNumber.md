Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

Note:

Although the above answer is in lexicographical order, your answer could be in any order you want.

Example:

Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].

source:LeetCode https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number

***

Consider the question as convert decimal to quanternary, discuss all situations

time complex: O(4^n*n)  

space complex: O(3^n)

```
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        vector<string> result;
        if(digits.size()<1) return result;
        for(int i = 0;i<pow(4,digits.size());++i){
            string temp = "";
            bool bInsert = true;
            for(int j = 0; j< digits.size(); ++j){
                if(digits[j]=='1') break;
                else if(digits[j] == '7')
                    temp += ('a'+ (digits[j]-'2')*4)+(i/(int)pow(4,j))%4-(digits[j]-'0')+2;
                else if( digits[j]=='9')
                    temp += ('a'+ (digits[j]-'2')*4)+(i/(int)pow(4,j))%4-(digits[j]-'0')+3;
                else{
                    int reminder = (i/(int)pow(4,j))%4;
                    if(reminder>2) {
                        bInsert = false;
                        break;}
                    else if(digits[j] == '8')
                    temp += ('a'+ (digits[j]-'2')*4) + reminder - (digits[j]-'0')+3;
                    else temp += ('a'+ (digits[j]-'2')*4) + reminder - (digits[j]-'0')+2;
                } 
            }
            if(bInsert) result.push_back(temp);
        }
        return result;
    }
};

```
***
BFS

time complex: O(3^i*4^j) (j:when consider 7 and 9, i+j=n)

space complex: O(3^n)
```
class Solution {
public:
    vector<string> bfs(const vector<string>& inputStrings, string digits ){
        unordered_map<char, string> map = { {'2',"abc" },{'3',"def"},{'4',"ghi"},{'5',"jkl"},{'6',"mno"},{'7',"pqrs"},{'8',"tuv"},{'9',"wxyz"} };
        if(digits.size()==0) return inputStrings;
        else {
            vector<string> result;
            string digitalToString = map[digits[0]];
            if(inputStrings.size()==0){
                for(int i=0;i<digitalToString.size();++i){
                    result.push_back(digitalToString.substr(i,1));
                }
                if(digits.size()>1)
                    return bfs(result,digits.substr(1));
                else
                    return result;
            }
            else{
                for(int i=0;i<digitalToString.size();++i){
                    for(int j=0;j<inputStrings.size();++j){
                        result.push_back(inputStrings[j]+digitalToString.substr(i,1));
                    }
                }
                if(digits.size()>1)
                    return bfs(result,digits.substr(1));
                else
                    return result;
            }
        }


    }
    vector<string> letterCombinations(string digits) {
        vector<string> inputStrings;
        return bfs(inputStrings, digits);
    }

};
```