Hards shells

Description :
After a recent hack, a laptop was seized and subsequently analyzed. The victim of the hack? An innocent mexican restaurant. During the investigation they found this suspicous file. Can you find any evidence that the owner of this laptop is the culprit?

Resolution

We download a file called hardshells , we have to determine his type

``` shell
file hardshell

hardshells: Zip archive data, at least v1.0 to extract
```

We try to extract this Zip archive , but it ask us a password .

```
# -D use bruteforce dictionnary
#-p dictionnary file 
#-u try unzip
fcrackzip -D -p rockyou.txt -u hardshells.zip

PASSWORD FOUND!!!!: pw == tacos
```

Now we have a folder called _hardshells.extracted with a file called d inside

- _hardshells.extracted
	- d
	
Now try to find file type of d

```
file d

d: Minix filesystem, V1, 30 char names, 20 zones
```

We have to mount the minix file system .

```
mkdir minix
mount -o loop -t minix d /mnt/minix
cd /mnt/minix
``

We can see a file called dat inside the mount point .
The file command on dat says us data.

Try to hex edit this file in order to have more information

00000000  89 50 55 47  0D 0A 1A 0A   00 00 00 0D  49 48 44 52   .PUG........IHDR
00000010  00 00 07 80  00 00 04 38   08 06 00 00  00 E8 D3 C1   .......8........
00000020  43 00 00 20  00 49 44 41   54 78 9C EC  DD 79 78 54   C.. .IDATx...yxT
...
...
0004D9C0  00 00 00 00  49 45 4E 44   AE 42 60 82  0A            ....IEND.B`..


It's possible that's dat is an PNG file .
Modify PUG with PNG and try to open the image

IceCTF{look_away_i_am_hacking}
