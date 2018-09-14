# Locked Out

## Description

This is a fancy looking lock, I wonder what would happen if you broke it open?

## Resolution

We analyse the structure of directory 
```sh
[adversary ~]$ ls -l
total 8
drwxr-xr-x. 2 root root 4096 Sep 11 11:04 lockedout

[adversary ~]$ cd lockedout

[adversary ~/lockedout]$ ls -l
total 20
-r--r-----. 1 root drevil   27 Sep 11 11:04 flag.txt
-rwxr-sr-x. 1 root drevil 5628 Sep 11 11:04 lock

[adversary ~/lockedout]$ ./lock
This is a pesky lock.. do you think you can open it?
Enter key:
```
We have an suid elf lock and file called flag.txt

It ask us a key so let's try to find it .


####################################################################################################################
lock:     format de fichier elf32-i386


Déassemblage de la section .text :

00000670 <main@@Base>:
 670:	8d 4c 24 04          	lea    ecx,[esp+0x4]
 674:	83 e4 f0             	and    esp,0xfffffff0
 677:	ff 71 fc             	push   DWORD PTR [ecx-0x4]
 67a:	55                   	push   ebp
 67b:	89 e5                	mov    ebp,esp
 67d:	56                   	push   esi
 67e:	53                   	push   ebx
 67f:	e8 ec 00 00 00       	call   770 <main@@Base+0x100>
 684:	81 c3 7c 19 00 00    	add    ebx,0x197c
 68a:	51                   	push   ecx
 68b:	8d b5 e8 fe ff ff    	lea    esi,[ebp-0x118]
 691:	8d 83 30 ea ff ff    	lea    eax,[ebx-0x15d0]
 697:	81 ec 18 01 00 00    	sub    esp,0x118
 69d:	50                   	push   eax
 69e:	e8 4d ff ff ff       	call   5f0 <puts@plt>
 6a3:	8d 83 0b ea ff ff    	lea    eax,[ebx-0x15f5]
 6a9:	89 04 24             	mov    DWORD PTR [esp],eax
 6ac:	e8 ef fe ff ff       	call   5a0 <printf@plt>
 6b1:	8b 83 f0 ff ff ff    	mov    eax,DWORD PTR [ebx-0x10]
 6b7:	83 c4 0c             	add    esp,0xc
 6ba:	ff 30                	push   DWORD PTR [eax]
 6bc:	68 00 01 00 00       	push   0x100
 6c1:	56                   	push   esi
 6c2:	e8 09 ff ff ff       	call   5d0 <fgets@plt>
 6c7:	83 c4 10             	add    esp,0x10                           ;break *0x565556c7
 6ca:	85 c0                	test   eax,eax                           ; test ET logique
 6cc:	74 39                	je     707 <main@@Base+0x97>
 6ce:	8d 83 17 ea ff ff    	lea    eax,[ebx-0x15e9]
 6d4:	83 ec 08             	sub    esp,0x8
 6d7:	50                   	push   eax                                ; pointeur sur la chaine \n
 6d8:	56                   	push   esi                                ; pointeur sur sur la chaine saisie
 6d9:	e8 d2 fe ff ff       	call   5b0 <strcspn@plt>                  ; permet le calcul de la longueur de la chaine saisie
                                                                          ; eax offset emplacement \n chaine saisie
 6de:	89 34 24             	mov    DWORD PTR [esp],esi
 6e1:	c6 84 05 e8 fe ff ff 	mov    BYTE PTR [ebp+eax*1-0x118],0x0
 6e8:	00 
 6e9:	e8 32 02 00 00       	call   920 <main@@Base+0x2b0>
 6ee:	83 c4 10             	add    esp,0x10
 6f1:	85 c0                	test   eax,eax
 6f3:	74 1f                	je     714 <main@@Base+0xa4>
 6f5:	8d 83 23 ea ff ff    	lea    eax,[ebx-0x15dd]
 6fb:	83 ec 0c             	sub    esp,0xc
 6fe:	50                   	push   eax
 6ff:	e8 ec fe ff ff       	call   5f0 <puts@plt>
 704:	83 c4 10             	add    esp,0x10
 707:	8d 65 f4             	lea    esp,[ebp-0xc]
 70a:	31 c0                	xor    eax,eax
 70c:	59                   	pop    ecx
 70d:	5b                   	pop    ebx
 70e:	5e                   	pop    esi
 70f:	5d                   	pop    ebp
 710:	8d 61 fc             	lea    esp,[ecx-0x4]
 713:	c3                   	ret    
 


