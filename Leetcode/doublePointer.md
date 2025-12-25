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