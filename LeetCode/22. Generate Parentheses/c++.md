```c++
#include<iostream>
#include<vector>

using namespace std;

class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> vec;

        helper(vec, "", n, 0, 0);
        return vec;
    }

    void helper(vector<string>& vec, string s, int n, int left, int right) {
        if (right == n) {
            vec.push_back(s);
            return;
        }

        if (left < n) {
            helper(vec, s + "(", n, left + 1, right);
        }
        if (right < left) {
            helper(vec, s + ")", n, left, right + 1);
        }
    }
};

int main() {
    Solution solution;
    for (string s : solution.generateParenthesis(1)) {
        cout << s << endl;
    }
```

