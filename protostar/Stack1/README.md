
## Answer

From using radare we can see that we are trying to write the string `dcba` into the variable modified.

To do this we just need to fill up the buffer by passing an arg of length 64 + 12 chars once we reach this the next char will start writting into modified.  So to solve we can simply do:

`./stack1 AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABCDEFGHIJKLMdcba
`
