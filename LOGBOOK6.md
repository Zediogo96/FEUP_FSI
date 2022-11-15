# LOGBOOK - WEEK 7

## #1

![task](/images/task1.png)

## #2 - Crash

![task](/images/task11.png)
![task](/images/task2.png)
## #3 - Stack Data

### Only in the 64th %x we can see the first four bytes of our input.
![task](/images/task3.png)
![task](/images/task4.png)
## #4 - Heap Data

![task](/images/task6.png)
![task](/images/task5.png)
## #5 - Change The Server's Program Memory

###In this task, we simply need to echo de printf() just like in the last one and then use the %n format to write de size of our echo to the first play in the memory where we can write and the values turns to 0x1fc which is our 63 format specifiers plus the size of the address: (63*8) + 4 = 508 = 0x1fc
![task](/images/task8.png)
![task](/images/task7.png)
## #6 - Change The Address To 0x500

##In this task, since we have to to write the value 0x500 (1280 in decimal) and we already have 0x1fc, then we just need to add the remaining characters to get to 0x500. So we do: 1280-508 = 772. Then, when using the format specifier we simply add all those characters at once (similar to %.8x, but instead of 8 it's the remaining). Since we are going to substitute the 8 that was already there, we need to add it to our characters (772+8 =780). Finally, by doing that, we can see that the target value is 0x500
![task](/images/task9.png)
![task](/images/task10.png)
