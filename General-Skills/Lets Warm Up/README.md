<h1>Lets Warm Up - PicoCTF 2019</h1>

<b>Points</b>: 50 points

link: https://play.picoctf.org/practice/challenge/22?category=5&page=1

<h1>Problem</h1>

If I told you a word started with 0x70 in hexadecimal, what would it start with in ASCII?

<h1>Solution</h1>

Convert the hexadecimal to ASCII using <b><i>printf</i></b> command :

```
┌──(riri㉿nb-riri)-[~]
└─$ printf '\x70'
p  
```

Obviously, writing just 'p' would not work. It has to be in the format of a flag which is picoCTF{answer-here}.

Good luck !

