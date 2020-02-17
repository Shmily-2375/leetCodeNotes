<div style="font-weight:bold;font-size:30px"><center>Notes for leetcode</center></div>
##### &emsp;1. 给定一个整数数组 `nums` 和一个目标值 `target`， 请你在该数组中找出和为目标值的那 **两个** 整数，并返回他们的数组下标 .

##### &emsp;给定 nums = [2, 7, 11, 15], target = 9, 因为 nums[0] + nums[1] = 2 + 7 = 9, 所以返回 [0, 1] .

&emsp;Answer:  

```
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
    let twoSum = function(nums, target) {
      let numsLength = nums.length;
      for(let i = 0; i < numsLength; i++){
        for (let j = i + 1 ; j < numsLength ; j++){
          if ((nums[i] + nums[j]) === target){
            return [i, j];
          }
        }
      }
    };
```

##### &emsp;2. 给定一个**非空**整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次. 找出那个只出现了一次的元素 .

##### &emsp;输入:  [2, 2, 1], 输出: 1 .  

&emsp;Answer:

```js
/**
 * @param {number[]} nums
 * @return {number}
 */ 
    let singleNumber = function(nums) {
        let result = 0;
        for(let term of nums){
            result = result ^ term;
        }
        return result;
    };
```

&emsp;**注: ** 通过异或运算来实现, 0⊕a == a, a⊕a == 0, 所以b⊕a⊕a == b, 由题目可知除了出现1次的元素以外, 其余元素都出现2次, 通过异或运算得0(两两抵消), 所以最后结果为  出现了1次的元素  ⊕  0  得到出现了1次的元素 .

##### &emsp;3. 

