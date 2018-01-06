# 思路（C）

在数组中找到两个数，a + b = target

step 1：数组排序。

step 2：两个下标i、j，从左以及从右遍历数组，分别为a、b。

step 3: 3.1、若a + b > target，b--
 
        3.2、若a + b < target, i++

step 4: 当a + b == target时，循环结束。

（note：考虑到返回值为两个数组成员的原下标，需要使用额外的n个空间保存原下标。故，空间复杂度为O(N)；时间复杂度为快速排序O(nlogn)。）
