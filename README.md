题目： Given an array of integers, return indices of the two numbers such that they add up to a specific target. You may assume that each input would have exactly one solution, and you may not use the same element twice. 给定一个整数数组,返回指数他们相加的两个数,这样一个特定的目标。 你可能认为每个输入完全一个解决方案,你可能无法使用相同元素的两倍。 个人想法： 看到题目的时候，想的就是遍历数组元素相加找到和为目标数字的两个元素然后输出下标。遍历的时候就想到了冒泡排序，而这里需要特别注意的是题目中说到了不能使用相同元素的两倍，所以我就没有让元素自身相加判断是否和为目标数字。那么，我一开始陷入的误区是，我以为整个过程都是自己实现，所以纠结于给定数组的读入，后来发现并不需要，要做的只是找到数组中的那两个元素的下标。那么，我最初的代码是这样的 int* twoSum(int* nums, int numsSize, int target) { for(int i = 0;i<numsSize;i++)
{
for(int j = i+1;(j<numsSize && j != i);j++)
{
if(nums[i] + nums[j] == target) return i,j;
}
}
} 运行错误，我想是返回值的用法不对，我就想将i、j分别赋给两个变量a、b，但是是RuntimeError，我想是定义两个变量没有必要，我就换用数组，将i、j给一个数组中的两个元素，然后返回这个数组，但是依然超时。这时候，我仔细审视了代码提交区的这句话： Note: The returned array must be malloced, assume caller calls free().这里提到的是malloc函数，我百度了这个函数，大致理解了一下，通过malloc函数分配给要储存的数值相应的空间，所以最终代码是这样： int* twoSum(int* nums, int numsSize, int target) { int p = (int)malloc(2*sizeof(int)); //分配两个整数的空间用以储存下标； for(int i = 0;i<numsSize;i++)
{
for(int j = i+1;(j<numsSize && j != i);j++)
{
if(nums[i] + nums[j] == target)
{
p[0] = i;
p[1] = j;
}
}
}
return p;
}
