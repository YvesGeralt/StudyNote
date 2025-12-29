# substring

- 和为k的子数组
  > 使用前缀和 + 哈希表的思想来降低时间复杂度<br>
  > `pre[j] - pre[i] = k` ==> `pre[j] - k = pre[i]`
  ```
    import java.util.HashMap;

    class Solution {
        public int subarraySum(int[] nums, int k) {
            int count = 0;
            int pre = 0;

            HashMap<Integer,Integer> map = new HashMap<>();
            map.put(0,1);
            for(int i = 0; i < nums.length; i++){
                pre += nums[i];
                if(map.containsKey(pre - k)){
                    count += map.get(pre - k);
                }
                /**
                    从map中获取键为sum的值（即之前出现过的前缀和为sum的次数），如果sum不存在于map中，则返回默认值0。
                    将这个值加1，表示当前前缀和sum又出现了一次。
                */
                map.put(pre,map.getOrDefault(pre,0) + 1);
            }

            return count;
        }
    }
  ```