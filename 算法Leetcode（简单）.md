# 算法Leetcode（简单）

## 1.两数之和

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。
https://leetcode.cn/problems/two-sum

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
   for(let i=0; i<nums.length; i++) {
     for(let j=i+1; j<nums.length; j++) {
       if(nums[i]+nums[j]===target) {
         return [i,j];
       }
     }
   }
};
```

## 2.回文数

给你一个整数 x ，如果 x 是一个回文整数，返回 true ；否则，返回 false 。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

例如，121 是回文，而 123 不是。
https://leetcode.cn/problems/palindrome-number

```js
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
  if(x<0) return false;
  if(x === 0) return true;
  let cur = 0;
  let num = x;
  while(num !== 0) {
    cur = cur * 10 + num % 10;
    num = Math.floor(num/10);
  }
  return cur === x;
};
```

## 3.罗马数字转整数

罗马数字包含以下七种字符: I， V， X， L，C，D 和 M。

字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
例如， 罗马数字 2 写做 II ，即为两个并列的 1 。12 写做 XII ，即为 X + II 。 27 写做  XXVII, 即为 XX + V + II 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 IIII，而是 IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 IX。这个特殊的规则只适用于以下六种情况：

I 可以放在 V (5) 和 X (10) 的左边，来表示 4 和 9。
X 可以放在 L (50) 和 C (100) 的左边，来表示 40 和 90。 
C 可以放在 D (500) 和 M (1000) 的左边，来表示 400 和 900。

给定一个罗马数字，将其转换成整数。
https://leetcode.cn/problems/roman-to-integer

```js
/**
 * @param {string} s
 * @return {number}
 */
var romanToInt = function(s) {
  let total = 0;
  for(let i=0; i<s.length; i++) {
    switch(s.charAt(i)) {
      case 'I':
        total = total + 1;
        break;
      case 'V':
        total = total + 5;
        break;
      case 'X':
        total = total + 10;
        break;
      case 'L':
        total = total + 50;
        break;
      case 'C':
        total = total + 100;
        break;
      case 'D':
        total = total + 500;
        break;
      case 'M':
        total = total + 1000;
        break;
    }
    if(i!==0) {
      if((s.charAt(i)=== 'V'||s.charAt(i)==='X') && (s.charAt(i-1)==='I')) {
        total = total - 1*2;
      }
      if((s.charAt(i)=== 'L'||s.charAt(i)==='C') && (s.charAt(i-1)==='X')) {
        total = total - 10*2;
      }
      if((s.charAt(i)=== 'D'||s.charAt(i)==='M') && (s.charAt(i-1)==='C')) {
        total = total - 100*2;
      }
    }
  }
  return total;
}
```

## 4.最长公共前缀

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。

https://leetcode.cn/problems/longest-common-prefix

```js
/**
 * @param {string[]} strs
 * @return {string}
 */
var longestCommonPrefix = function(strs) {
  let com = strs[0];
  for(let i=1; i<strs.length; i++) {
    let j=0;
    for(;j<strs[i].length;j++) {
      if(com[j] !== strs[i][j]) break;
    }
    com = com.substr(0,j);
  }
  return com;
}
```

## 5.有效的括号

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串 s ，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
每个右括号都有一个对应的相同类型的左括号。
https://leetcode.cn/problems/valid-parentheses

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function(s) {
    let stack = [];
    for(let val of s) {
        if(val==='(') stack.push(')');
        else if(val==='{') stack.push('}');
        else if(val==='[') stack.push(']');
        else if(s.length===0 || val!==stack.pop()) return false;
    }
    return stack.length===0;
}
```

## 6.合并两个有序链表

将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

<img src="https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg" alt="img" style="zoom:50%;" />

https://leetcode.cn/problems/merge-two-sorted-lists

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} list1
 * @param {ListNode} list2
 * @return {ListNode}
 */
