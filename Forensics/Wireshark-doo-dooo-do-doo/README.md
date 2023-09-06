<h1>Wireshark doo dooo do doo... - PicoCTF 2021</h1>

<b>Points</b>: 50 points

link: [https://play.picoctf.org/practice/challenge/186?category=4&page=1](https://play.picoctf.org/practice/challenge/115?category=4&page=1)

<h1>Problem</h1>
Can you find the flag? [shark1.pcapng](https://mercury.picoctf.net/static/ea41c400c3c7b4a63406e5e607d362ab/shark1.pcapng).

<h1>Solution</h1>

After downloading the file with the command <i>wget</i>, I opened it with Wireshark application since it is a .pcapng file.
By looking at a few lines, there are a lot of HTTP traffic. I proceeded by filtering with a HTTP response code 200 :

```
http.respones.code = 200
```

This resulted in keberos encrypted traffic except for 2 packets which are text/html and text/plain. One of the packets had a line-based text data that looked like a flag but with randoms characters.

![packet with a flag](https://github.com/RiriJane/picoCTF-journey/blob/main/Forensics/Wireshark-doo-dooo-do-doo/packet-with-flag.PNG)

I checked the PicoCTF primer to learn more about encryption and the first subject was about [Caeser Cipher](https://primer.picoctf.org/#_substitution_ciphers). I made a python file to decrypt the flag but to no success.

I searched online if there were any terminal command to decrypt the flag and I found this [repository](https://gist.github.com/IQAndreas/030b8e91a8d9a407caa6) but it didn't work. I tried looking for more information and found [this](https://askubuntu.com/questions/1097761/changing-individual-letter-position-with-bash).
```
echo "Gur synt vf cvpbPGS{c33xno00_1_f33_h_qrnqorrs}\n" | tr '[n-za-mN-ZA-M]' '[a-zA-Z]'
```

```
ririjane-picoctf@webshell:~$ echo "Gur synt vf cvpbPGS{c33xno00_1_f33_h_qrnqorrs}\n" | tr '[n-za-mN-ZA-M]' '[a-zA-Z]'
The flag is picoCTF{p33kab00_1_s33_u_deadbeef}\a
```
<h1>Flag</h1>

picoCTF{p33kab00_1_s33_u_deadbeef}

