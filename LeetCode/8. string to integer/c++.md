```c++
class Solution {
public:
    int myAtoi(string s) {
        int index = 0;
        int res = 0;
        bool positive = true;
        // ignore white space
        while (s[index] == ' ')
            index++;

        if (s[index] == '+')
            index++;
        else if (s[index] == '-') {
            index++;
            positive = false;
        }

        while ('0' <= s[index] && s[index] <= '9') {
            int current = s[index] - '0';

            if (res > INT_MAX / 10 || (res == INT_MAX / 10 && ((positive && current >= 7) || (!positive && current >= 8)))) {
                if (positive)
                    return INT_MAX;
                else
                    return INT_MIN;
            }
            res = res * 10 + current;
            index++;
        }

        return positive ? res : -res;
    }
};
```