714:	8d 83 19 ea ff ff    	lea    eax,[ebx-0x15e7]
 71a:	83 ec 0c             	sub    esp,0xc
 71d:	50                   	push   eax
 71e:	e8 cd fe ff ff       	call   5f0 <puts@plt>
 723:	e8 78 01 00 00       	call   8a0 <main@@Base+0x230>
 728:	83 c4 10             	add    esp,0x10
 72b:	eb da                	jmp    707 <main@@Base+0x97>
 72d:	31 ed                	xor    ebp,ebp
 72f:	5e                   	pop    esi
 730:	89 e1                	mov    ecx,esp
 732:	83 e4 f0             	and    esp,0xfffffff0
 735:	50                   	push   eax
 736:	54                   	push   esp
 737:	52                   	push   edx
 738:	e8 22 00 00 00       	call   75f <main@@Base+0xef>
 73d:	81 c3 c3 18 00 00    	add    ebx,0x18c3
 743:	8d 83 e0 e9 ff ff    	lea    eax,[ebx-0x1620]
 749:	50                   	push   eax
 74a:	8d 83 80 e9 ff ff    	lea    eax,[ebx-0x1680]
 750:	50                   	push   eax
 751:	51                   	push   ecx
 752:	56                   	push   esi
 753:	ff b3 f4 ff ff ff    	push   DWORD PTR [ebx-0xc]
 759:	e8 c2 fe ff ff       	call   620 <__libc_start_main@plt>
 75e:	f4                   	hlt    
 75f:	8b 1c 24             	mov    ebx,DWORD PTR [esp]
 762:	c3                   	ret    
 763:	66 90                	xchg   ax,ax
 765:	66 90                	xchg   ax,ax
 767:	66 90                	xchg   ax,ax
 769:	66 90                	xchg   ax,ax
 76b:	66 90                	xchg   ax,ax
 76d:	66 90                	xchg   ax,ax
 76f:	90                   	nop
 


770:	8b 1c 24             	mov    ebx,DWORD PTR [esp]
 773:	c3                   	ret    
 

