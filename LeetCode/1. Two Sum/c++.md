```c++
#include<iostream>
#include<vector>
#include<map>

using namespace std;

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int, int> nums_map;
        // 保存两个数
        vector<int> result;

        for (int i = 0; i < nums.size(); i++) {
            nums_map[nums[i]] = i;
        }

        for (int i = 0; i < nums.size(); i++) {
            int value = target - nums[i];
            if (nums_map.find(value) != nums_map.end() && nums_map[value] != i) {
                result.push_back(i);
                result.push_back(nums_map[value]);
                break;
            }
        }
        return result;
    }
};
```

