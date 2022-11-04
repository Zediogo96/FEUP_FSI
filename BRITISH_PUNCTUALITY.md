# British Punctuality

## Challenge description:

The challenge consists in reading a file (flag.txt) that resides in a privileged folder to which we have no permission to even read. In the home directory where we are placed we have read-only permissions.

<br>

## CTF Solution

When I first got into the machine I was clueless as to which direction take while approaching the problem so I started by reading the script and understand what it does.

![main.c](/images/main.png)

![my_script](/images/my_script.png)

After a more thorough examination I saw that it accessed the following file: _/tmp/env_ that gives as a hint on how to solve the CTF. So I headed to the _/tmp_ folder and saw nothing but a *last_log* file that contained the environment variables but from the _flag_reader_ and not the _nobody_ which gave me a clue that whatever created that file has _flag_reader_ permissions.

![last_log](/images/last_log.png)

The name of the challenge can also be a hint. *British Punctuality* directs us to cron jobs. So I went into the _/etc_ folder. After going through all the cron folders, one file standed out: _my_cron_script_. I read the filed and noticed that it was running the first _my_script_ every minute (because the time fields where all as "*") and after seeing the privileges of this _my_cron_script_ noticed it run as _flag_reader_ and outputs the result to _/tmp/last_log_. Found it!

![my_cron_script](/images/my_cron_script.png)

Now the idea is: since it runs _my_script_ as _flag_reader_ I can inject my commands in there by changing what the script does or intended to do by, for example, changing the *cat* command by changing the $PATH with the _/tmp/env_ file.

These where the commands:

`sh`

`
echo "int main() { \n setuid(0);\n system(\"cat /flags/flag.txt\"); \n }" > service.c ; gcc service.c -o printenv
`

`
echo "PATH=/tmp:$PATH" > env
`

## Result:

![flag](/images/flag.png)

