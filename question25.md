# 大于等于顺序前缀和的最小缺失整数

给你一个下标从 **0** 开始的整数数组 `nums` 。

如果一个前缀 `nums[0..i]` 满足对于 `1 <= j <= i` 的所有元素都有 `nums[j] = nums[j - 1] + 1` ，那么我们称这个前缀是一个 顺序前缀 。特殊情况是，只包含 `nums[0]` 的前缀也是一个 顺序前缀 。

请你返回` nums `中没有出现过的 **最小** 整数 `x` ，满足` x `大于等于**最长** 顺序前缀的和。

## 示例一：
>### 输入：
>nums = [1,2,3,4,5]
>### 输出：
>6
>### 解释：
>nums 的最长顺序前缀是 [1,2,3] ，和为 6 ，6 不在数组中，所以 6 是大于等于最长顺序前缀和的最小整数。

## 示例二：
>### 输入：
>nums = [3,4,5,1,12,14,13]
>### 输出：
>15
>### 解释：
>nums 的最长顺序前缀是 [3,4,5] ，和为 12 ，12、13 和 14 都在数组中，但 15 不在，所以 15 是大于等于最长顺序前缀和的最小整数。

## 代码：
1.

    public class Solution {
        public int MissingInteger(int[] nums) {
            int sum = nums[0];
            int n = nums.Length;
            for (int i = 1; i < n && nums[i] - nums[i - 1] == 1; i++) {
                sum += nums[i];
            }
            ISet<int> set = new HashSet<int>();
            foreach (int num in nums) {
                set.Add(num);
            }
            int x = sum;
            while (set.Contains(x)) {
                x++;
            }
            return x;
        }
    }
2.

    public class Solution {
            public int MissingInteger(int[] nums)
            {
                int n = nums.Length, sum = nums[0], i = 1;

                // 寻找最长顺序前缀和
                for (; i < n; ++i)
                {
                    if (nums[i] - nums[i - 1] == 1) sum += nums[i];
                    else break;
                }

                // 数组转set
                HashSet<int> set = new HashSet<int>();
                foreach(var num in nums) set.Add(num);

                // set中寻找x
                while (set.Contains(sum)) sum++;

                return sum;
            }
    }
3.

    public class Solution {
        public int MissingInteger(int[] nums) {
            int max=nums[0];
            int index=0;
            for(int i=1;i<nums.Length;i++){
                if(nums[i]==nums[i-1]+1){
                    max+=nums[i];
                    index+=1;
                }
                else{
                    break;
                }
            }
            int m=nums.Length-index;
            while(m!=0){
                for(int n=index;n<nums.Length;n++){
                    if(nums[n]==max){
                        max++;
                    }
                }
                m--;
            }
            return max;
        }
    }