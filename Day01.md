## Leetcode

### day01 

#### T2027转换字符串的最少操作次数

给你一个字符串 s ，由 n 个字符组成，每个字符不是 'X' 就是 'O' 。一次 操作 定义为从 s 中选出 三个连续字符 并将选中的每个字符都转换为 'O' 。注意，如果字符已经是 'O' ，只需要保持 不变 。返回将 s 中所有字符均转换为 'O' 需要执行的 最少 操作次数。

```c
int minimumMoves(char * s){
        int count = 0;
        int i = 0;
        while(i < strlen(s)){
                if(s[i]=='X'){
                count++;
                i+=3;
        }else {
                i++;
                }
        }
        return count;
}

```

**学习感悟：**

- c语言字符串结束标志**‘\0’**

- 头文件<string.h>---函数**strlen()**求字符串长度

- 算法只是算个次数，不用将题目中结果实现，例如本题中不用考虑将X变为0的过程，而只需要考虑遇到X时次数加1，仅此而已。

  

#### T1两数之和

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。你可以按任意顺序返回答案。

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().//数组要被分配空间
 */
int* twoSum(int* nums, int numsSize, int target, int* returnSize){
        int i = 0;
        int j = 1;
        for(i = 0;i < numsSize-1;i++){
                //j需要在进入下一次i循环之前重置
                for(j = i+1;j < numsSize;j++){
                        if(nums[i]+nums[j]==target){
                                int* ret = malloc(sizeof(int)*2);//分配内存
                                ret[0] = i;
                                ret[1] = j;
                                *returnSize = 2;//返回数组大小为2
                                return ret;
                        }
                }
        } 
        *returnSize = 0;//未找到匹配的数，不用返回数组大小
        return NULL;//未找到匹配的数，返回空值
}

```

**学习感悟**

- 双层for循环的条件限定
  - 对于每次新的i值，j层的循环都要<font color='red'>相对后移一位</font>，所以j=i+1
  - 确定好i,j层循环的终止条件

- 分配内存malloc函数(**头文件#include<malloc.h>**)

  - malloc内的参数是需要<font color='red'>动态分配的字节数</font>>

  - ```
    type *var_name = (type*)malloc(sizeof(type)*num);
    ```

- *returnSize记录返回值个数便于获取**所有**返回值（ps:该参数为地址传递，会带值出去，有可能是在函数外部有用到该参数）
- return ret为返回值（<font color='red'>需要内存空间</font>>）

