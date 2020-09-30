8.String to Integer

### 1.题目地址
- [String to Integer(atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

### 2.初步思路

```
/**
 * 步骤:
 *   1, 跳过首部空格;
 *   2, 判断字符为正负号;
 *   3, 判断字符为数字;
 *      3.1 数字的大小是否超范围;
 *      3.1.1 不超范围,正常返回;
 *      3.1.2 超范围,返回INT_MAX或者INT_MIN
 *   4, 如果全是字符, 空字符串或者只包含空格的字符,返回0
 */
 public int stringToInteger(String str) {
	 int sign = 1;
	 int total = 0;
	 for(int i = 0; i < str.length(); i++) {
		 if (str.charAt(i) == ' ') {
			 continue;
		 } else {
			 if (str.charAt(i) == '-' || str.charAt(i) == '+') {
				 // need a variable sign to record the "+" or "-"
				 sign = str.charAt(i) == '+' ? 1 : -1;
				 continue;
			 }
			 // how to change a character to int
			 int digit = str.charAt(i) - '0';
			 // digit belongs to 0 to 9, other result is wrong
			 if (digit < 0 || digit > 9) {
				 break;
			 }
			 // check if total will be overflow after 10 times and add digit
			 if (Integer.MAX_VALUE/10 < total || Integer.MAX_VALUE/10 == total && Integer.MAX_VALUE%10 < digit) {
				 return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
			 }
			 total = 10 * total + digit;
		 }
	 }
	 return total * sign;
 }
```

### 3. 正确解法

```
// 解法一: 正常遍历
public int stringToInteger(String str) {
	int index = 0;
	int sign = 1;
	int total = 0;
	// 1, Empty String
	if (str.length() == 0) {
		return 0;
	}

	// 2, Remove Spaces
	while (index < str.length() && str.charAt(index) == ' ') {
		index++;
	}

	// check if index equals string length
	if (index == str.length()) {
		return 0;
	}

	// 3, Handle signs
	if (str.charAt(index) == '+' || str.charAt(index) == '-') {
		sign = str.charAt(index) == '+' ? 1 : -1;
		index++;
	}

	// 4, Convert number and avoid overflow
	while (index < str.length()) {
		int digit = str.charAt(index) - '0';
		if (digit < 0 || digit > 9) {
			break;
		}

		if (Integer.MAX_VALUE/10 < total || Integer.MAX_VALUE/10 == total && Integer.MAX_VALUE%10 < digit) {
			return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
		}
		total = 10 * total + digit;
		index++;
	}
	return total * sign;
}
```