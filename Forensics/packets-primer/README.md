<h1>Packets Primer - PicoCTF 2022</h1>

<b>Points</b>: 100 points

link: https://play.picoctf.org/practice/challenge/286?category=4&page=2

<h1>Problem</h1>
Download the packet capture file and use packet analysis software to find the flag. [Download packet capture.](https://artifacts.picoctf.net/c/195/network-dump.flag.pcap)

<h1>Solution</h1>
After downloading the file, I opened it up with [WireShark](https://www.geeksforgeeks.org/how-to-install-and-use-wireshark-on-ubuntu-linux/). There are 9 packets. I analysed the lines briefly (Protocols used or if there is anything unusual. Looks normal.

![]()

Then, I looked at the protocol hierarchy. I find that there is data. I used this as filter and it gave me one result. By opening it up, it shows the flag.




```
```
<h1>Flag</h1>

p i c o C T F { p 4 c k 3 7 _ 5 h 4 r k _ b 9 d 5 3 7 6 5 }
