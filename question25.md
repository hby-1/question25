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