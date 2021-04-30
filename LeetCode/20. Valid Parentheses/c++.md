```c++
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        map<char, char> m = {
            {'(', ')'},
            {'[', ']'},
            {'{', '}'}
        };

        for (char c : s) {
            if (!st.empty() && st.top() == c)
                st.pop();
            else {
                st.push(m[c]);
            }
        }

        return st.empty();

    }
};
```

