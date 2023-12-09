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

<details>
    <summary>By checking its content we will find the first flag!</summary>
    >> flag1: Pr0Jmngmnt15c00l
    >> User: admin
    >> Password: thispasswordishuge!
    >> You got the flag! What a place for a password to be, right? :P
    >> How much can you do with your new admin account? There must be some way to control the forum. 
</details>


## Flag 2


## Flag 3



# More Studies
If you want to go deeper into what you practiced in this Challenge, check some recommendations.

## Reverse Shell scripts
A reverse shell script was used in this challenge to gain access to the target machine. Although it was used to simulate an attack, these scripts can be used with no ill intentions.

Besides that, reverse shell scripts can be programmed in different languages, and even customized to your own project. Check some by yourself!

## Brute force tools
Bruteforce is a well known strategy that consists in trying over and over different combinations until you get the right one.

Although we use a directory brute force in this Challenge, there are many other types of brute force tools, the most common being password crackers. But also give it a try to explore other tools that interact with DNS and even biometrics. 

