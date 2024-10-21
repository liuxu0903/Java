# H 指数

## 题目(中等)

给你一个整数数组 `citations` ，其中 `citations[i]` 表示研究者的第 `i` 篇论文被引用的次数。计算并返回该研究者的 **`h` 指数**。

根据维基百科上 [h 指数的定义](https://baike.baidu.com/item/h-index/3991452?fr=aladdin)：`h` 代表“高引用次数” ，一名科研人员的 `h` **指数** 是指他（她）至少发表了 `h` 篇论文，并且 **至少** 有 `h` 篇论文被引用次数大于等于 `h` 。如果 `h` 有多种可能的值，**`h` 指数** 是其中最大的那个。

**示例 1：**

> **输入**：citations = [3,0,6,1,5]
> **输出**：3 
> **解释**：给定数组表示研究者总共有 5 篇论文，每篇论文相应的被引用了 3, 0, 6, 1, 5 次。
>      由于研究者有 3 篇论文每篇 至少 被引用了 3 次，其余两篇论文每篇被引用 不多于 3 次，所以她的 h 指数是 3。

**示例 2：**

> **输入**：citations = [1,3,1]
> **输出**：1

**提示：**

- n == citations.length
- 1 <= n <= 5000
- 0 <= citations[i] <= 1000

## 思路

![](D:\消息记录\TyporaPages\论文引用次数.png)

- 先从小到大排序
- 再遍历判断当前元素是否大于等于剩余长度(当前元素到最后一个元素的长度)
- 如果大于等于则最大引用次数就是剩余长度

## 答案

```java
class Solution {
    public int hIndex(int[] citations) {
        Arrays.sort(citations);//从小到大排序
        int length = citations.length;//数组长度
        for(int i = 0; i < length; i++){
            if(citations[i] >= (length - i))//当前元素是否大于等于剩余长度
                return length - i;//最大引用次数就是剩余长度
        }
        return 0;
    }
}
```

# 罗马数字转整数

## 题目(简单)

罗马数字包含以下七种字符: `I`， `V`， `X`， `L`，`C`，`D` 和 `M`。

> **字符**          **数值**
> I             	  1
> V            	   5
> X             	 10
> L             	  50
> C             	 100
> D             	 500
> M             	1000

例如， 罗马数字 `2` 写做 `II` ，即为两个并列的 1 。`12` 写做 `XII` ，即为 `X` + `II` 。 `27` 写做 `XXVII`, 即为 `XX` + `V` + `II` 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 `IIII`，而是 `IV`。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 `IX`。这个特殊的规则只适用于以下六种情况：

- `I` 可以放在 `V` (5) 和 `X` (10) 的左边，来表示 4 和 9。
- `X` 可以放在 `L` (50) 和 `C` (100) 的左边，来表示 40 和 90。 
- `C` 可以放在 `D` (500) 和 `M` (1000) 的左边，来表示 400 和 900。

给定一个罗马数字，将其转换成整数。

**示例 1:**

> **输入**:  s = "III"
> **输出**:  3

**示例 2:**

> **输入**:  s = "IV"
> **输出**:  4

**示例 3:**

> **输入**:  s = "IX"
> **输出**:  9

**示例 4:**

> **输入**:  s = "LVIII"
> **输出**:  58
> **解释**:  L = 50, V= 5, III = 3.

**示例 5:**

> **输入**:  s = "MCMXCIV"
> **输出**:  1994
> **解释**:  M = 1000, CM = 900, XC = 90, IV = 4.

**提示：**

- `1 <= s.length <= 15`
- `s` 仅含字符 `('I', 'V', 'X', 'L', 'C', 'D', 'M')`
- 题目数据保证 `s` 是一个有效的罗马数字，且表示整数在范围 `[1, 3999]` 内
- 题目所给测试用例皆符合罗马数字书写规则，不会出现跨位等情况。
- IL 和 IM 这样的例子并不符合题目要求，49 应该写作 XLIX，999 应该写作 CMXCIX 。
- 关于罗马数字的详尽书写规则，可以参考 [罗马数字 - 百度百科](https://baike.baidu.com/item/罗马数字/772296)。

## 思路

### 思路一

只用 if-else 和 switch 语句写出来。

### 思路二

- 设 x=s[i−1],y=s[i]，这是两个相邻的罗马数字。
- 如果 x 的数值小于 y 的数值，那么 x 的数值要取相反数。例如 IV 中的 I 相当于 −1，CM 中的 C 相当于 −100。
  把所有数值相加，即为答案。

代码实现时，可以创建一个哈希表，把字符映射为对应的数值，这样无需写一堆 if-else。

## 答案

### 思路一答案

```java
class Solution {
    public int romanToInt(String s) {
        int sum = 0;
        for (int i = 0; i < s.length(); i++) {
            if (i > 0 && (s.substring(i, i + 1).equals("V") || s.substring(i, i + 1).equals("X")) && s.substring(i - 1, i).equals("I")){
                sum += result(s.substring(i, i + 1)) - 2 * result(s.substring(i - 1, i));
                //I 在 V 和 X 左边时
            } else if (i > 0 && (s.substring(i, i + 1).equals("L") || s.substring(i, i + 1).equals("C")) && s.substring(i - 1, i).equals("X")){
                sum += result(s.substring(i, i + 1)) - 2 * result(s.substring(i - 1, i));
                //X 在 L 和 C 左边时
            } else if (i > 0 && (s.substring(i, i + 1).equals("D") || s.substring(i, i + 1).equals("M")) && s.substring(i - 1, i).equals("C")){
                sum += result(s.substring(i, i + 1)) - 2 * result(s.substring(i - 1, i));
                //C 在 D 和 M 左边时
            } else {
                sum += result(s.substring(i, i + 1));
            }
        }
        return sum;
    }

    public int result(String c) { //用switch语句保存字符信息
        int sum = 0;
        switch (c) {
            case "I":
                sum = 1;
                break;
            case "V":
                sum = 5;
                break;
            case "X":
                sum = 10;
                break;
            case "L":
                sum = 50;
                break;
            case "C":
                sum = 100;
                break;
            case "D":
                sum = 500;
                break;
            case "M":
                sum = 1000;
                break;
            default:
                return 0;
        }
        return sum;
    }
}
```

### 思路二答案

```java
class Solution {
    private static final Map<Character, Integer> ROMAN = Map.of(
        'I', 1,
        'V', 5,
        'X', 10,
        'L', 50,
        'C', 100,
        'D', 500,
        'M', 1000
    );

    public int romanToInt(String S) {
        char[] s = S.toCharArray(); // 也可以下面用 charAt，从而保证空间复杂度是 O(1)
        int n = s.length;
        int ans = 0;
        for (int i = 1; i < n; i++) { // 遍历相邻的罗马数字
            int x = ROMAN.get(s[i - 1]);
            int y = ROMAN.get(s[i]);
            ans += x < y ? -x : x;
        }
        return ans + ROMAN.get(s[n - 1]); // 加上最后一个
    }
}
```

