# 面试题56 - I. 数组中数字出现的次数

解法选择
看到题目第一眼就觉得应该是需要用到异或来做的。
题目又要求了：时间复杂度为O(n),空间复杂度为O(1)。
因此不能用map（空间复杂度为O(n)）与双重循环嵌套（空间复杂度为O(n^2)）。

解析题目
由于数组中存在着两个数字不重复的情况，我们将所有的数字异或操作起来，最终得到的结果是这两个数字的异或结果：(相同的两个数字相互异或，值为0)) 最后结果一定不为0，因为有两个数字不重复。

演示：

```
4 ^ 1 ^ 4 ^ 6 => 1 ^ 6

6 对应的二进制： 110
1 对应的二进制： 001
1 ^ 6  二进制： 111
```
此时我们无法通过 111（二进制），去获得 110 和 001。
那么当我们可以把数组分为两组进行异或，那么就可以知道是哪两个数字不同了。
我们可以想一下如何分组：

重复的数字进行分组，很简单，只需要有一个统一的规则，就可以把相同的数字分到同一组了。例如：奇偶分组。因为重复的数字，数值都是一样的，所以一定会分到同一组！
此时的难点在于，对两个不同数字的分组。
此时我们要找到一个操作，让两个数字进行这个操作后，分为两组。
我们最容易想到的就是 & 1 操作， 当我们对奇偶分组时，容易地想到 & 1，即用于判断最后一位二进制是否为1。来辨别奇偶。
你看，通过 & 运算来判断一位数字不同即可分为两组，那么我们随便两个不同的数字至少也有一位不同吧！
我们只需要找出那位不同的数字mask，即可完成分组（ & mask ）操作。

为了操作方便，我们只去找最低位的mask:

|      |      |      |      |
| :---: | :---: | :---: | :---: |
|num1: | 101110 |   110  |   1111 |
|num2: | 111110   | 001   |  1001 |
|mask: | 010000  |   001 |    0010 |
由于两个数异或的结果就是两个数数位不同结果的直观表现，所以我们可以通过异或后的结果去找最低位的mask！