var mergeTwoLists = function(list1, list2) {
  if(list1===null) return list2;
  if(list2===null) return list1;
  if(list1.val>list2.val) {
    list2.next = mergeTwoLists(list1,list2.next);
    return list2;
  }	else {
    list1.next = mergeTwoLists(list1.next,list2);
    return list1;
  }
}
```

## 7.删除有序数组中的重复项

给你一个升序排列的数组 nums ，请你原地删除重复出现的元素，使每个元素只出现一次 ，返回删除后数组的新长度。元素的相对顺序 应该保持一致 。

由于在某些语言中不能改变数组的长度，所以必须将结果放在数组nums的第一部分。更规范地说，如果在删除重复项之后有 k 个元素，那么 nums 的前 k 个元素应该保存最终结果。

将最终结果插入 nums 的前 k 个位置后返回 k 。

不要使用额外的空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

- 判题标准:

  ​	系统会用下面的代码来测试你的题解:

  ​	int[] nums = [...]; // 输入数组
  ​	int[] expectedNums = [...]; // 长度正确的期望答案

  ​	int k = removeDuplicates(nums); // 调用

  ​	assert k == expectedNums.length;
  ​	for (int i = 0; i < k; i++) {
  ​    	assert nums[i] == expectedNums[i];
  ​	}

如果所有断言都通过，那么您的题解将被 通过。

https://leetcode.cn/problems/remove-duplicates-from-sorted-array
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
    if(nums.length===0) return 0;
    let p = 1;
    let q = 1;
    while(p < nums.length) {
        if(nums[p] !== nums[p-1]) {
            nums[q] = nums[p];
            q++;
        }
        p++;
    }
    return q;
};
```

## 8.移除元素

给你一个数组 nums 和一个值 val，你需要**原地**移除所有数值等于 val 的元素，并返回移除后数组的新长度。不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

-  说明:

  ​		为什么返回数值是整数，但输出的答案是数组呢?

  ​		请注意，输入数组是以「引用」方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

  ​		你可以想象内部操作如下

  ​		// nums 是以“引用”方式传递的。也就是说，不对实参作任何拷贝
  ​			int len = removeElement(nums, val);

  ​		// 在函数里修改输入数组对于调用者是可见的。
  ​		// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内的所有元素。
  ​			for (int i = 0; i < len; i++) {
     			 print(nums[i]);
  ​			}

https://leetcode.cn/problems/remove-element
```js
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
var removeElement = function(nums, val) {
    if(nums.length === 0) return 0;
    let p = 0;
    let q = 0;
    while(p < nums.length) {
        if(nums[p] !== val) {
            nums[q] = nums[p];
            q++;
        }
        p++;
    }
    return q;
};
```

## 9.搜索插入位置

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。请必须使用时间复杂度为 O(log n) 的算法。

https://leetcode.cn/problems/search-insert-position
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {
   let l = nums.length;
   if(target > nums[l-1]) return l;
   for(let i=0; i<l; i++) {
       if(nums[i]===target || target < nums[i]) return i;
   }
};
```

## 10.最后一个单词的长度

给你一个字符串 s，由若干单词组成，单词前后用一些空格字符隔开。返回字符串中 最后一个 单词的长度。

单词 是指仅由字母组成、不包含任何空格字符的最大子字符串。
https://leetcode.cn/problems/length-of-last-word

```js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLastWord = function(s) {
  	//方法一
    let strs = s.trim().split(" ");
    return strs[strs.length-1].length;
  
  	//方法二
  	//let end = s.length - 1;
    //while(s.charAt(end) === " ") end--;
    //let wordLength = 0;
    //while(end >= 0 && s.charAt(end) !== " ") {
        //wordLength++;
        //end--;
    //};
    //return wordLength;
};
```

## 11.加一

给定一个由 整数 组成的 非空 数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。
https://leetcode.cn/problems/plus-one

```js
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function(digits) {
    //①方法一
    let len = digits.length;
    for(let i=len-1; i>=0; i--) {
        if(digits[i] !== 9) {
            digits[i] += 1;
            for(let j=i+1; j<len; j++) {
                digits[j] = 0;
            }
            return digits;
        }
    }
    const ans = new Array(len+1).fill(0);
    ans[0] = 1;
    return ans;
   //②方法二
   const len = digits.length;
    for(let i=len-1; i>=0; i--) {
        digits[i] += 1;
        digits[i] %= 10;
        if(digits[i] !== 0) {
            return digits;
        }
    }
    digits = [1,...Array(len).fill(0)];
    return digits;
};
```

## 12.二进制求和

给你两个二进制字符串 `a` 和 `b` ，以二进制字符串的形式返回它们的和。

https://leetcode.cn/problems/add-binary

```js
/**
 * @param {string} a
 * @param {string} b
 * @return {string}
 */