774:	66 90                	xchg   ax,ax
 776:	66 90                	xchg   ax,ax
 778:	66 90                	xchg   ax,ax
 77a:	66 90                	xchg   ax,ax
 77c:	66 90                	xchg   ax,ax
 77e:	66 90                	xchg   ax,ax
 780:	e8 17 01 00 00       	call   89c <main@@Base+0x22c>
 785:	81 c2 7b 18 00 00    	add    edx,0x187b
 78b:	8d 8a 4c 00 00 00    	lea    ecx,[edx+0x4c]
 791:	8d 82 4f 00 00 00    	lea    eax,[edx+0x4f]
 797:	29 c8                	sub    eax,ecx
 799:	83 f8 06             	cmp    eax,0x6
 79c:	76 17                	jbe    7b5 <main@@Base+0x145>
 79e:	8b 82 e4 ff ff ff    	mov    eax,DWORD PTR [edx-0x1c]
 7a4:	85 c0                	test   eax,eax
 7a6:	74 0d                	je     7b5 <main@@Base+0x145>
 7a8:	55                   	push   ebp
 7a9:	89 e5                	mov    ebp,esp
 7ab:	83 ec 14             	sub    esp,0x14
 7ae:	51                   	push   ecx
 7af:	ff d0                	call   eax
 7b1:	83 c4 10             	add    esp,0x10
 7b4:	c9                   	leave  
 7b5:	f3 c3                	repz ret 
 7b7:	89 f6                	mov    esi,esi
 7b9:	8d bc 27 00 00 00 00 	lea    edi,[edi+eiz*1+0x0]
 7c0:	e8 d7 00 00 00       	call   89c <main@@Base+0x22c>
 7c5:	81 c2 3b 18 00 00    	add    edx,0x183b
 7cb:	55                   	push   ebp
 7cc:	8d 8a 4c 00 00 00    	lea    ecx,[edx+0x4c]
 7d2:	8d 82 4c 00 00 00    	lea    eax,[edx+0x4c]
 7d8:	89 e5                	mov    ebp,esp
 7da:	53                   	push   ebx
 7db:	29 c8                	sub    eax,ecx
 7dd:	c1 f8 02             	sar    eax,0x2
 7e0:	83 ec 04             	sub    esp,0x4
 7e3:	89 c3                	mov    ebx,eax
 7e5:	c1 eb 1f             	shr    ebx,0x1f
 7e8:	01 d8                	add    eax,ebx
 7ea:	d1 f8                	sar    eax,1
 7ec:	74 14                	je     802 <main@@Base+0x192>
 7ee:	8b 92 fc ff ff ff    	mov    edx,DWORD PTR [edx-0x4]
 7f4:	85 d2                	test   edx,edx
 7f6:	74 0a                	je     802 <main@@Base+0x192>
 7f8:	83 ec 08             	sub    esp,0x8
 7fb:	50                   	push   eax
 7fc:	51                   	push   ecx
 7fd:	ff d2                	call   edx
 7ff:	83 c4 10             	add    esp,0x10
 802:	8b 5d fc             	mov    ebx,DWORD PTR [ebp-0x4]
 805:	c9                   	leave  
 806:	c3                   	ret    
 807:	89 f6                	mov    esi,esi
 809:	8d bc 27 00 00 00 00 	lea    edi,[edi+eiz*1+0x0]
 810:	55                   	push   ebp
 811:	89 e5                	mov    ebp,esp
 813:	53                   	push   ebx
 814:	e8 57 ff ff ff       	call   770 <main@@Base+0x100>
 819:	81 c3 e7 17 00 00    	add    ebx,0x17e7
 81f:	83 ec 04             	sub    esp,0x4
 822:	80 bb 4c 00 00 00 00 	cmp    BYTE PTR [ebx+0x4c],0x0
 829:	75 27                	jne    852 <main@@Base+0x1e2>
 82b:	8b 83 e8 ff ff ff    	mov    eax,DWORD PTR [ebx-0x18]
 831:	85 c0                	test   eax,eax
 833:	74 11                	je     846 <main@@Base+0x1d6>
 835:	83 ec 0c             	sub    esp,0xc
 838:	ff b3 44 00 00 00    	push   DWORD PTR [ebx+0x44]
 83e:	e8 1d fe ff ff       	call   660 <__cxa_finalize@plt>
 843:	83 c4 10             	add    esp,0x10
 846:	e8 35 ff ff ff       	call   780 <main@@Base+0x110>
 84b:	c6 83 4c 00 00 00 01 	mov    BYTE PTR [ebx+0x4c],0x1
 852:	8b 5d fc             	mov    ebx,DWORD PTR [ebp-0x4]
 855:	c9                   	leave  
 856:	c3                   	ret    
 857:	89 f6                	mov    esi,esi
 859:	8d bc 27 00 00 00 00 	lea    edi,[edi+eiz*1+0x0]
 860:	e8 37 00 00 00       	call   89c <main@@Base+0x22c>
 865:	81 c2 9b 17 00 00    	add    edx,0x179b
 86b:	8d 82 f0 fe ff ff    	lea    eax,[edx-0x110]
 871:	8b 08                	mov    ecx,DWORD PTR [eax]
 873:	85 c9                	test   ecx,ecx
 875:	75 09                	jne    880 <main@@Base+0x210>
 877:	e9 44 ff ff ff       	jmp    7c0 <main@@Base+0x150>
 87c:	8d 74 26 00          	lea    esi,[esi+eiz*1+0x0]
 880:	8b 92 f8 ff ff ff    	mov    edx,DWORD PTR [edx-0x8]
 886:	85 d2                	test   edx,edx
 888:	74 ed                	je     877 <main@@Base+0x207>
 88a:	55                   	push   ebp
 88b:	89 e5                	mov    ebp,esp
 88d:	83 ec 14             	sub    esp,0x14
 890:	50                   	push   eax
 891:	ff d2                	call   edx
 893:	83 c4 10             	add    esp,0x10
 896:	c9                   	leave  
 897:	e9 24 ff ff ff       	jmp    7c0 <main@@Base+0x150>
 89c:	8b 14 24             	mov    edx,DWORD PTR [esp]
 89f:	c3                   	ret    
 8a0:	53                   	push   ebx
 8a1:	e8 ca fe ff ff       	call   770 <main@@Base+0x100>
 8a6:	81 c3 5a 17 00 00    	add    ebx,0x175a
 8ac:	83 ec 08             	sub    esp,0x8
 8af:	e8 2c fd ff ff       	call   5e0 <getegid@plt>
 8b4:	83 ec 04             	sub    esp,0x4
 8b7:	50                   	push   eax
 8b8:	50                   	push   eax
 8b9:	50                   	push   eax
 8ba:	e8 91 fd ff ff       	call   650 <setresgid@plt>
 8bf:	8d 83 00 ea ff ff    	lea    eax,[ebx-0x1600]
 8c5:	89 04 24             	mov    DWORD PTR [esp],eax
 8c8:	e8 33 fd ff ff       	call   600 <system@plt>
 8cd:	83 c4 18             	add    esp,0x18
 8d0:	5b                   	pop    ebx
 8d1:	c3                   	ret    
 8d2:	8d b4 26 00 00 00 00 	lea    esi,[esi+eiz*1+0x0]
 8d9:	8d bc 27 00 00 00 00 	lea    edi,[edi+eiz*1+0x0]
 8e0:	57                   	push   edi
 8e1:	56                   	push   esi
 8e2:	53                   	push   ebx
 8e3:	e8 88 fe ff ff       	call   770 <main@@Base+0x100>
 8e8:	81 c3 18 17 00 00    	add    ebx,0x1718
 8ee:	83 ec 0c             	sub    esp,0xc
 8f1:	8b b3 48 00 00 00    	mov    esi,DWORD PTR [ebx+0x48]
 8f7:	56                   	push   esi
 8f8:	e8 13 fd ff ff       	call   610 <strlen@plt>
 8fd:	89 34 24             	mov    DWORD PTR [esp],esi
 900:	89 c7                	mov    edi,eax
 902:	e8 29 fd ff ff       	call   630 <__strdup@plt>
 907:	89 c6                	mov    esi,eax
 909:	58                   	pop    eax
 90a:	5a                   	pop    edx
 90b:	57                   	push   edi
 90c:	56                   	push   esi
 90d:	e8 2e fd ff ff       	call   640 <memfrob@plt>
 912:	83 c4 10             	add    esp,0x10
 915:	89 f0                	mov    eax,esi
 917:	5b                   	pop    ebx
 918:	5e                   	pop    esi
 919:	5f                   	pop    edi
 91a:	c3                   	ret    
 91b:	90                   	nop
 91c:	8d 74 26 00          	lea    esi,[esi+eiz*1+0x0]
 



