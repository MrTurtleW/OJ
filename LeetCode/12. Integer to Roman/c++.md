```c++
class Solution {
public:
    string intToRoman(int num) {
        string result;
        while (num > 0) {
            pair<int, string>* p = getPair(num);
            result += p->second;
            num -= p->first;
        }
        return result;
    }

    pair<int, string>* getPair(int num) {
        for (pair<int, string> p : vec) {
            if (p.first <= num) {
                return &p;
            }
        }
        return nullptr;
    }

private:
    vector<pair<int, string>> vec = {
            {1000, "M"}, {900, "CM"}, {500, "D"}, {400, "CD"},
            {100, "C"}, {90, "XC"}, {50, "L"}, {40, "XL"},
            {10, "X"}, {9, "IX"}, {5, "V"}, {4, "IV"}, {1, "I"},
    };
};
```

