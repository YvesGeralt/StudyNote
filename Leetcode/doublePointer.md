# doublePointer

- 移动零
  >本质是移动非零，使得非零数在数列左边有序
  ```
    /**
        思路：
        定义两个指针，cur遍历元素,i指向第一个非零元素，若nums[cur] != 0 , 交换nums[cur] 和nums[i],
        i++

    */

    class Solution {
        public void moveZeroes(int[] nums) {
            int i = 0;
            for(int cur = 0; cur < nums.length; cur++) {
                if(nums[cur] != 0){
                    int temp = nums[i];
                    nums[i] = nums[cur];
                    nums[cur] = temp;
                    i++;
                }
            }
        }
    }
  ```

- 盛最多水的容器
  > 要试着放弃计算一些明显不用计算的值，来避免嵌套循环
  ```
    /**
        思路：
        两个指针分别指向首尾，不断计算出容积，并收缩较短的边，可以避免计算一定小的容积
    */
    import static java.lang.Math.*;

    class Solution {
        public int maxArea(int[] height) {
            int len = height.length;
            if(len < 2){
                return 0;
            }
            
            int maxVal = 0;
            int i = 0, j = len - 1;
            while(i < j){
                int val = min(height[i], height[j]) * (j - i);
                if(val > maxVal){
                    maxVal = val;
                }
                if(height[i] < height[j]) {
                    i++;
                } else {
                    j--;
                }
            }

            return maxVal;
        }
    }
  ```

- 三数之和
  > 遍历数组判断条件不难，关键在于跳过重复值。可以先将数组排序，则相等的值只可能在该元素前后
  ```
    import java.util.*;

    class Solution {
        public List<List<Integer>> threeSum(int[] nums) {
            List<List<Integer>> result = new ArrayList<>();
            int len = nums.length;

            if(len < 3) return result;

            // 排序
            Arrays.sort(nums);

            // 遍历固定第一个数
            for(int i = 0; i < len - 2; i++) {
                // 跳过重复值
                if(i > 0 && nums[i] == nums[i - 1]) {
                    continue;
                }

                // 双指针查找后两数
                int left = i + 1;
                int right = len - 1;

                while(left < right) {
                    int sum = nums[i] + nums[left] + nums[right];

                    if(sum == 0){
                        result.add(Arrays.asList(nums[i], nums[left], nums[right]));

                        // 跳过重复值
                        while(left < right && nums[left] == nums[left + 1]) left++;
                        while(left < right && nums[right] == nums[right - 1]) right--;

                        left++;
                        right--;
                    } else if (sum < 0) {
                        left++; // 和太小，左指针右移
                    } else {
                        right--; //和太大，右指针左移
                    }
                }

            }

            return result;
        }
    }
  ```
- 接雨水
  > 不要总考虑双指针从一边出发，要考虑双指针从两边同时出发。
  ```
    /**
        思路一：从左边界出发，寻找有=右边界，计算中间积水值
        思路二：从左右边界出发，记录leftMax和rightMax,计算每个元素能积水的最大值
    */

    class Solution {
        public int trap(int[] height) {
            int i = 0;
            int sum = 0;
            int len = height.length;
            
            // 跳过左边为0的起点
            while (i < len && height[i] == 0) {
                i++;
            }
            
            while (i < len - 1) {  // 至少需要两个柱子才能积水
                int j = i + 1;
                int maxIndex = j;  // 记录最大高度的索引
                
                // 寻找右边界：比当前左边界高，或者是最高的
                while (j < len && height[j] < height[i]) {
                    if (height[j] > height[maxIndex]) {
                        maxIndex = j;
                    }
                    j++;
                }
                
                // 情况1：找到了比左边界高的柱子
                if (j < len) {
                    int h = Math.min(height[i], height[j]);
                    int width = j - i - 1;
                    int volume = h * width;
                    
                    for (int k = i + 1; k < j; k++) {
                        volume -= Math.min(height[k], h);  // 减去中间柱子的高度
                    }
                    sum += volume;
                    i = j;
                } 
                // 情况2：没有找到比左边界高的柱子，使用最高的柱子作为右边界
                else if (maxIndex < len) {
                    int h = Math.min(height[i], height[maxIndex]);
                    int width = maxIndex - i - 1;
                    int volume = h * width;
                    
                    for (int k = i + 1; k < maxIndex; k++) {
                        volume -= Math.min(height[k], h);
                    }
                    sum += volume;
                    i = maxIndex;
                } else {
                    i++;  // 没有找到右边界，移动左指针
                }
            }
            
            return sum;
        }
    }
  ```