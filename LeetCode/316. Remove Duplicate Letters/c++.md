贪心

```c++
class Solution {
public:
    string removeDuplicateLetters(string s) {
        if (s.size() == 0)
            return "";

        int count[26] = { 0 };

        for (int i = 0; i < s.size(); i++) {
            count[s[i] - 'a'] ++;
        }

        int pos = 0;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] < s[pos])
                pos = i;

            if (--count[s[i] - 'a'] == 0)
                break;
        }

        char c = s[pos];
        s = s.substr(pos + 1);
        s.erase(remove(s.begin(), s.end(), c), s.end());
        return c + removeDuplicateLetters(s);
    }
};
```

