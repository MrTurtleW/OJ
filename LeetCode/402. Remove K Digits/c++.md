```c++
class Solution {
public:
    string removeKdigits(string num, int k) {
        stack<char> s;

        for (char c : num) {
            while (!s.empty() && s.top() > c && k > 0) {
                s.pop();
                k--;
            }
            s.push(c);
        }



        string result;
        while (!s.empty()) {
            result = s.top() + result;
            s.pop();
        }
        int index = 0;

        result = result.substr(0, result.size() - k);
        if (result == "")
            result = "0";
        while (result[index] == '0' and index < result.size()-1)
            index++;
        result = result.substr(index);
        return result;
    }
};
```

题解：

```c++
class Solution {
public:
    string removeKdigits(string num, int k) {
       string ans = "";                                         // treat ans as a stack in below for loop
       
       for (char c : num) {
           while (ans.length() && ans.back() > c && k) {
               ans.pop_back();                                  // make sure digits in ans are in ascending order
               k--;                                             // remove one char
           }
           
           if (ans.length() || c != '0') { ans.push_back(c); }  // can't have leading '0'
       }
       
       while (ans.length() && k--) { ans.pop_back(); }          // make sure remove k digits in total
       
       return ans.empty() ? "0" : ans;
	}
};
```

