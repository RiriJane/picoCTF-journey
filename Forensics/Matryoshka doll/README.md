<h1>Matryoshka Doll - PicoCTF 2021</h1>

<b>Points</b>: 30 points

link: https://play.picoctf.org/practice/challenge/129?category=4&page=1

<h1>Problem</h1>
Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one? Image: [this](https://play.picoctf.org/practice/challenge/129?category=4&page=1)

<h1>Solution</h1>
Since the problem indicates that there are images hidden, I used the command <i>binwalk</i> to extract the hidden images.

Checking if there is a file hidden:

```
┌──(riri㉿nb-riri)-[~/Downloads]
└─$ binwalk dolls.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 594 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378954, uncompressed size: 383940, name: base_images/2_c.jpg
651612        0x9F15C         End of Zip archive, footer length: 22

```

With result given, it confirms that there is a hidden image. First extraction:

```
┌──(riri㉿nb-riri)-[~/Downloads]
└─$ binwalk -e dolls.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 594 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378954, uncompressed size: 383940, name: base_images/2_c.jpg
651612        0x9F15C         End of Zip archive, footer length: 22

```

After extracting the hidden image, I checked the files extracted and found another image: 


```
┌──(riri㉿nb-riri)-[~/Downloads/_dolls.jpg.extracted/base_images]
└─$ ls
2_c.jpg
         
```

I repeated these steps until I got the flag. The flag is in .txt file and hidden in the last image:

```
┌──(riri㉿nb-riri)-[~/…/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images]
└─$ binwalk 4_c.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 320 x 768, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
79578         0x136DA         Zip archive data, at least v2.0 to extract, compressed size: 64, uncompressed size: 81, name: flag.txt
79786         0x137AA         End of Zip archive, footer length: 22

```

Once this file is extracted, I used the command <i>cat</i> to display the flag:

```
┌──(riri㉿nb-riri)-[~/…/base_images/_3_c.jpg.extracted/base_images/_4_c.jpg.extracted]
└─$ cat flag.txt 
picoCTF{e3f378fe6c1ea7f6bc5ac2c3d6801c1f} 
```

<h1>Flag</h1>

picoCTF{e3f378fe6c1ea7f6bc5ac2c3d6801c1f}
