```c++
#include<iostream>
#include<vector>
#include<algorithm>

using namespace std;

class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> result;

        if (nums.size() < 4)
            return result;

        sort(nums.begin(), nums.end());

        for (int i = 0; i < nums.size() - 3;) {
            for (int j = i + 1; j < nums.size() - 2;) {
                for (int k = j + 1, l = nums.size() - 1; k < l;) {
                    int temp = nums[i] + nums[j] + nums[k] + nums[l];

                    if (temp < target)
                        while (k < l && nums[k++] == nums[k]);
                    else if (temp > target)
                        while (k < l && nums[l--] == nums[l]);
                    else {
                        result.push_back(vector<int>{nums[i], nums[j], nums[k], nums[l]});
                        while (k < l && nums[k++] == nums[k]);
                        while (k < l && nums[l--] == nums[l]);
                    }
                }
                while (j < nums.size() - 2 && nums[j++] == nums[j]);
            }
            while (i < nums.size() - 3 && nums[i++] == nums[i]);
        }

        return result;
    }
};

int main() {
    Solution solution;
    vector<int> nums{ 1,0,-1,0,0, 0, 0, 0, -2,2 };
    for (vector<int> vec : solution.fourSum(nums, 0)) {
        for (int i: vec) {
            cout << i << " ";
        }
        cout << endl;
    }
}
```