var addBinary = function(a, b) {
    let str = '';
    let ca = 0;
    for(let i=a.length-1 , j=b.length-1; i>=0 || j>=0; i-- , j--) {
        let sum = ca;
        sum += i>=0? parseInt(a[i]) : 0;
        sum += j>=0? parseInt(b[j]) : 0;
        str += sum % 2;
        ca = Math.floor(sum/2);
    }
    str += ca==1 ? ca : '';
    return str.split('').reverse().join('');
};
```

## 13.x的平方根

给你一个非负整数 x ，计算并返回 x 的 算术平方根 。由于返回类型是整数，结果只保留 整数部分 ，小数部分将被 舍去 。

注意：不允许使用任何内置指数函数和算符，例如 pow(x, 0.5) 或者 x ** 0.5 。

https://leetcode.cn/problems/sqrtx
```js
/**
 * @param {number} x
 * @return {number}
 */
var mySqrt = function(x) {
  let left = 1;
  let right = x;
  let mid = 0;
  while(left <= right) {
    let mid = left + Math.floor((right - left)/2);
    let temp = Math.floor(x / mid);
    if(temp < mid) {
      right = mid - 1;
    } else if(temp > mid) {
      left = mid + 1;
    } else if(temp === mid) {
      return temp;
    }
  }
  return right;
};
```

## 14.爬楼梯

假设你正在爬楼梯。需要 `n` 阶你才能到达楼顶。

每次你可以爬 `1` 或 `2` 个台阶。你有多少种不同的方法可以爬到楼顶呢？

https://leetcode.cn/problems/climbing-stairs

```js
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function(n) {
  	//方法①
    let dp = [1,2];
    for(let i = 2; i < n; i++) {
        dp[i] = dp[i-1] + dp[i-2];
    }
    return dp[n-1];
  
  	//方法②
    if(n===1) return 1;
    if(n===2) return 2;
    let a = 1,b = 2,temp = 0;
    for(let i=3; i<=n; i++) {
       temp = a + b;
       a = b;
       b = temp;
    }
    return b;
};
```

## 15.删除链表中的重复元素

给定一个已排序的链表的头 `head` ， *删除所有重复的元素，使每个元素只出现一次* 。返回 *已排序的链表* 。

https://leetcode.cn/problems/remove-duplicates-from-sorted-list

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var deleteDuplicates = function(head) {
    let cur = head;
    while(cur && cur.next) {
        if(cur.val !== cur.next.val) {
            cur = cur.next;
        } else {
            cur.next = cur.next.next;
        }
    }
    return head;
};
```

## 16.合并两个有序数组

给你两个按 非递减顺序 排列的整数数组 nums1 和 nums2，另有两个整数 m 和 n ，分别表示 nums1 和 nums2 中的元素数目。请你 合并 nums2 到 nums1 中，使合并后的数组同样按 非递减顺序 排列。

注意：最终，合并后数组不应由函数返回，而是存储在数组 nums1 中。为了应对这种情况，nums1 的初始长度为 m + n，其中前 m 个元素表示应合并的元素，后 n 个元素为 0 ，应忽略。nums2 的长度为 n 。

