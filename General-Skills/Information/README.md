<h1>Information - PicoCTF 2021</h1>

<b>Points</b>: 10 points

link: https://play.picoctf.org/practice/challenge/186?category=4&page=1

<h1>Problem</h1>

Files can always be changed in a secret way. Can you find the flag? cat.jpg

<h1>Solution</h1>

I used the exiftool to dig into the metadata of the image :
```
┌──(riri㉿nb-riri)-[~/Downloads]

└─$ exiftool cat.jpg

ExifTool Version Number         : 12.40

File Name                       : cat.jpg

Directory                       : .

File Size                       : 858 KiB

File Modification Date/Time     : 2023:08:25 14:33:36+02:00

File Access Date/Time           : 2023:08:25 14:43:04+02:00

File Inode Change Date/Time     : 2023:08:25 14:42:58+02:00

File Permissions                : -rw-rw-r--

File Type                       : JPEG

File Type Extension             : jpg

MIME Type                       : image/jpeg

JFIF Version                    : 1.02

Resolution Unit                 : None

X Resolution                    : 1

Y Resolution                    : 1

Current IPTC Digest             : 7a78f3d9cfb1ce42ab5a3aa30573d617

Copyright Notice                : PicoCTF

Application Record Version      : 4

XMP Toolkit                     : Image::ExifTool 10.80

License                         : cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9

Rights                          : PicoCTF

Image Width                     : 2560

Image Height                    : 1598

Encoding Process                : Baseline DCT, Huffman coding

Bits Per Sample                 : 8

Color Components                : 3

Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)

Image Size                      : 2560x1598

Megapixels                      : 4.1

```
From the information collected, we can tell that it is definitely a .jpg file. There are two elements that look promising : Current IPTC Digest and License.

I converted each to base64. The first one gave me unreadable characters :
```
┌──(riri㉿nb-riri)-[~/Downloads]
└─$ echo 7a78f3d9cfb1ce42ab5a3aa30573d617 | base64 -d
���w}q��q�6i�Zݦ�Ӟ�w�{  
```

But the second one gave the me flag :
```
┌──(riri㉿nb-riri)-[~/Downloads]
└─$ echo cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9 | base64 -d
picoCTF{the_m3tadata_1s_modified} 
```

<h1>Flag</h1>

picoCTF{the_m3tadata_1s_modified} 

