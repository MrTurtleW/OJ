```c++
class Solution {
public:
    vector<int> findSubstring(string s, vector<string>& words) {
        map<string, int> count;
        vector<int> res;

        for (string word: words)
        {
            count[word]++;
        }

        int wordLength = words[0].size(), numOfWords = words.size();
        if (s.size() < wordLength * numOfWords)
            return res;
        for (int i=0; i<= s.size() - wordLength * numOfWords; i++)
        {
            map<string, int> seen;
            for (int j=0; j< numOfWords; j++)
            {
                string subStr = s.substr(i + j * wordLength, wordLength);

                if (subStr.empty())
                    break;

                auto it = count.find(subStr);
                if (it == count.end())
                    break;

                seen[subStr]++;

                if (seen[subStr] > count[subStr])
                    break;

                if (j == numOfWords - 1)
                    res.push_back(i);
            }
        }
        return res;
    }
};
```