https://leetcode.cn/problems/merge-sorted-array
```js
/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function(nums1, m, nums2, n) {
    let p = m - 1;
    let q = n - 1;
    let cur = m + n - 1;
    while(p >= 0 || q >= 0) {
        if(p<0) {
            nums1[cur] = nums2[q];
            q--;
        } else if(q<0) {
            nums1[cur] = nums1[p];
            p--;
        } else if(nums1[p] < nums2[q]) {
            nums1[cur] = nums2[q];
            q--;
        } else {
            nums1[cur] = nums1[p];
            p--;
        }
        cur--;
    }
};
```

## 17.二叉树的中序遍历

给定一个二叉树的根节点 `root` ，返回 *它的 **中序** 遍历* 。

https://leetcode.cn/problems/binary-tree-inorder-traversal

<img src="https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg" alt="img" style="zoom:50%;" />

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var inorderTraversal = function(root) {
    let res = [];
    let stack = [];
    while(root || stack.length) {
        while(root) {
            stack.push(root);
            root = root.left;
        }
        root = stack.pop();
        res.push(root.val);
        root = root.right;
    }
    return res;
};
```

## 18.相同的树

给你两棵二叉树的根节点 `p` 和 `q` ，编写一个函数来检验这两棵树是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

https://leetcode.cn/problems/same-tree

 ```js
 /**
 * Definition for a binary tree node.
  * function TreeNode(val, left, right) {
  *     this.val = (val===undefined ? 0 : val)
  *     this.left = (left===undefined ? null : left)
  *     this.right = (right===undefined ? null : right)
  * }
  */
 /**
  * @param {TreeNode} p
  * @param {TreeNode} q
  * @return {boolean}
  */
 var isSameTree = function(p, q) {
    if(p===null && q===null) return true;
    if(p===null || q===null) return false;
    if(p.val !== q.val) return false;
    return isSameTree(p.left,q.left) && isSameTree(p.right,q.right);
 };
 ```

## 19.对称二叉树

给你一个二叉树的根节点 `root` ， 检查它是否轴对称。

https://leetcode.cn/problems/symmetric-tree

```js
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
//递归
var isSymmetric = function(root) {
  if(root === null) return true;
  return isChildSymmetric(root.left,root.right);
}
function isChildSymmetric(left,right) {
  if(left === null && right === null) return true;
  if(left === null || right === null) return false;
  if(left.val !==  right.val) return false;
  return isChildSymmetric(left.left,right.right)&&isChildSymmetric(right.left,left.right);
}
```

## 20.二叉树的最大深度

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明:** 叶子节点是指没有子节点的节点。

https://leetcode.cn/problems/maximum-depth-of-binary-tree

```js
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function(root) {
  if(root === null) {
    return 0;
  } else {
    let left = maxDepth(root.left);
    let right = maxDepth(root.right);
    let depth = 1 + Math.max(left,right);
    return depth;
  }
}
```

## 21.将有序数组转化为二叉搜索树

给你一个整数数组 nums ，其中元素已经按 升序 排列，请你将其转换为一棵 高度平衡 二叉搜索树。

高度平衡 二叉树是一棵满足「每个节点的左右两个子树的高度差的绝对值不超过 1 」的二叉树。

https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {number[]} nums
 * @return {TreeNode}
 */

 //方法① 
var sortedArrayToBST = function(nums) {
  if(!nums.length) return null;
  let rootIndex = Math.floor(nums.length/2);
  let root = new TreeNode(nums[rootIndex]);
  let left = rootIndex - 1;
  let right = rootIndex + 1;
  if(left >= 0) {
    root.left = sortedArrayToBST(nums.slice(0,rootIndex));
  }
  if(right >= 0) {
    root.right = sortedArrayToBST(nums.slice(right,nums.length));
  }
  return root;
}

//方法②
var sortedArrayToBST = function(nums) {
  return helper(nums,0,nums.length-1);
}
var helper = function(nums,left,right) {
  if(left > right) return null;
  let mid = Math.floor((left+right)/2);
  let root = new TreeNode(nums[mid]);
  root.left = helper(nums,left,mid-1);
  root.right = helper(nums,mid+1,right);
  return root;
}
```

