```c++
class Solution {
public:
    string convert(string s, int numRows) {
        if (numRows == 1)
            return s;

        if (s.length() < 2)
            return s;

        int total = 2 * (numRows - 1);

        string result = "";
        for (int i = 0; i < numRows; i++) {
            int current = 0;
            while (current + i < s.size()) {
                result += s[current + i];
                if (i != 0 && i != numRows - 1 && current + total - i < s.size())
                    result += s[current + total - i];
                current += total;
            }
        }
        return result;
    }
};
```

