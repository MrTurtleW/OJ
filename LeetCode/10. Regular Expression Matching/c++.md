```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        if (p.size() == 0)
            return s.size() == 0;

        bool match = s.size() > 0 && (s[0] == p[0] || p[0] == '.');
        if (p.size() > 1 && p[1] == '*')
            return isMatch(s, p.substr(2, p.size() - 2)) || match && isMatch(s.substr(1, s.size() - 1), p);
        else
            return match && isMatch(s.substr(1, s.size() - 1), p.substr(1, p.size() - 1));
    }
};
```

# DP

```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.size();
        const int n = p.size();

        // M[i][j] represents if the 1st i characters in s can match the 1st j characters in p
        vector<vector<bool>> M;

        for (int i = 0; i < m+1; i++) {
            vector<bool> vec;
            for (int j = 0; j < n+1; j++) {
                vec.push_back(false);
            }
            M.push_back(vec);
        }

        // empty string match empty pattern
        M[0][0] = true;

        // M[i][0] = false, since empty pattern cannot match non-empty string

        // what pattern matches empty string ""? It should be #*#*#*
        // the length of ther pattern should be even and the character at the even position should be *
        // the length of repeat sub-pattern #* is only 2, we can just make use of M[0][j-2]
        for (int j = 2; j < n + 1; j += 2) {
            if (p[j - 1] == '*' && M[0][j - 2])
                M[0][j] = true;
        }

        for (int i = 1; i < m + 1; i++) {
            for (int j = 1; j < n + 1; j++) {
                char curS = s[i - 1];
                char curP = p[j - 1];

                if (curS == curP || curP == '.')
                    M[i][j] = M[i - 1][j - 1];
                else if (curP == '*') {
                    char preCurP = p[j - 2];
                    if (preCurP != '.' && preCurP != curS)
                        // empty
                        M[i][j] = M[i][j - 2];
                    else
                        // empty || single || multiple
                        M[i][j] = M[i][j - 2] || M[i - 1][j - 2] || M[i - 1][j];
                }
            }
        }

        return M[m][n];
    }
};

```

