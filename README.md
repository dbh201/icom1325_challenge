# Challenge Overview
This CTF Challenge was created as part of the Project Management course. It contains 3 flags and it is all about getting access one step at a time!

This challenge can be difficult for a student, so don't worry if you can't get it done. Also, don't forget to check the hints if you are struggling at some point.

# Getting started
First, download the challenge container.
```
docker pull ghcr.io/dbh201/challenge4:latest
```
Now, launch the container.
```
docker run -p 4443:4443 ghcr.io/dbh201/challenge4:latest
```
Access the website https://localhost:4443 and good luck!

At some point, you will use a reverse shell script in this challenge. If you are not familiar with them, we recommend one as a hint, so don't worry about it.

Also, Kali is not mandatory but recommended, since it has plenty of pre-installed tools that could be useful for this and other challenges. 

# Hints
## Flag 1
Can you get all 3 flags? Let's start by navigating to pages you are not supposed to see.
Wonder what kind of information you can find in there

<details>
    <summary>Hint 1</summary>
    Try navigating to a different directory
</details>

<details>
    <summary>Hint 2</summary>
    Some names are very common across different applications
</details>

<details>
    <summary>Hint 3</summary>
    Alright! Let's bruteforce! Kali has some cool pre-installed Web Crawlers & Directory bruteforces.
</details>

## Flag 2
How much can you do with your new admin account? There must be some way to control the forum.

<details>
    <summary>Hint 1</summary>
    You can definitely do a lot from the admin control panel!
</details>

<details>
    <summary>Hint 2</summary>
    Isn't it cool that you can even upload any file you want?
</details>

<details>
    <summary>Hint 3</summary>
    Some scripts (files) can even give you access to the system, just like magic.
</details>

<details>
    <summary>Hint 4</summary>
    give "p0wny" a try x)
</details>

## Flag 3
Now it's time to escalate...
You need to become root using your p0wny shell, but you can't seem to type in your password...


<details>
    <summary>Hint 1</summary>
    sudo will not work, so let's try switching user.
</details>

<details>
    <summary>Hint 2</summary>
    Can you believe some people reutilize their passwords?! Crazy, right?
</details>

<details>
    <summary>Hint 3</summary>
    It's all about the one-liners these days, isn't it?
</details>


# Solution
## Flag 1
Since we are supposed to look for pages that should be unacessible, we could try a few common names such as "/admin". However, some tools can do their job for us.

Dirb is a fantastic tool for that, and it is already installed in Kali. We can simply run it on our server (make sure you change the IP to match yours).
```bash

```
After checking some of the results, we will eventually find the /data directory, that contains some interest files such as "flag1.txt". 

>> IMG 1

<details>
    <summary>By checking "flag1.txt" content we will find the first flag!</summary>
    <pre><code>
    flag1: Pr0Jmngmnt15c00l

    User: admin
    Password: thispasswordishuge!

    You got the flag! What a place for a password to be, right? :P
    How much can you do with your new admin account? There must be some way to control the forum. 
</code></pre>

</details>


## Flag 2
Now that we have admin credentials, let's see what we can do with that.

First, login with your recently "stolen" credentials! Hey, they shouldn't keep it on a text file!

Exploring some of the buttons on the forum, we will eventually come across "Administration", which will take us to the Admin Control Panel.

>> IMG 2

More exploring! After checking some of the links on the Admin Control Panel, we will eventually find the "File Administration System", where we can see, download, and - most important - upload some files.

>> IMG 3

Good for us, this forum doesn't even check what files are being uploaded, so we are going to import a script!

Some scripts can grant you access to the system, and although programming one from scratch can be done, we will simply use an already-working solution.

p0wny is a php script that will allow you to get access to the server's terminal, check it out: https://github.com/flozz/p0wny-shell

The only file we will need is "shell.php". Let's upload it and then navigate to it. Don't forget to match your IP address, port, and file name. 

```
https://192.168.0.5:4443/shell.php
```

We now have access to the server's terminal as nginx's user.

>> IMG 4

Unfortunely, we can't really find the flag here, so we need to navigate on the system. Changing our directory to www-data's home directory, then listing the files there, we will see flag2.txt.

```
cd
ls
cat flag2.txt
```

<details>
    <summary>Let's see what's inside of it</summary>
    <pre><code>
    flag2: BforBodyNotBook-ofKnowledge

    You got the flag! Now it's time to escalate...

    You need to become root using your p0wny shell, but you can't seem to type in your password...
</code></pre>

</details>

## Flag 3
Let's try escalating then! Why not starting with `sudo`?

```
www-data@fc1b13fe1365:/var/www# sudo ls /root
sh: 1: sudo: not found
```

Unfortunetely, `sudo` doesn't seem to work. How about we simply try to switch user with `su`?

```
www-data@fc1b13fe1365:/var/www# su 
Password: su: Authentication failure
```

Although `su` worked, the terminal doesn't prompt us for the password, maybe there is a way to provide that password in a one-liner?

```
www-data@fc1b13fe1365:/var/www# echo "thispasswordishuge!" | su - root
Password:
www-data@fc1b13fe1365:/var/www#
```

So this time we got no `Authentication failure`, so lucky us that the owner of this system decided to reuse his password. But if you check the user, it is still the same. Let's see if we can pass any command to that user.

```
www-data@fc1b13fe1365:/var/www# echo "thispasswordishuge!" | su - root -c "ls"
Password: flag3.txt
```

The prompt is definitely a bit weird, but we just listed items on root. Let's also read it with `cat`!

```
www-data@fc1b13fe1365:/var/www# echo "thispasswordishuge!" | su - root -c "ls; cat flag3.txt"
Password: flag3.txt
flag3: plzM477letU5pass

You got the last flag! Wasn't that easy?
```

Hope you enjoyed this challenge as much as we did!


# More Studies
If you want to go deeper into what you practiced in this Challenge, check some recommendations.

## Reverse Shell scripts
A reverse shell script was used in this challenge to gain access to the target machine. Although it was used to simulate an attack, these scripts can be used with no ill intentions.

Besides that, reverse shell scripts can be programmed in different languages, and even customized to your own project. Check some by yourself!

## Brute force tools
Bruteforce is a well known strategy that consists in trying over and over different combinations until you get the right one.

Although we use a directory brute force in this Challenge, there are many other types of brute force tools, the most common being password crackers. But also give it a try to explore other tools that interact with DNS and even biometrics. 

