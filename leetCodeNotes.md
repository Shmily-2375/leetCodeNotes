<div style="font-weight:bold;font-size:30px; text-align:center">Notes for leetcode</div>

##### &emsp;1. 给定一个整数数组 `nums` 和一个目标值 `target`， 请你在该数组中找出和为目标值的那 **两个** 整数，并返回他们的数组下标.

##### &emsp;给定 nums = [2, 7, 11, 15], target = 9, 因为 nums[0] + nums[1] = 2 + 7 = 9, 所以返回 [0, 1].

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

##### &emsp;2. 给定一个**非空**整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次. 找出那个只出现了一次的元素.

##### &emsp;输入:  [2, 2, 1], 输出: 1.

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

##### &emsp;3. 买卖股票的最佳时机, 给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格, 如果你最多只允许完成一笔交易(即买入和卖出一支股票), 设计一个算法来计算你所能获取的最大利润, 注意你不能在买入股票前卖出股票.

##### &emsp;输入: [7, 1, 5, 3, 6, 4], 输出5, 解释: 在第 2 天(股票价格 = 1)的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5, 注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格.

&emsp;Answer1:

```js
/**
 * @param {number[]} prices
 * @return {number}
 */
    let maxProfit = function(prices) {
      let profit = 0;
      for (let i = 0; i<prices.length; i++){
        for (let j = i+1; j<prices.length; j++){
          let tempProfit = prices[j] - prices[i];
            if (tempProfit > profit){
              profit = tempProfit;
            }
        }
      }
      return profit;
    };
```

&emsp;Answer2:

```javascript
    /**
     * @param {number[]} prices
     * @return {number}
     */
    let maxProfit = function(prices) {
      let minValue = prices[0];
      let maxProfit = 0;
      for(let i = 1 ; i<prices.length; i++){
        if (prices[i] < minValue){
          minValue = prices[i];
        }else{
          let tempProfit = prices[i] - minValue;
          if (tempProfit > maxProfit)
            maxProfit = tempProfit;
        }
      }
      return maxProfit;
    };
```

##### &emsp;4. 给定一个数组 `nums`, 编写一个函数将所有 `0` 移动到数组的末尾, 同时保持非零元素的相对顺序, 必须在原数组上操作，不能拷贝额外的数组.

#####  &emsp;输入: [0, 1, 0, 3, 12], 输出: [1, 3, 12, 0, 0].

&emsp;Answer:

```javascript
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
    let moveZeroes = function(nums) {
      let index = 0;
      for (let i = 0; i<nums.length; i++){
        if (nums[i]!==0){
          nums[index] = nums[i];
          index ++;
        }
      }
      for (;index < nums.length; index++){
        nums[index] = 0;
      }
      return nums;
    };
```

&emsp;**注:** 1.遍历数组把非零元素（假设有k个）按顺序存入数组的0至k-1位置上; 2.把原数组剩余未新赋值部分(k到n-1位置上)全设置为0.  

##### &emsp;5. 给定一个大小为 *n* 的数组，找到其中的多数元素。多数元素是指在数组中出现次数**大于** `⌊ n/2 ⌋` 的元素, 你可以假设数组是非空的，并且给定的数组总是存在多数元素.

##### &emsp;输入: [3, 2, 3], 输出: 3.

&emsp;Answer1:

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
    let majorityElement = function(nums) {
      let numsLength = nums.length;
      let countObject = {};
      for (let i = 0; i < numsLength; i++){
        if (countObject.hasOwnProperty(nums[i])){
          countObject[nums[i]]++;
        }else {
          countObject[nums[i]] = 1;
        }
        for (let j in countObject){
          if (countObject[j] > numsLength/2)
            return j;
        }
      }
    };
```

&emsp;**注:** 创建一个对象, 记录每个元素出现的次数.  

##### &emsp; 6. 给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串，判断字符串是否有效, 左括号必须用相同类型的右括号闭合, 左括号必须以正确的顺序闭合, 注意空字符串可被认为是有效字符串.  

```example
示例 1:

输入: "()"
输出: true
示例 2:

输入: "()[]{}"
输出: true
示例 3:

输入: "(]"
输出: false
示例 4:

输入: "([)]"
输出: false
示例 5:

输入: "{[]}"
输出: true
```

&emsp;Answer1:  

```javascript
   let isValid = function (s) {
      while (s.length){
        let tempStr = s;
        s = s.replace('()','');
        s = s.replace('{}','');
        s = s.replace('[]','');
        if (s === tempStr)
          return false
      }
      return true
    }
```

&emsp;**注:** 暴力解法

&emsp;Answer2:

```javascript
let isValid = function (s) {
      if (s.length % 2 !==0)
        return false;
      else {
        let leftArray = [];
        let Map = {
          '(' : ')',
          '[' : ']',
          '{' : '}'
        };
        for (let item of s){
          if (item in Map){
            leftArray.push(item);
          }else{
            if (Map[leftArray.pop()] !==item)
              return false;
          }
        }
        return !leftArray.length
      }
    }
```

&emsp;**注:**&nbsp;换一种思路，可以边遍历边匹配。也就是遍历的时候遇到左括号存入数组，下次遇到的第一个右括号必须和数组中最后一个元素匹配，否则为无效字符串，匹配完成后从数组中删除此元素。若最终数组为空，表示括号已全部匹配完，字符串有效, 非常nice!

##### &emsp;7. 给定一个整数数组 `nums` ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和.  

```example
输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6
```

&emsp;Answer:  

```javascript
   let maxSubArray = function(nums) {

      if (Math.max(nums) <= 0) {
        return Math.max(nums);

      } else {

        let tempSum = Number.MIN_VALUE;
        let ans = nums[0];

        for (let item of nums) {
          if (tempSum > 0) {
            tempSum = tempSum + item;
          } else if (tempSum <= 0) {
            tempSum = item;
          }
          ans = Math.max(ans, tempSum);
        }
        return ans;
      }
    }
```

&emsp;**注:** 首先进入函数先判断是否要求判别的数组里全部都是负数, 如果全是负数就返回负数里的最大值即可(因为负数相加只会越来越小); 若是正常的数组, 设置tempSum为累加和, ans为最后返回的最大子序和, tempSum不停地加, 每加一次ans都会记录一下当前的最大值(如果当前的累加值tempSum为目前的最大值则赋值给ans, 若不是则ans保持之前的最大值, 每一步都做记录也许下一时刻tempSum就变为最大值了), 如果tempSum累加之后＜0, 则应该抛弃tempSum(只要tempSum大于0就对累加和有增益), 将遍历到的数组当前元素的值赋值给tempSum进行新一轮的累加(之前累加的最大值早已经赋值给ans, 不用担心, 只管累加).  

##### &emsp;8.