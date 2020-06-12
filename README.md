# HCMUS-CTF 2020 WARM-UP
### Team: paddingsugar
### Author: QT23

## Cryptography
### 1. Decoder
**Point: 50 (52 solves)**

**Description:**
> I think the decoder is an essential technique you need to know. 
>
SSB0aGluayB0aGUgZmxhZyBpcyBlbmNvZGVkIGluIGJhc2UoNjQvMik6IEpCQlUyVktURlZCVklSVDNOSktYRzVDN0tOVVcyNERNSVZQVUlaTERONVNHSzRUNQ==


**Solution:**

The name of this challenge is `decoder` so I guess we must use a decoder!

The `==` on the end is a tell-tale sign of the value being base64 encoded. Thus, we just use the base64 decoder and here is the result:
> I think the flag is encoded in base(64/2): JBBU2VKTFVBVIRT3NJKXG5C7KNUW24DMIVPUIZLDN5SGK4T5

The result tells us that the flag is encoded in base(64/2) = base32, so let's continue to use the base32 decoder then we are saluted with the flag!
> HCMUS-CTF{jUst_SimplE_Decoder} 

---

### 2. Dot and Underscore
**Point: 50 (53 solves)**

**Description:**
> It's extremely easy :) Remember put the content inside HCMUS-CTF{...}

> When you were young, I think you knew this one: .. - ... --. --- --- -.. - --- .-.. . .- .-. -. -- --- .-. ... . -.-. --- -.. .

**Solution:**

It is definitely the Morse code at the first glance. If you are not familiar with this, just google for dot and underscore.

So the job is easy now, just use a Morse code translator and get the flag!

> HCMUS-CTF{ITSGOODTOLEARNMORSECODE}

---

### 3. sub
**Point: 50 (46 solves)**

**Description:**
> I think you should read that report in a different way :)

> And a file called sub (shorturl.at/eimo7).

**Solution:**

First, let's see what is inside the given file.

![sub](https://i.imgur.com/5e6KEed.png)

The file includes ASCII text so we must think of cipher. Additionally, the challenge's title is sub so I guess it might be substitution cipher. 

Try using a substitution cipher decoder to get the flag. Here I use https://www.guballa.de/substitution-solver for solving the cipher.

> HCMUS-CTF{YOU_SHOULD_LEARN_A_BIT_HISTORY_OF_FIT}

---

### 4. The Ripper
**Point: 100 (27 solves)**

**Description:**
> If you use linux, you should know two important files :) Can you crack it! John can help you a hand...

> nc 159.65.13.76 33001

> Link to files: shorturl.at/iotU5

**Solution:**

John? The Ripper? It must be John The Ripper - a password cracking tool. If you haven't heard about it, you are free to google it. 

---

### 5. Factorization
**Point: 150 (16 solves)**

**Description:**
> RSA is weak if you use small prime :)

> Here is your ciphertext: 27039685590612119275089010235300223759019803357397398877100224864989993317282

> Link to files: shorturl.at/glJNQ

**Solution:**

We have the public key file, it means that we can get n and e because public key is formed by (n, e). Let's find out. 