920:	57                   	push   edi                     ;fonction appelée par main
 921:	56                   	push   esi
 922:	53                   	push   ebx
 923:	e8 48 fe ff ff       	call   770 <main@@Base+0x100>
 928:	81 c3 d8 16 00 00    	add    ebx,0x16d8
 92e:	83 ec 0c             	sub    esp,0xc
 931:	8b b3 48 00 00 00    	mov    esi,DWORD PTR [ebx+0x48]
 937:	56                   	push   esi
 938:	e8 d3 fc ff ff       	call   610 <strlen@plt>


0x56555a68 : 4b 72 4b 5e 13 58 1e 1f 7f 5e 53 67 40 5d 1e 43   KrK^.X...^Sg@].C
0x56555a78 : 1f 7d 42 12 59 5d 7c 7d 47 6f 4d 19 5c 6b 48 7d   .}B.Y]|}GoM.\kH}
0x56555a88 : 70 4b 43 40 7e 7d 7a 12 00 00 00 00 01 1b 03 3b   pKC@.}z........;

 								; eax = 0x28 longueur de la chaine 




 93d:	89 34 24             	mov    DWORD PTR [esp],esi
 940:	89 c7                	mov    edi,eax
 942:	e8 e9 fc ff ff       	call   630 <__strdup@plt>      
                                                           ; eax contient addresse sur la chaine dupliquée 
 947:	89 c6                	mov    esi,eax     
 949:	58                   	pop    eax
 94a:	5a                   	pop    edx
 94b:	57                   	push   edi
 94c:	56                   	push   esi

Avant exécution de memfrob
0x56558980 : 4b 72 4b 5e 13 58 1e 1f 7f 5e 53 67 40 5d 1e 43   KrK^.X...^Sg@].C
0x56558990 : 1f 7d 42 12 59 5d 7c 7d 47 6f 4d 19 5c 6b 48 7d   .}B.Y]|}GoM.\kH}
0x565589a0 : 70 4b 43 40 7e 7d 7a 12 00                        pKC@.}z.


 94d:	e8 ee fc ff ff       	call   640 <memfrob@plt>     ; xor 0x2a sur chaque caractère de la chaine de longueur 0x28

