### 题意
**中文描述**  
给定一个数列 S ，包含 n 个整数.在 S 中找到四个元素 a, b, c, d 使得 a + b + c + d = target . 找到所有的独特的满足上述条件的四元组.  
注意: 结果集包含的四元组不重复.  

### 题解
**算法及复杂度(45 ms)**  
本题与第 15 题 ([3Sum](https://leetcode.com/problems/3sum/#/description)) 比较类似，第 15 题是求三个数的和，本题是求四个数的和.建议先去练习第 15 题.  
首先，为了避免结果的重复，先对数列进行排序.依照在 15 题中提到的: **在一段数列上找到和为固定值的两个数的复杂度可以为 O(n)**.于是，很简单的思路是: 先固定前两个数 nums[l1], nums[l2]（使用两重循环），这样后两个数的和是固定的 `target - nums[l1] - nums[l2]` ，只需要在 `(l2, len)` 上进行和为固定值的两个数的寻找就可以了.  
需要注意的是: 在算法运行过程中注意保证求出的结果不重复，控制方法参考AC代码。其实可以看出，即使求出的结果重复也可以在求出所有的结果后很容易找出所有不重复的结果,原因是根据求出的四元组的有序性。  
在实现过程中，在一段数列上找到和为固定值的两个数直接使用了第 15 题中的 twoSum 函数。  
***时间复杂度:*** O(n ^ 3) . n 是数列的长度的, 排序时间复杂度为 O(nlogn) , 求解过程中:前两个数两重循环复杂度为 O(n ^ 2) , 后两个数查找过程复杂度为 O(n) , 总的时间复杂度为 `O(nlogn) + O(n ^ 2) * O(n)` , 即 O(n ^ 3) .  
***代码参见同文件夹solution.cpp***  

### 算法正确性
**正确性证明**  
算法的正确性等同于枚举的正确性。  
**举个例子**  
    
    ```
    // 给定数列和target
    nums = [1,0,-1,0,-2,2]
    target = 0
    
    //排序数列
    nums = [-2, -1, 0, 0, 1, 2]
    
    //i = 0, j = 1, l = 2, r = 5
    nums[i] + num[j] + num[l] + num[r] = -1 < target, l ++
    
    //i = 0, j = 1, l = 3, r = 5
    nums[i] + num[j] + num[l] + num[r] = -1 < target, l ++
    
    //i = 0, j = 1, l = 4, r = 5
    nums[i] + num[j] + num[l] + num[r] = 0 == target, l ++ , r--, 此时l !< r ,因此 j ++
    
    之后的步骤和之前类似
    ```
