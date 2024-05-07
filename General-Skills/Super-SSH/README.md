<h1>Information - PicoCTF 2024</h1>
Points: 25 points

link: https://play.picoctf.org/practice/challenge/424?category=5&page=1

<h1>Problem</h1>
Using a Secure Shell (SSH) is going to be pretty important.
Additional details will be available after launching your challenge instance.

<h1>Solution</h1>

1. Start instance.

2. You will be given a username, a domain and a port.

```
cuddlebug-picoctf@webshell:~$ ssh ctf-player@titan.picoctf.net -p 56439
The authenticity of host '[titan.picoctf.net]:56439 ([3.139.174.234]:56439)' can't be established.
ED25519 key fingerprint is SHA256:4S9EbTSSRZm32I+cdM5TyzthpQryv5kudRP9PIKT7XQ.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[titan.picoctf.net]:56439' (ED25519) to the list of known hosts.
ctf-player@titan.picoctf.net's password: 
Welcome ctf-player, here's your flag: picoCTF{s3cur3_c0nn3ct10n_8969f7d3}
Connection to titan.picoctf.net closed.
cuddlebug-picoctf@webshell:~$ 
```
