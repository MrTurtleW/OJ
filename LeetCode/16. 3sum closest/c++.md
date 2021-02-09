```c++
#include<iostream>
#include<vector>
#include<algorithm>

using namespace std;

class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());

        int res = nums[0] + nums[1] + nums[nums.size() - 1];

        for (int k = 0; k < nums.size() - 2; k++) {
            for (int i = k + 1, j = nums.size() - 1; i < j;) {
                int temp = nums[k] + nums[i] + nums[j];

                if (temp < target) {
                    i++;
                }
                else if (temp > target)
                    j--;
                else
                    return temp;

                if (abs(temp - target) < abs(res - target))
                    res = temp;
            }
        }
        return res;
    }
};
```

