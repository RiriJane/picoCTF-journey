<h1>Python Wrangling - PicoCTF 2021</h1>

<b>Points :<b> 10 points

Link : https://play.picoctf.org/practice/challenge/166?category=5&page=1

<h1>Problem</h1>

Python scripts are invoked kind of like programs in the Terminal... Can you run this Python script using this password to get the flag?

<h1>Solution<h1>

1. View each file  ``` cat <name-of-file>```
    - ende.py: script of instructions
    - flag.txt.en: .en file means it's encrypted. By using the cat command, it shows random characters and numbers.
    - pw.txt: some random characters.
2. First execution of ende.py result:
```
─$ python3 ende.py 
Usage: ende.py (-e/-d) [file]

```
    - This indicates to use flags -e or -d and it is requiring a file afterwards. 
    - By using the flag -h, it indicates how to decrypt a file : ```python ende.py -d pole.txt```

3. Executing ende.py with -d flag:
```
python3 ende.py -d flag.txt.en
```
- This command will prompt a password.
4. Using cat command to show password. Copy and paste the password and use it for step 3.