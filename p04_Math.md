#### 0007 Reverse Integer

```
Input: 123
Output: 321

Input: -123
Output: -321

Input: 120
Output: 21
```



1. 取正负， 取每一位数

   * Java

   ```c++
   class Solution {
       public int reverse(int x) {
           
           if (x == 0)
               return x;
   
           long res = 0;
           long absNum = Math.abs(x);
           long sgin = x / absNum;
   
           while ( absNum != 0) {
               res = res * 10 + (absNum % 10);
               absNum = absNum / 10;
           }
           
           if (res > Integer.MAX_VALUE || res < Integer.MIN_VALUE)
               return 0;
   
           return (int) (sgin * res);
       }
   }
   ```

   

