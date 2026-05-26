1. 两数之和
  	 ① 核心思想：使用Map保存数组中的元素和对应的索引下标：key为数组元素，value为索引下标：
          1. key保存数组的元素：因为需要判断target-nums[i]是否存在
          2. value：因为题目要求返回数组的索引，因此value保存索引下标

     ② 代码理解：若map包含target-nums[i]，则返回，否则使用map保存nums[i]，及其索引下标

     ③ 易错点：不能先将nums[i]和对应的索引i保存至map中，否则会出现错误：[3, 3]，target = 6，返回[0, 0]，因为map的key唯一，所以map只保存了(3, 0)

167. 两数之和 II 
     ① 核心思想：第二题使用双指针的左右指针


# Solution | 1

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; ++i) {
            if (map.containsKey(target - nums[i])) {
                return new int[]{i, map.get(target - nums[i])};
            }
            map.put(nums[i], i);
        }

        return null;
    }
}
```

# Solution | 167

去重思想类似leetcode209

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int i = 0;
        int j = numbers.length - 1;

        while (i < j) {
            if (target == numbers[i] + numbers[j]) {
                return new int[]{i + 1, j + 1}; // 根据题意，下标从1开始，因此结果需要+1
            } else if (target > numbers[i] + numbers[j]) {
                ++i;
            } else {
                --j;
            }
        }

        return null;
    }
}
```