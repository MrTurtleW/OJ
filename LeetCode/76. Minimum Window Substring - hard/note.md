For most substring problem, we are given a string and find a substring of it which satisfy some restrictions. A general way is to use a hashmap assisted with two pointers. The template given below.

```c++
int findSubstring(string s){
        vector<int> map(128,0);
        int counter; // check whether the substring is valid
        int begin=0, end=0; //two pointers, one point to tail and one  head
        int d; //the length of substring

        for() { /* initialize the hash map here */ }

        while(end<s.size()){

            if(map[s[end++]]-- ?){  /* modify counter here */ }

            while(/* counter condition */){ 
                 
                 /* update d here if finding minimum*/

                //increase begin to make it invalid/valid again
                
                if(map[s[begin++]]++ ?){ /*modify counter here*/ }
            }  

            /* update d here if finding maximum*/
        }
        return d;
  }
```

- [Longest substring with at most two Distinct characters.](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)

- [Longest substring without repeating characters.](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

  - 159

  ```c++
  int lengthOfLongestSubstringTwoDistinct(string s) {
      vector<int> map(128, 0);
      int counter=0, begin=0, end=0, d=0; 
      while(end<s.size()){
          if(map[s[end++]]++==0) counter++;
          while(counter>2) if(map[s[begin++]]--==1) counter--;
          d=max(d, end-begin);
      }
      return d;
  }
  ```

  