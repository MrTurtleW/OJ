```c++
class Solution {
public:
    int divide(int A, int B) {
        if (A == INT_MIN && B == -1)
            return INT_MAX;

        unsigned int a = abs(A);
        unsigned int b = abs(B);
        unsigned int res = 0;

        for (int x = 31; x >= 0; x--) {
            if ((a >> x) >= b) {
                a -= (b << x);
                res += (1 << x);
            }
        }

        return (A > 0) == (B > 0) ? res : -res;
    }
};

```

