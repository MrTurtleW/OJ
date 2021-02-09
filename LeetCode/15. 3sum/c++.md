```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> result;
        
        if (nums.size() < 3)
            return result;
        
        sort(nums.begin(), nums.end());
        
        for (int k = 0; k < nums.size() - 2; k++) {
            
            // already sorted
            if (nums[k] > 0)
                break;

            // duplicates
            if (k > 0 && nums[k] == nums[k - 1])
                continue;

            for (int i = k + 1, j = nums.size() - 1; i < j;) {
                int s = nums[i] + nums[j] + nums[k];
                if (s > 0)
                    while (nums[j--] == nums[j] && j > i);
                else if (s < 0)
                    while (nums[i++] == nums[i] && i < j);
                else {
                    result.push_back(vector<int>{nums[i], nums[j], nums[k]});
                    while (nums[j--] == nums[j] && j > i);
                    while (nums[i++] == nums[i] && i < j);
                }
            }
        }

        return result;
    }
};
```

