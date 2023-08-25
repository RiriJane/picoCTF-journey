<h1>Information - PicoCTF 2021</h1>

<b>Points</b>: 10 points

link: https://play.picoctf.org/practice/challenge/186?category=4&page=1

<h1>Problem</h1>
Files can always be changed in a secret way. Can you find the flag? cat.jpg

<h1>Solution</h1>
I used exiftool to dig into the metadata of the image:

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

After looking through all these data, we can definitely tell that it is a .jpg file. I could have used the <i>file</i> command to check but since I know that the exiftool also provide this information, I immediately used this tool. It also gives the information of the execution permission. Here it is not executable. 

There are two promising information : Current IPTC Digest and License. The current IPTC Digest made me think about SHA-256 Hash but since we don't have the hash stored, I skipped this part and converted the License value with the <i>base64</i> command :

```
┌──(riri㉿nb-riri)-[~/Downloads]
└─$ echo cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9 | base64 -d
picoCTF{the_m3tadata_1s_modified} 
```

<h1>Flag</h1>
picoCTF{the_m3tadata_1s_modified} 
