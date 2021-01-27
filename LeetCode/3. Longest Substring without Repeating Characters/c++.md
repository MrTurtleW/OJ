# 暴力破解 超时

```c++
#include<iostream>
#include<set>

using namespace std;

class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if (s.size() < 2) {
            return s.size();
        }

        size_t maxLength = 0;

        for (size_t i = 0; i < s.size(); i++) {
            for (size_t j = i + 1; j <= s.size(); j++) {
                if (!checkRepeat(s, i, j) && maxLength < j - i) {
                    maxLength = j - i;
                }
            }
        }
        return maxLength;
    }

    /*
     * 判断一个子串是否有重复
    */
    bool checkRepeat(const string &s, const size_t i, const size_t j) {
        set<char> _set;

        for (size_t cur = i; cur < j; cur++) {
            if (_set.find(s[cur]) != _set.end()) {
                return true;
            }
            _set.insert(s[cur]);
        }
        return false;
    }
};

int main() {
    Solution solution;
    cout << solution.lengthOfLongestSubstring("au") << endl;
}
```

# 滑动窗口 44ms

如果`s[i,j]` 不包含重复字符，那么只需要确认`s[i,j]`是否包含`s[j+1]`

```c++
#include<iostream>
#include<set>

using namespace std;

class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        size_t n = s.length();
        set<char> _set;

        size_t ans = 0, i = 0, j = 0;
        while (i < n && j < n) {
            if (_set.find(s[j]) == _set.end()) {
                _set.insert(s[j++]);
                ans = max(ans, j - i);
            }
            else {
                _set.erase(s[i++]);
            }
        }

        return ans;
    }
};

int main() {
    Solution solution;
    cout << solution.lengthOfLongestSubstring("") << endl;
}
```

# 优化的滑动窗口 16ms

使用map来保存字符和对应下标

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        size_t n = s.length(), ans = 0;
        map<char, size_t> _map;
        for (size_t j = 0, i = 0; j < n; j++) {
            map<char, size_t>::iterator iter = _map.find(s[j]);
            if (iter != _map.end()) {
                i = max(iter -> second, i);
            }
            ans = max(ans, j - i + 1);
            _map[s[j]] = j + 1;
        }
        return ans;
    }
};
```

# 使用数组 0ms

如果只是ascii码，则使用数组更快

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> dict(256, -1);
        int maxLen = 0, start = -1;
        for (int i = 0; i != s.length(); i++) {
            if (dict[s[i]] > start)
                start = dict[s[i]];
            dict[s[i]] = i;
            maxLen = max(maxLen, i - start);
        }
        return maxLen;
    }
};
```

