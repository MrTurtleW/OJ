```c++
#include<iostream>
#include<vector>

using namespace std;

class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0)
            return false;

        vector<char> vec;

        while (x != 0) {
            vec.push_back(x % 10);
            x /= 10;
        }
        
        int i = 0;
        while (i < vec.size() / 2) {
            if (vec[i] != vec[vec.size() - 1 - i])
                return false;
            i++;
        }
        return true;
    }
};

int main() {
    Solution solution;
    cout << solution.isPalindrome(1231) << endl;
}
```

# 比较数字的一半

```c++
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0)
            return false;
        
        if (x != 0 and x % 10 == 0)
            return false;

        int rev = 0;
        while (x > rev) {
            rev = rev * 10 + x % 10;
            x = x / 10;
        }

        return x == rev || x == rev / 10;
        
    }
};
```

