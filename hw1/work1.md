# 软件工程 第一周作业
## 学号：41911241
## 姓名：檀永正
# 二分搜索算法
![二分搜索图解](https://pic2.zhimg.com/v2-85aec23a60b2a7dc66a2a8454d4302fc_1440w.jpg?source=172ae18b)

## 一、前提条件
*有序数组*
## 二、解决问题
**在有序数组中查找一个数，如果存在返回其下标**
## 三、解决思路
***双指针left和right，分别指向有序数组的头和尾，设置middle存储start和end的均值与需要查找的数组比较。***
~~sos~~
## 四、常见问题
### 寻找一个数（基本的二分搜索）
```java
int binarySearch(int[] nums, int target) {
    int left = 0; 
    int right = nums.length - 1; // 注意

    while(left <= right) { // 注意
        int mid = (right + left) / 2;
        if(nums[mid] == target)
            return mid; 
        else if (nums[mid] < target)
            left = mid + 1; // 注意
        else if (nums[mid] > target)
            right = mid - 1; // 注意
        }
    return -1;
}
```
因为我们初始化 right = nums.length - 1  
所以决定了我们的「搜索区间」是 [left, right]  
所以决定了 while (left <= right)  
同时也决定了 left = mid+1 和 right = mid-1  
因为我们只需找到一个 target 的索引即可 
所以当 nums[mid] == target 时可以立即返回
### 寻找左侧边界的二分搜索
```java
int left_bound(int[] nums, int target) {
    if (nums.length == 0) return -1;
    int left = 0;
    int right = nums.length; // 注意

    while (left < right) { // 注意
        int mid = (left + right) / 2;
        if (nums[mid] == target) {
            right = mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid; // 注意
        }
    }
    return left;
}
```
因为我们初始化 right = nums.length  
所以决定了我们的「搜索区间」是 [left, right)  
所以决定了 while (left < right)  
同时也决定了 left = mid+1 和 right = mid
因为我们需找到 target 的最左侧索引  
所以当 nums[mid] == target 时不要立即返回  
而要收紧右侧边界以锁定左侧边界
### 寻找右侧边界的二分查找
```java
int right_bound(int[] nums, int target) {
    if (nums.length == 0) return -1;
    int left = 0, right = nums.length;

    while (left < right) {
        int mid = (left + right) / 2;
        if (nums[mid] == target) {
            left = mid + 1; // 注意
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid;
        }
    }
    return left - 1; // 注意

```
因为我们初始化 right = nums.length  
所以决定了我们的「搜索区间」是 [left, right)  
所以决定了 while (left < right)  
同时也决定了 left = mid+1 和 right = mid  
因为我们需找到 target 的最右侧索引  
所以当 nums[mid] == target 时不要立即返回  
而要收紧左侧边界以锁定右侧边界  
又因为收紧左侧边界时必须 left = mid + 1  
所以最后无论返回 left 还是 right，必须减一
## 五、参考文献
[详解二分查找方法](https://www.cnblogs.com/kyoner/p/11080078.html)