Après exécution memfrob
0x56558980 : 61 58 61 74 39 72 34 35 55 74 79 4d 6a 77 34 69   aXat9r45UtyMjw4i
0x56558990 : 35 57 68 38 73 77 56 57 6d 45 67 33 76 41 62 57   5Wh8swVWmEg3vAbW
0x565589a0 : 5a 61 69 6a 54 57 50 38 00                        ZaijTWP8.




 952:	59                   	pop    ecx
 953:	5f                   	pop    edi
 954:	56                   	push   esi
 955:	ff 74 24 1c          	push   DWORD PTR [esp+0x1c]

Guessed arguments:
arg[0]: 0xffffd180 ("123456789abcdefg")
arg[1]: 0x56558980 ("aXat9r45UtyMjw4i5Wh8swVWmEg3vAbWZaijTWP8")


 959:	e8 32 fc ff ff       	call   590 <strcmp@plt>
 95e:	89 34 24             	mov    DWORD PTR [esp],esi
 961:	89 c7                	mov    edi,eax
 963:	e8 58 fc ff ff       	call   5c0 <free@plt>
 968:	83 c4 10             	add    esp,0x10
 96b:	89 f8                	mov    eax,edi
 96d:	5b                   	pop    ebx
 96e:	5e                   	pop    esi
 96f:	5f                   	pop    edi
 970:	c3                   	ret    
 


971:	66 90                	xchg   ax,ax
 973:	66 90                	xchg   ax,ax
 975:	66 90                	xchg   ax,ax
 977:	66 90                	xchg   ax,ax
 979:	66 90                	xchg   ax,ax
 97b:	66 90                	xchg   ax,ax
 97d:	66 90                	xchg   ax,ax
 97f:	90                   	nop
 980:	55                   	push   ebp
 981:	57                   	push   edi
 982:	56                   	push   esi
 983:	53                   	push   ebx
 984:	e8 e7 fd ff ff       	call   770 <main@@Base+0x100>
 989:	81 c3 77 16 00 00    	add    ebx,0x1677
 98f:	83 ec 0c             	sub    esp,0xc
 992:	8b 6c 24 20          	mov    ebp,DWORD PTR [esp+0x20]
 996:	8d b3 ec fe ff ff    	lea    esi,[ebx-0x114]
 99c:	e8 b3 fb ff ff       	call   554 <strcmp@plt-0x3c>
 9a1:	8d 83 e8 fe ff ff    	lea    eax,[ebx-0x118]
 9a7:	29 c6                	sub    esi,eax
 9a9:	c1 fe 02             	sar    esi,0x2
 9ac:	85 f6                	test   esi,esi
 9ae:	74 25                	je     9d5 <main@@Base+0x365>
 9b0:	31 ff                	xor    edi,edi
 9b2:	8d b6 00 00 00 00    	lea    esi,[esi+0x0]
 9b8:	83 ec 04             	sub    esp,0x4
 9bb:	ff 74 24 2c          	push   DWORD PTR [esp+0x2c]
 9bf:	ff 74 24 2c          	push   DWORD PTR [esp+0x2c]
 9c3:	55                   	push   ebp
 9c4:	ff 94 bb e8 fe ff ff 	call   DWORD PTR [ebx+edi*4-0x118]
 9cb:	83 c7 01             	add    edi,0x1
 9ce:	83 c4 10             	add    esp,0x10
 9d1:	39 fe                	cmp    esi,edi
 9d3:	75 e3                	jne    9b8 <main@@Base+0x348>
 9d5:	83 c4 0c             	add    esp,0xc
 9d8:	5b                   	pop    ebx
 9d9:	5e                   	pop    esi
 9da:	5f                   	pop    edi
 9db:	5d                   	pop    ebp
 9dc:	c3                   	ret    
 9dd:	8d 76 00             	lea    esi,[esi+0x0]
 9e0:	f3 c3                	repz ret 


####################################################################################################################

We can think that the key is  aXat9r45UtyMjw4i5Wh8swVWmEg3vAbWZaijTWP8

so let's try this in the shell :

[adversary ~/lockedout]$ ./lock
This is a pesky lock.. do you think you can open it?
Enter key: aXat9r45UtyMjw4i5Wh8swVWmEg3vAbWZaijTWP8
unlocked!
sh-4.4$

We obtain a shell , we just have to read the file flag.txt 

sh-4.4$ cat flag.txt
IceCTF{you_m3ddling_k1ds}
