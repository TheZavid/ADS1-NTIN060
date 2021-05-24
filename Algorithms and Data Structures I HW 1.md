# Algorithms and Data Structures I: HW 1:

*Task:* Arbitrarily large integers are represented as an arrays where elements are digits in decimal base are numbered 0,...,n.
Write a pseudocode of a function to multiply two such numbers and outputs the result in the same format as the input:
$\sum_{i=0}^{n}10^iA[i]$

Estimate its complexity.

*Solution:* As we have arbitrarily large numbers we have no chance in splitting the in some sensible amount of parts so we have to rely on doing operations with individual digits. My plan is to do the following: iteratively multiply each digit  of one number by the each digit of another adding the carry from the last multiplication (if any) and writing the result to the corresponding position in the resulting array (sum of the positions of both digits).

```jsx
function multiply(int array: num1, int array: num2):
	int len_1 = length(num1);
	int len_2 = length(num2);
	int[] result = [0] * (len_1 + len_2);
	
	for int i = 0 to len_1:
		int carry = 0;

		for int j = 0 to len_2:
			cur_res = num1[i]*num2[j] + result[i+j] + carry;
			carry = cur_res / 10;
			result[i+j] = cur_res % 10;
		
		result[i+j] += carry;
	
	// if needed the leading zeros can be deleted but the resulting number of an array is
	// correct even without it 
	
	return result;
```

The estimated complexity of this function would be $\Theta(len\_1\times len\_2)$ as  every number in array num_1 has to multiplied with number from an array num_2. Due to that limitation the algorithm cannot be further optimized.