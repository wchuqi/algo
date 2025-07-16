leetcode已完成题目

https://leetcode.cn/problem-list/6uaxYMyj/



参考：

https://algo.itcharge.cn/01_array/01_15_array_two_pointers/#_5-%E5%8F%8C%E6%8C%87%E9%92%88%E6%80%BB%E7%BB%93



https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC







# 常用操作

```java
public static void main(String[] args) {
    // List<Integer> -> new int[]
    List<Integer> integerList = Arrays.asList(1, 2, 3, 4, 5);
    int[] intArray = integerList.stream().mapToInt(Integer::intValue).toArray();
    System.out.println(Arrays.toString(intArray));
    // List<String> -> new String[]
    List<String> list = Arrays.asList("A", "B", "C");
    String[] array = list.stream().toArray(String[]::new);
    System.out.println(Arrays.toString(array));
    // new int[] -> List<Integer>
    int[] intArr = {1, 2, 3};
    List<Integer> intList = Arrays.stream(intArr).boxed().collect(Collectors.toList());
    System.out.println(intList);
}
```



```java
// java.lang.Character

char c = 'a';
System.out.println(Character.isLetter(c)); // 判断是否是字母（A-Z, a-z）
System.out.println(Character.isDigit(c)); // 判断是否是数字（0-9）
System.out.println(Character.isWhitespace(c)); // 判断是否是空白字符（空格、换行、制表符等）
System.out.println(Character.isLetterOrDigit(c)); // 是否是字母或数字

System.out.println(Character.isUpperCase(c)); // 是否是大写字母
System.out.println(Character.isLowerCase(c)); // 是否是小写字母

System.out.println(Character.toLowerCase(c)); // 将大写字符转为小写
System.out.println(Character.toUpperCase(c)); // 将小写字符转为大写

char x = '1';
char y = 'a';
/*
比较两个字符的 Unicode 值大小
返回值 < 0 表示 x < y
返回值 == 0 表示 x == y
返回值 > 0 表示 x > y
*/
System.out.println(Character.compare(x, y));

Character obj = '7';
System.out.println(obj.charValue()); // 7 获取封装的 char 值（用于对象）
System.out.println(Character.getNumericValue('A')); // 10 获取字符对应的数值（如 '5' → 5，'A' → 10（十六进制））

System.out.println(Character.toString('A')); // 返回指定字符的字符串形式
System.out.println(Character.digit('A', 10)); // 在指定进制下返回字符对应的数值
System.out.println(Character.forDigit('A', 10)); // 返回指定进制下对应数字的字符表示
```



# 二分查找

**有序**数组查找特定元素

**减而治之**



基本用法

```java
int binary_search(int[] nums, int target) {
    int left = 0, right = nums.length - 1; 
    while(left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1; 
        } else if(nums[mid] == target) {
            // 直接返回
            return mid;
        }
    }
    // 直接返回
    return -1;
}

int left_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，锁定左侧边界
            right = mid - 1;
        }
    }
    // 最后要检查 left 越界的情况
    if (left >= nums.length || nums[left] != target)
        return -1;
    return left;
}


int right_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，锁定右侧边界
            left = mid + 1;
        }
    }
    // 最后要检查 right 越界的情况
    if (right < 0 || nums[right] != target)
        return -1;
    return right;
}

作者：labuladong
链接：https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/solutions/13230/er-fen-cha-zhao-suan-fa-xi-jie-xiang-jie-by-labula/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```





# 数组

## 双指针

时间复杂度一般是`O(n)`，最大是`O(n^2)`

### 对撞指针（方向相反）

![对撞指针](https://qcdn.itcharge.cn/images/202405092155032.png)

```python
left, right = 0, len(nums) - 1

while left < right:
    if 满足要求的特殊条件:
        return 符合条件的值 
    elif 一定条件 1:
        left += 1
    elif 一定条件 2:
        right -= 1

return 没找到 或 找到对应值
```



适用问题：

1、查找有序数组中满足某些条件的元素

2、字符串反转问题



https://leetcode.cn/problems/two-sum-ii-input-array-is-sorted/description/

从一个有序数组中找到等于target的2个数的下标

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;
        while (left < right) {
            if (numbers[left] + numbers[right] > target) {
                right--;
            } else if (numbers[left] + numbers[right] < target) {
                left++;
            } else {
                break;
            }
        }
        return new int[]{left + 1, right + 1};
    }
}
```



https://leetcode.cn/problems/valid-palindrome/description/

验证字符串是个回文串

```java
public boolean isPalindrome(String s) {
    int left = 0;
    int right = s.length() - 1;
    while (left < right) {
        if (!check(s.charAt(left))) {
            left++;
        } else if (!check(s.charAt(right))) {
            right--;
        } else if (String.valueOf(s.charAt(left)).equalsIgnoreCase(String.valueOf(s.charAt(right)))) {
            left++;
            right--;
        } else {
            return false;
        }
    }
    return true;
}
private boolean check(char c) {
    return Character.isAlphabetic(c) || Character.isDigit(c);
}
```



https://leetcode.cn/problems/container-with-most-water/description/

盛最多水的容器

```java
public int maxArea(int[] height) {
    int left = 0;
    int right = height.length - 1;
    int res = 0;
    while (left < right) {
        res = Math.max(res, Math.min(height[left], height[right]) * (right - left));
        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }
    return res;
}
```



### 快慢指针（方向相同）



### 分离指针（分属不同结构）

​				

​		

 

