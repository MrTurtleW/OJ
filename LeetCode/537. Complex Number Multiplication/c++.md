```c++
#include<iostream>
#include<string>

using namespace std;

struct Complex {
    int real;
    int imaginary;

    static Complex str2complex(string num) {
        Complex complex;
        auto add_sig = num.find('+');
        if (add_sig == num.npos) {
            complex.real = atoi(num.c_str());
            complex.imaginary = 0;
        }
        else {
            complex.real = atoi(num.substr(0, add_sig).c_str());
            complex.imaginary = atoi(num.substr(add_sig + 1, num.size() - add_sig - 1).c_str());
        }
        return complex;
    }
};

class Solution {
public:
    string complexNumberMultiply(string num1, string num2) {
        Complex complex1 = Complex::str2complex(num1);
        Complex complex2 = Complex::str2complex(num2);

        int real = complex1.real * complex2.real - complex1.imaginary * complex2.imaginary;
        int imaginary = complex1.real * complex2.imaginary + complex1.imaginary * complex2.real;

        return to_string(real) + "+" + to_string(imaginary) + "i";
    }
};

int main() {
    Solution solution;
    cout << solution.complexNumberMultiply("1+1i", "1+1i");
    system("pause");
}
```

