# 回溯、DFS

## 0046 全排列

**题目：**[https://leetcode-cn.com/problems/permutations/](https://leetcode-cn.com/problems/permutations/)

**标签：**回溯

### 精选题解

* 回溯算法入门级详解 + 练习（持续更新） 
  * [https://leetcode-cn.com/problems/permutations/solution/hui-su-suan-fa-python-dai-ma-java-dai-ma-by-liweiw/](https://leetcode-cn.com/problems/permutations/solution/hui-su-suan-fa-python-dai-ma-java-dai-ma-by-liweiw/)
* 官方题解
  * [https://leetcode-cn.com/problems/permutations/solution/quan-pai-lie-by-leetcode-solution-2/](https://leetcode-cn.com/problems/permutations/solution/quan-pai-lie-by-leetcode-solution-2/)
* **※ C++ 回溯法/交换法/stl 简洁易懂的全排列**
  * \*\*\*\*[https://leetcode-cn.com/problems/permutations/solution/c-hui-su-fa-jiao-huan-fa-stl-jian-ji-yi-dong-by-sm/](https://leetcode-cn.com/problems/permutations/solution/c-hui-su-fa-jiao-huan-fa-stl-jian-ji-yi-dong-by-sm/)

### 精选代码

* [https://leetcode-cn.com/problems/permutations/solution/quan-pai-lie-by-leetcode-solution-2/532710](https://leetcode-cn.com/problems/permutations/solution/quan-pai-lie-by-leetcode-solution-2/532710)

### 个人提交

#### 方法一：标记数组

{% embed url="https://leetcode-cn.com/submissions/detail/127476452/" %}

{% tabs %}
{% tab title="0046 全排列.cpp" %}
```cpp
/*
* 【46】C++ 回溯法/交换法/stl 简洁易懂的全排列 - 全排列 - 力扣（LeetCode） 
    * https://leetcode-cn.com/problems/permutations/solution/c-hui-su-fa-jiao-huan-fa-stl-jian-ji-yi-dong-by-sm/
*/
class Solution {
public:
    vector<vector<int>> res;

    void backtrack(vector<int> &nums, vector<int> &current, vector<bool> &flags) {
        if (current.size() == flags.size()) {
            res.push_back(current);
        } else {
            for (int i=0; i<nums.size(); ++i) {
                if (not flags[i]) { // nums[i] not in current
                    current.push_back(nums[i]);
                    flags[i] = true;
                    backtrack(nums, current, flags);
                    current.pop_back();
                    flags[i] = false;
                }
            }
        }
    }

    vector<vector<int>> permute(vector<int>& nums) {
        if (nums.empty()) {
            return {};
        }
        vector<bool> flags(nums.size(), false); // true: in current; false: not in current
        vector<int> current;
        backtrack(nums, current, flags);
        return res;
    }
};
```
{% endtab %}
{% endtabs %}

#### 方法二：交换元素

{% embed url="https://leetcode-cn.com/submissions/detail/127482585/" %}

{% tabs %}
{% tab title="0046 全排列 - swap" %}
```cpp
/*
* 【46】C++ 回溯法/交换法/stl 简洁易懂的全排列 - 全排列 - 力扣（LeetCode） 
    * https://leetcode-cn.com/problems/permutations/solution/c-hui-su-fa-jiao-huan-fa-stl-jian-ji-yi-dong-by-sm/
* 全排列 - 全排列 - 力扣（LeetCode） 
    * https://leetcode-cn.com/problems/permutations/solution/quan-pai-lie-by-leetcode-solution-2/
*/
class Solution {
public:
    vector<vector<int>> res;

    void backtrack(vector<int> &nums, int start, int end) {
        if (start == end) {
            res.push_back(nums);
        } else {
            for (int i=start; i<=end; ++i) {
                swap(nums[i], nums[start]);
                backtrack(nums, start+1, end);
                swap(nums[i], nums[start]);
            }
        }
    }


    vector<vector<int>> permute(vector<int>& nums) {
        if (nums.empty()) {
            return {};
        } else {
            backtrack(nums, 0, nums.size()-1);
            return res;
        }
    }
};
```
{% endtab %}
{% endtabs %}



