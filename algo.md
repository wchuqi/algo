# 常用操作

```java
isLetter(char ch)
判断是否是字母（A-Z, a-z）
isDigit(char ch)
判断是否是数字（0-9）
isWhitespace(char ch)
判断是否是空白字符（空格、换行、制表符等）
isLetterOrDigit(char ch)
是否是字母或数字

isUpperCase(char ch)
是否是大写字母
isLowerCase(char ch)
是否是小写字母

toLowerCase(char ch)
将大写字符转为小写
toUpperCase(char ch)
将小写字符转为大写

compare(char x, char y)
比较两个字符的 Unicode 值大小
返回值 < 0 表示 x < y
返回值 == 0 表示 x == y
返回值 > 0 表示 x > y
    
charValue()
获取封装的 char 值（用于对象）
getNumericValue(char ch)
获取字符对应的数值（如 '5' → 5，'A' → 10（十六进制））
eg:
Character obj = '7';
System.out.println("charValue()：" + obj.charValue()); // 7
char hexChar = 'F';
System.out.println("getNumericValue('F')：" + Character.getNumericValue(hexChar)); // 15

toString(char c)
返回指定字符的字符串形式
digit(int codePoint, int radix)
在指定进制下返回字符对应的数值
forDigit(int digit, int radix)
返回指定进制下对应数字的字符表示
eg:
System.out.println("toString('X')：" + Character.toString('X')); // "X"
int value = Character.digit('A', 16);
System.out.println("digit('A', 16)：" + value); // 10
char hex = Character.forDigit(12, 16);
System.out.println("forDigit(12, 16)：" + hex); // 'c'
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





### 快慢指针（方向相同）



### 分离指针（分属不同结构）





 

