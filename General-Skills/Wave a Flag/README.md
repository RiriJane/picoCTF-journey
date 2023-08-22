<h1>Wave a flag - PicoCTF 2021</h1>

<b>Points</b>: 10 points

<h1>Problem</h1>

Can you invoke help flags for a tool or binary? This program has extraordinarily helpful information...

<h1>Solution</h1>

I downloaded the file and went to the folder.

I tried executing the file :

```
┌──(riri㉿nb-riri)-[~/Downloads]
└─$ warm
Command 'warm' not found, did you mean:
  command 'worm' from deb bsdgames (2.17-29)
  command 'swarm' from deb swarm (3.1.0+dfsg-1)
  command 'warp' from deb libghc-wai-app-static-dev (3.1.7.1-1build5.1)
  command 'warg' from deb clonalorigin (1.0-6build1)
Try: sudo apt install <deb name>

```

Unfortunately, since it's not a command. My shell doesn't recognized. I proceed by executing it in this way:

```
┌──(riri㉿nb-riri)-[~/Downloads]
└─$ ./warm

```

Obviously, that was too easy! I got permission denied. :

```
┌──(riri㉿nb-riri)-[~/Downloads]
└─$ ./warm
zsh: permission denied: ./warm

```

I changed the permission with the command chmod :

```
┌──(riri㉿nb-riri)-[~/Downloads]
└─$ chmod +x warm

```

And re-executed it :

```
┌──(riri㉿nb-riri)-[~/Downloads]
└─$ ./warm       
Hello user! Pass me a -h to learn what I can do!

```

As it indicates, I added the flag -h and it gave me the flag! 

```
┌──(riri㉿nb-riri)-[~/Downloads]
└─$ ./warm -h
Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_755f3544}

```