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

- 接雨水
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