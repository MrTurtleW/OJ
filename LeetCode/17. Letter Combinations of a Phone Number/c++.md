```c++
#include<iostream>
#include<vector>
#include<map>

using namespace std;

class Solution {
public:
    vector<string> letterCombinations(string digits) {
        vector<string> result;
        if (digits.size() == 0)
            return result;

        helper(&result, "", digits);
        return result;
    }

    void helper(vector<string> *result, string part, string digits){
        if (digits.size() == 0) {
            result->push_back(part);
            return;
        }

        map<char, vector<char>>::iterator it = m.find(digits[0]);
        for (char c : it->second) {
            helper(result, part + c, digits.substr(1));
        }
    }

private:
    map<char, vector<char>> m = {
            {'2', {'a', 'b', 'c'}},
            {'3', {'d', 'e', 'f'}},
            {'4', {'g', 'h', 'i'}},
            {'5', {'j', 'k', 'l'}},
            {'6', {'m', 'n', 'o'}},
            {'7', {'p', 'q', 'r', 's'}},
            {'8', {'t', 'u', 'v'}},
            {'9', {'w', 'x', 'y', 'z'}}
    };
};

int main() {
    Solution solution;
    for (string s : solution.letterCombinations("")) {
        cout << s << endl;
    }
}
```

