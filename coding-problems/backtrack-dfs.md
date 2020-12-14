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

## 0047 全排列 II

题目：[https://leetcode-cn.com/problems/permutations-ii/](https://leetcode-cn.com/problems/permutations-ii/)

标签：回溯

### 精选题解

* 官方题解
  * [https://leetcode-cn.com/problems/permutations-ii/solution/quan-pai-lie-ii-by-leetcode-solution/](https://leetcode-cn.com/problems/permutations-ii/solution/quan-pai-lie-ii-by-leetcode-solution/)

### 关键思路

要解决重复问题，只需保证在填第 i 个数时，重复数字只被填入一次。方法：**对原数组排序，保证相同数字都相邻，然后每次填入的数一定是这个数所在重复数集合中「从左往右第一个未被填过的数字」**，即如下的判断条件：

```cpp
if (i > 0 && nums[i] == nums[i - 1] && !vis[i - 1]) {
    continue;
}
```

假如排完序后的完整数组 nums 中有三个连续的数，那么一定只有如下 4 种状态：\[×, ×, ×\]，\[√, ×, ×\]，\[√, √, ×\]，\[√, √, √\]。（√ 表示已在生成的数组中，× 表示未在生成的数组中。）

### 复杂度

时间复杂度：O\(n\*n!\)。回溯复杂度 O\(n!\)；每次新的生成数组需要复制 n 个元素。

空间复杂度：SO\(n\)。长度为 n 的标记数组；递归时深度最大为 n。

详见官方题解。

