# C Code
C code has some interesting vulnerabilities when it comes to binary exploitation. 
### Max Value 
Below has a good explanation with example code. I got this from the AllArmyCTF.
```
int tmp = first * second;
  /* In some languages (e.g. Python 3) there are no issues with the line above
   * and it will always match the intuitive meaning: `tmp` equals the product
   * of the two integers that were passed in and is therefore positive.
   *
   * However, this is not how C (or most languages with fixed-width integers)
   * works.  Instead the calculation can "overflow" the highest expressible
   * integer and wrap around to the lowest expressible integer and keep going.
   * In other words, it is entirely possible to get a negative number for
   * `tmp` by multiplying two numbers that are less than INT_MAX (2147483647).
   *
   * In the line below, we create the vulnerability by using `tmp` to access
   * the "numbers" array in our struct.  In C the modulo operator (%) (also
   * known as "remainder"), has the same sign as the left-hand side.  This
   * means if `tmp` is negative, we will end up accessing memory that is
   * outside of the array.
   *
   * How can we leverage this to print the flag?
   */
  printf("%d * %d = %d which ends in a '%s'\r\n",
         first, second, tmp, s.numbers[tmp % 10]);
}
```