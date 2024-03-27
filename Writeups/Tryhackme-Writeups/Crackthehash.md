# Crack the Hash. 🕵️‍♂️💻

  
Uncover the secrets of various hash algorithms, from MD5 to SHA-256, and learn the art of cracking them using the Hashcat tool.
Tools Used: Hashcat, hashid, hash-identifier  
#### Links: 
- https://www.stationx.net/how-to-use-hashcat/
- https://hashcat.net/wiki/doku.php?id=example_hashes 






## Part 1:

#### 1.48bb6e862e54f2a795ffc4e541caed4d 

- The first step, find out what kind of hash this is

```bash
  hashid-m 'filename'
```
![App Screenshot](https://miro.medium.com/v2/resize:fit:640/format:webp/1*hFON28fehvZuMfNZTma_fw.png) 

- Use hash-identifier just to be sure

![App Screenshot](https://miro.medium.com/v2/resize:fit:720/format:webp/1*b_9IhG9_oNc-Zq4ibRBEMg.png) 

- Both say it could be MD5 

#### Hint: hashid -m tells you the hashcat extension

Command:
```bash
hashcat -m 0 hash1.1 /usr/share/seclists/Passwords/Leaked-Databases/rockyou.txt
```
![App Screenshot](https://miro.medium.com/v2/resize:fit:720/format:webp/1*x6It5Y8wsmc4INQRMsO4mg.png) 

#### 2.CBFDAC6008F9CAB4083784CBD1874F76618D2A97
- Same process as before, use both hashid-m and hash-identifier

- We find out the hash is SHA-1 

Command:
```bash
hashcat -m 100 hash1.2 /usr/share/seclists/Passwords/Leaked-Databases/rockyou.txt
```

![App Screenshot](https://miro.medium.com/v2/resize:fit:720/format:webp/1*5e6ERpGCRyfjJZXqD2JEsQ.png) 

#### 3.1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032

- Hashid-m and hash-identifier both indicate that this is a SHA-256 hash 

Command:
```bash
hashcat -m 1400 hash1.3 /usr/share/seclists/Passwords/Leaked-Databases/rockyou.txt
```   

![App Screenshot](https://miro.medium.com/v2/resize:fit:720/format:webp/1*nuQncFK2zPqNxdroBpCRJA.png)

#### 4.$2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom 

- Hash-identifier cam up with nothing and hashid -m said it could either be blowfish(openbsd) or bcrypt, both have the same extension 

#### hint: it says that the cracked hash is 4 characters long 
- danielmiessler’s “SecLists”: (You can find on github @ https://github.com/danielmiessler/SecLists ) 
- there is a wordlist called 1–4_all_letters_a-z.txt, running this takes significantly less time
- Use the command: 

```bash
grep -E ‘^[a-zA-Z]{4}$’ /usr/shares/seclists/Fuzzing/1–4_all_letters_a-z.txt > filteredwords.txt
``` 
- limits it to just to the words containg 4 characters

- Now run the command: 

```bash
hashcat -m 3200 hash1.4 filteredwords.txt
``` 

![App Screenshot](https://miro.medium.com/v2/resize:fit:640/format:webp/1*LWp2B63zcIl-iLF2_9VRNw.png) 

![App Screenshot](https://miro.medium.com/v2/resize:fit:720/format:webp/1*QbbAeJ50WbZs0XEkSH44Rw.png)

#### 5.279412f945939ba78ce0758d3fd83daa 

- MD4 hash 

- Used Crackstation to crack this one 


![App Screenshot](https://miro.medium.com/v2/resize:fit:720/format:webp/1*d95ZNrmUtETuC6fITzJF3Q.png)


## Part 2:

#### 1.F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85 

- Hash is SHA-256   

Command:

```bash
hashcat -m 1400 hash2.1 /usr/share/seclists/Passwords/Leaked-Databases/rockyou.txt
```  

![App Screenshot](https://miro.medium.com/v2/resize:fit:720/format:webp/1*NySrmjlcxT5LyDntiKpq6Q.png) 

#### 2.1DFECA0C002AE40B8619ECF94819CC1B 

- Hint says that it is an NTLM hash 

Command: 

```bash
hashcat -m 1000 hash2.2 /usr/share/seclists/Passwords/Leaked-Databases/rockyou.txt
```  

![App Screenshot](https://miro.medium.com/v2/resize:fit:720/format:webp/1*ArY74ziqFKQT4OC50krGVA.png) 

#### 3.$6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02.

- Hashid -m says it is a SHA-512 Crypt 
#### Hint: Use hashcat wiki for example hashes 

Command: 

```bash
hashcat -m 1800 hash2.3 /usr/share/seclists/Passwords/Leaked-Databases/rockyou.txt
```  

![App Screenshot](https://miro.medium.com/v2/resize:fit:720/format:webp/1*RNRUaqxWh2VHj-_e_FHLwQ.png) 

![App Screenshot](https://miro.medium.com/v2/resize:fit:720/format:webp/1*oyFjbzET70yIqbua5yveNg.png)

#### 4.e5d8870e5bdd26602cab8dbe07a942c8669e56d6 Salt: tryhackme 

#### Hint: The salt isn’t included in the hash already as it was in the previous problem

- This is the format to use when placing in txt file:
```bash 
e5d8870e5bdd26602cab8dbe07a942c8669e56d6:tryhackme
```  

- HMAC-SHA1 (key = $salt) - hashcat wiki for example hashes 


Command: 

```bash
hashcat -m 160 hash2.4 /usr/share/seclists/Passwords/Leaked-Databases/rockyou.txt
```  

![App Screenshot](https://miro.medium.com/v2/resize:fit:720/format:webp/1*aInGoaFVMNkTAaHFA0s3Ww.png)
