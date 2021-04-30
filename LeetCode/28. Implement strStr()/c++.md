```c++
#include<iostream>

using namespace std;

class Solution {
public:
    int strStr(string haystack, string needle)
    {
        if (needle.size() == 0)
            return 0;

        if (haystack.size() < needle.size())
            return -1;

        for (int i = 0; i <= haystack.size() - needle.size(); i++) {
            if (checkMatch(haystack, needle, i))
                return i;
        }
        return -1;
    }

private:
    bool checkMatch(const string &haystack, const string &needle, int index)
    {
        for (int i = 0; i < needle.size(); i++) {
            if (haystack[index + i] != needle[i])
                return false;
        }
        return true;
    }
};

int main()
{
    Solution solution;
    cout << solution.strStr("a", "a");
}
```

