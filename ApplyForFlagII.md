# Apply for a flag II

## Challenge description:

The challenge consists in creating a stored XSS to make the website admin, unintentionally give as the flag.

<br>

## CTF Solution

When first trying to make the admin click the "Give the Flag" button, I tried to make the javascript reach that page almost the same as the Apply For Flag original CTF but unsurprisingly, it didn't work.

![XSS](/images/aff2_1.png)

![alert](/images/aff2_2.png)

Therefore, if we can't reach that page we need to emulate it, and we can do so by recreating the form in the page we can reach and then make the admin click it there when the page refreshes.

```html
    <form name=TheForm action=http://ctf-fsi.fe.up.pt:5005/request/a02d0c9f2e174b52271fdd308238dd74dfcba007/approve method=post><script> document.TheForm.submit();</script>
```


![XSS Injection](/images/aff2_3.png)

Although there was a small detail that could drive anyone crazy if they didn't know about this. Depending on the browser, in Mozilla Firefox for example, you need to disable javascript for this to work, otherwhise the browser will block your request.

![js disabled](/images/aff2_4.png)

Now, when the admin enters that page, he will unwillingly submit this form and give as the flag.

## Result:

![flag{3bf33f44ceb03ffc3ee3fad11f3f96e5}](/images/aff2_5.png)
