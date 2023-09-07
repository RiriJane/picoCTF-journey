<h1>File Types - PicoCTF 2022</h1>

<b>Points</b>: 100 points

link: https://play.picoctf.org/practice/challenge/268?category=4&page=1 

<h1>Problem</h1>
This file was found among some files marked confidential but my pdf reader cannot read it, maybe yours can.
You can download the file from [here](https://artifacts.picoctf.net/c/81/Flag.pdf). 


<h1>Solution</h1>
Download the file :

```
ririjane-picoctf@webshell:~/file-types$ wget https://artifacts.picoctf.net/c/81/Flag.pdf


--2023-09-07 13:08:40--  https://artifacts.picoctf.net/c/81/Flag.pdf
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.93, 3.160.5.71, 3.160.5.18, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.93|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 5161 (5.0K) [application/octet-stream]
Saving to: 'Flag.pdf'

Flag.pdf                                     100%[===========================================================================================>]   5.04K  --.-KB/s    in 0s      

2023-09-07 13:08:40 (72.4 MB/s) - 'Flag.pdf' saved [5161/5161]
```

Check the file type:

```
ririjane-picoctf@webshell:~/file-types$ file Flag.pdf


Flag.pdf: shell archive text
```

Rename file type to shell:
```
ririjane-picoctf@webshell:~/file-types$ cp Flag.pdf Flag.sh
```

Check if the file is exectuable :
```
ririjane-picoctf@webshell:~/file-types$ ls -l

total 16
-rw-rw-r-- 1 ririjane-picoctf ririjane-picoctf 5161 Mar 16 03:16 Flag.pdf
-rw-rw-r-- 1 ririjane-picoctf ririjane-picoctf 5161 Sep  7 13:09 Flag.sh
```

Make the file executable:
```
ririjane-picoctf@webshell:~/file-types$ chmod +x Flag.sh 
ririjane-picoctf@webshell:~/file-types$ ls -l
total 16
-rw-rw-r-- 1 ririjane-picoctf ririjane-picoctf 5161 Mar 16 03:16 Flag.pdf
-rwxrwxr-x 1 ririjane-picoctf ririjane-picoctf 5161 Sep  7 13:09 Flag.sh
```

I then executed the file:
```
ririjane-picoctf@webshell:~/file-types$ ./Flag.sh 
x - created lock directory _sh00046.
x - extracting flag (text)
x - removed lock directory _sh00046.
```

It indicates that a flag has been extracted. Check the type of the file:
```
ririjane-picoctf@webshell:~/file-types$ file flag
flag: current ar archive
```
Extract data and go in the extracted files:
```
ririjane-picoctf@webshell:~/file-types$ binwalk -e flag

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
100           0x64            bzip2 compressed data, block size = 900k

ririjane-picoctf@webshell:~/file-types$ ls -l
total 20
-rw-rw-r-- 1 ririjane-picoctf ririjane-picoctf 5161 Mar 16 03:16 Flag.pdf
-rwxrwxr-x 1 ririjane-picoctf ririjane-picoctf 5161 Sep  7 13:09 Flag.sh
drwxrwxr-x 2 ririjane-picoctf ririjane-picoctf   16 Sep  7 13:20 _flag.extracted
-rw-r--r-- 1 ririjane-picoctf ririjane-picoctf 1092 Mar 16 01:40 flag
ririjane-picoctf@webshell:~/file-types$ cd _flag.extracted/
```

Check out the files:
```
ririjane-picoctf@webshell:~/file-types/_flag.extracted$ ls
64
ririjane-picoctf@webshell:~/file-types/_flag.extracted$ file 64
64: gzip compressed data, was "flag", last modified: Thu Mar 16 01:40:17 2023, from Unix, original size modulo 2^32 327
```

Unzip data and go in to the files:
```
ririjane-picoctf@webshell:~/file-types/_flag.extracted$ ls
64
ririjane-picoctf@webshell:~/file-types/_flag.extracted$ file 64
64: gzip compressed data, was "flag", last modified: Thu Mar 16 01:40:17 2023, from Unix, original size modulo 2^32 327
```
Check the file of flag:
```
ririjane-picoctf@webshell:~/file-types/_flag.extracted/_64.extracted$ file flag
flag: lzip compressed data, version: 1
```
Unzip with lzip and check new file:
```
ririjane-picoctf@webshell:~/file-types/_flag.extracted/_64.extracted$ lzip -d flag
ririjane-picoctf@webshell:~/file-types/_flag.extracted/_64.extracted$ ls
flag.gz  flag.out
ririjane-picoctf@webshell:~/file-types/_flag.extracted/_64.extracted$ file flag.out
flag.out: LZ4 compressed data (v1.4+)
```
Decompress with LZ4 and check new file:
```
ririjane-picoctf@webshell:~/file-types/_flag.extracted/_64.extracted$ lz4 -d flag.out flag2
flag.out             : decoded 265 bytes                                       
ririjane-picoctf@webshell:~/file-types/_flag.extracted/_64.extracted$ ls
flag.gz  flag.out  flag2
ririjane-picoctf@webshell:~/file-types/_flag.extracted/_64.extracted$ file flag2
flag2: LZMA compressed data, non-streamed, size 254
```

Decompress with LZMA, check new file:
```
ririjane-picoctf@webshell:~/file-types/_flag.extracted/_64.extracted$ lzma -d flag2.lzma
lzma: flag2: File exists
```
Add -f to overwrite the old flag2, then check new file:
```
ririjane-picoctf@webshell:~/file-types/_flag.extracted/_64.extracted$ lzma -d flag2.lzma -f   
ririjane-picoctf@webshell:~/file-types/_flag.extracted/_64.extracted$ ls
flag.gz  flag.out  flag2
ririjane-picoctf@webshell:~/file-types/_flag.extracted/_64.extracted$ file flag2
flag2: lzop compressed data - version 1.040, LZO1X-1, os: Unix
```
Note: I had to use my personal shell since PicoCTF's webshell does not have lzop installed... A little detour.

Send file to web browser and save:
```
ririjane-picoctf@webshell:~$ sz flag2
```

Decompress with lzop and check file:
```
┌──(riri㉿nb-riri)-[~/CTF/file-types]
└─$ lzop -d flag2 -o flag3
┌──(riri㉿nb-riri)-[~/CTF/file-types]
└─$ ls
flag2  flag3
┌──(riri㉿nb-riri)-[~/CTF/file-types]
└─$ file flag3
flag3: lzip compressed data, version: 1
```
Decompress with lzip and check new file:
```
┌──(riri㉿nb-riri)-[~/CTF/file-types]
└─$ lzip -d flag3 -o flag4
                                                                                
┌──(riri㉿nb-riri)-[~/CTF/file-types]
└─$ ls
flag2  flag3  flag4
                                                                                
┌──(riri㉿nb-riri)-[~/CTF/file-types]
└─$ file flag4
flag4: XZ compressed data, checksum CRC64

```

Decompress with XZ and check new file:
```
┌──(riri㉿nb-riri)-[~/CTF/file-types]
└─$ xz -d flag4      
xz: flag4: Filename has an unknown suffix, skipping

```

Add .xz to the end of the file:
```
┌──(riri㉿nb-riri)-[~/CTF/file-types]
└─$ cp flag4 flag4.xz
```

Decompress with XZ:
```
┌──(riri㉿nb-riri)-[~/CTF/file-types]
└─$ xz -d flag4.xz
xz: flag4: File exists
```

So, I used the <i>help</i> tag to see if I can write a new file:
```
┌──(riri㉿nb-riri)-[~/CTF/file-types]
└─$ xz -h
Usage: xz [OPTION]... [FILE]...
Compress or decompress FILEs in the .xz format.

  -z, --compress      force compression
  -d, --decompress    force decompression
  -t, --test          test compressed file integrity
  -l, --list          list information about .xz files
  -k, --keep          keep (don't delete) input files
  -f, --force         force overwrite of output file and (de)compress links
  -c, --stdout        write to standard output and don't delete input files
  -0 ... -9           compression preset; default is 6; take compressor *and*
                      decompressor memory usage into account before using 7-9!
  -e, --extreme       try to improve compression ratio by using more CPU time;
                      does not affect decompressor memory requirements
  -T, --threads=NUM   use at most NUM threads; the default is 1; set to 0
                      to use as many threads as there are processor cores
  -q, --quiet         suppress warnings; specify twice to suppress errors too
  -v, --verbose       be verbose; specify twice for even more verbose
  -h, --help          display this short help and exit
  -H, --long-help     display the long help (lists also the advanced options)
  -V, --version       display the version number and exit

With no FILE, or when FILE is -, read standard input.

Report bugs to <lasse.collin@tukaani.org> (in English or Finnish).
XZ Utils home page: <https://tukaani.org/xz/>
```

I tried the -c tag:
```
┌──(riri㉿nb-riri)-[~/CTF/file-types]
└─$ xz -d -c flag4.xz
7069636f4354467b66316c656e406d335f6d406e3170756c407431306e5f
6630725f3062326375723137795f37396230316332367d0a
```

By looking carefully at the characters, it looks like hex. Little internet [search](https://safjan.com/bash-encode-decode-base64-and-hex/) to decode hex and voilà:
```
┌──(riri㉿nb-riri)-[~/CTF/file-types]
└─$ echo "7069636f4354467b66316c656e406d335f6d406e3170756c407431306e5f
6630725f3062326375723137795f37396230316332367d0a" | xxd -r -p
picoCTF{f1len@m3_m@n1pul@t10n_f0r_0b2cur17y_79b01c26}
```

<h1>Flag</h1>

picoCTF{f1len@m3_m@n1pul@t10n_f0r_0b2cur17y_79b01c26}
