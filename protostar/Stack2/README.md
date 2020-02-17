

This time the variable that we need to modify is setup in rbp-0xc

```
0x00001209      c745f4000000.  mov dword [rbp - 0xc], 0 # initialising modified variable to 0
0x00001210      488b55f8       mov rdx, qword [rbp - 8]
0x00001214      488d45b0       lea rax, qword [rbp - 0x50] # these two lines are preparing the call to strcpy, greenie pointer is in rbp-8, and buffer is in rbp-0x50
```

To calculate the padding to overwrite the varible we just need work out where the buffer starts and take off the modified variable:

```
0x50 - 0xc 
80   - 12 = 68
```



