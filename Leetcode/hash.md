# Hash

- 两数之和<br>
  >在遍历的同时，记录一些信息，以省去一层循环，这是“以空间换时间”的想法<br>
  需要记录已遍历过的数值和它对应的下标，可以借助**查找表**实现<br>
  **查找表**有两个常用的实现：
  > - 哈希表
  > - AVL树
  
  ```
    /*
    思路：
    将元素存入哈希表中，遍历数组，查看target - nums[i]是否存在哈希表中如果是,则返回
    */
    import java.util.HashMap;
    import java.util.Map;

    class Solution {
        public int[] twoSum(int[] nums, int target) {
            int len = nums.length;
            //创建hash表，长度为len-1是因为最后一个元素不需要放入表中
            Map<Integer, Integer> hashMap = new HashMap<>(len-1);
            hashMap.put(nums[0] , 0);
            for(int i = 1; i < len; i++){
                int another = target - nums[i];
                // 比对hash表中元素和another
                if(hashMap.containsKey(another)){
                    return new int[]{i , hashMap.get(another)};
                }
                hashMap.put(nums[i],i);
            }
            //异常处理
            throw new IllegalArgumentException("No two sum solution");
        }
    }
  ```

- 字母异位词分组<br>
  >模式识别：一旦需要根据特征进行归类，使用HashMap<br>

  ```
    /*
    思路
    1.字母排序，字母顺序排序的字符串是值，字母不同排序是键
    */

    import java.util.HashMap;
    import java.util.Map;
    import java.util.ArrayList;

    class Solution {
        public List<List<String>> groupAnagrams(String[] strs) {
            if(strs.length == 0){
                return new ArrayList();
            }
            
            HashMap<String , List> ans = new HashMap<String, List>();
            for(String s : strs){
                //将字符串按字母顺序排序，作为key
                char[] ca = s.toCharArray();
                Arrays.sort(ca);
                String key = String.valueOf(ca);

                //将当前字符串放入hash表中
                //与hash表中的key比较，若不存在，则创建新的键值对
                if(!ans.containsKey(key)){
                    ans.put(key,new ArrayList());
                }

                ans.get(key).add(s);
            }

            return new ArrayList(ans.values());
        }
    }
  ```
  