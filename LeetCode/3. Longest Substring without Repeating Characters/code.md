
# C++

```c++
#include<iostream>
#include<map>
#include<string>

using namespace std;

class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        map<char, int> usedChar;
        int start = 0, maxLength = 0;
        for(int i=0; i<s.length(); i++){
        	if(usedChar.count(s.at(i)) == 1 && start <= usedChar[s.at(i)]){
        		start = usedChar[s.at(i)] + 1;
			}
			else{
				maxLength = max(maxLength, i - start + 1);
			}
			
			usedChar[s.at(i)] = i;
		}
		
		return maxLength;
    }
};

int main(){
	string s;
	Solution *solution = new Solution;
	while(cin >> s){
		cout << solution->lengthOfLongestSubstring(s) << endl;
	}
} 
```

# python
```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        start = result = 0
        for index in  range(len(s)):
            if s[index] in s[start:index]:
                start = start + s[start:index].index(s[index]) + 1
            elif result < index - start + 1:
                result = index - start + 1

        return result
```


```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        start = maxLength = 0
        usedChar = {}
        
        for i in range(len(s)):
            if s[i] in usedChar and start <= usedChar[s[i]]:
                start = usedChar[s[i]] + 1
            else:
                maxLength = max(maxLength, i - start + 1)

            usedChar[s[i]] = i

        return maxLength
```


# java

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> usedChar = new HashMap<>();

        int start = 0, maxLength = 0;

        for (int i=0; i< s.length(); i++) {
            if (usedChar.containsKey(s.charAt(i)) && start <= usedChar.get(s.charAt(i))) {
                start = usedChar.get(s.charAt(i)) + 1;
            }
            else {
                maxLength = Math.max(maxLength, i - start + 1);
            }
            usedChar.put(s.charAt(i), i);
        }

        return maxLength;
    }
}
```