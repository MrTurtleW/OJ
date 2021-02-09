```c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if (strs.size() == 0)
            return "";
        int index = 0;
        while (true) {
            if (helper(strs, index))
                index++;
            else
                break;
        }
        return strs[0].substr(0, index);
    }
    bool helper(vector<string>& strs, int index) {
        for (string s : strs) {
            if (index < s.size() && s[index] == strs[0][index])
                continue;
            return false;
        }
        return true;
    }
};
```

```c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if (strs.size() == 0)
            return "";

        size_t index = 0;
        while (true) {
            if (strs[0].length() <= index)
                return strs[0].substr(0, index);

            for (string s : strs) {
                if (s.size() <= index || s[index] != strs[0][index])
                    return strs[0].substr(0, index);
            }
            index++;
        }
    }
};
```

