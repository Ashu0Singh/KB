### Optimal Solution 

So first we will calculate sum of the array and sum of the first n elements, and we'll get an equation like `x - y = sum - sumOfN` we'll do the same for squares and we'll get `(x - y)(x + y) = sqSum + sqSumOfN` solve the above equations to get the ans.

If you're wonder how did we get to this equation
```
{1 4 2 2 5}

sum of all - sum of n

(u + v + x + x + z) - ( u + x + v + y + z)

so you can see that x(repeating number) is there in the first array and y(missing number) in the second array is there in the second array everything else will cancel out
```

```java
class Solution {
    public int[] findMissingRepeatingNumbers(int[] nums) {
        long sum = 0, sumn = 0;
        long sqSum = 0, sqSumn = 0;
        int n = nums.length;
        for(int num : nums){
            sum = sum + num;
            sqSum = sqSum + (num * num);
        }

        sumn = (n * (n + 1))/2;
        sqSumn = (n * (n + 1) * (2 * n + 1))/6;

        long value1 = sum - sumn;
        long value2 = (sqSum - sqSumn)/value1;

        long x = (value1 + value2)/2;
        long y = x - value1;

        return new int[]{(int)x,(int)y};
    }
}
```