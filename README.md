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

We already have 2 important files called shadow and passwd. 

First we need to create a file from our passwd and shadow files. Here `mypasswd` is created.

> unshadow passwd shadow > mypasswd

Next use John to crack the password.

> john mypasswd

And the last step is to show what we've got.

> john --show mypasswd

![john1](https://i.imgur.com/gO9823R.png)

`john` is our username and `secret` is our password. Come get the flag!

![john2](https://i.imgur.com/zPHDsDc.png)

> HCMUS-CTF{Use_John_the_ripper_to_crack_password_is_fun!!!HAHAHA}



---

### 5. Factorization
**Point: 150 (16 solves)**

**Description:**
> RSA is weak if you use small prime :)

> Here is your ciphertext: 27039685590612119275089010235300223759019803357397398877100224864989993317282

> Link to files: shorturl.at/glJNQ

**Solution:**

We have the public key file, it means that we can get n and e because public key is formed by (n, e). Let's find out. 

![factor1](https://i.imgur.com/ogH2UhZ.png)

So, we have e = 65537 and n = 769a46997d37aefa6cad4cb8b9007de489a376218ad3a72498d427cf66a2a329 but in hex. After converting n to dec, we have: 

e = 65537, 

n = 53645497841104363753713788673417879039272642720860679513927265402830022943529 

and c = 27039685590612119275089010235300223759019803357397398877100224864989993317282.

In this step, we use a tool named RsaCtfTool (https://github.com/Ganapati/RsaCtfTool) to get the decrypted message as follows:

![factor2](https://i.imgur.com/lQNKxW6.png)

> HCMUS-CTF{smaLL_NumbeR}

---

### 6. Xor
**Point: 100 (21 solves)**

**Description:**
> I have used XOR to encrypt the message! Oh, it's cool. Unfortunately, I lost my key. But why do I need to remember the key when I know something in plaintext? meh

> e0a19131a79051d123d113b14166535163519023d280d0b290f0b053b2d363d3b3b

**Solution:**

For a XOR problem, we must know that XOR is reversible. That is, if I have a message M and XOR it with key K of the same length, then if I XOR it again with K, I will meet my original message again.

Now let's glance at the encrypted message. It has 63 characters so we must add 0 to the beginning so that the string has full of 64 characters.

Additionally, we know for sure that the message contains "HCMUS-CTF{" which is converted to hex as 48434d55532d4354467b. But its length is just 20 characters, we paste those characters for multiple times so that the total length reaches 64. The reason is that we have to XOR strings at the same length.

After that, we get the result of the encrypted message and "HCMUS-CTF{" using XOR tool as below. Here I use http://xor.pw/.

![xor1](https://i.imgur.com/Ib7Rv5S.png)

Let's look at the result, we notice that the string "464954" is duplicated. We copy and paste it multiple times so that it creates a string with the length of 64 characters. Then XOR the created string with our encrypted message.

The last step, we convert the hex string from the result of previous step to text and here the flag! Do not forget to put the number 0 in the beginning of our hex string.

> HCMUS-CTF{XoR_1s_a_KinD_oF_Crypto}

---

### 7. smalleeeee
**Point: 200 (8 solves)**

**Description:**
> I know you've mastered RSA. You know the way to encrypt the password with RSA right?. I just add a little step to spice up a password with XOR before it comes to RSA...

> It seems the public key of RSA has some weaknesses...

> Link to files: shorturl.at/NWX13


**Solution:**

This challenge is definitely the same with the challenge "Lowe" of CSAW CTF Qualification Round 2018. We follow the write-up of author  Aurel300 / EmpireCTF with a little bit of alternative to solve this problem. 

Link to that write-up: shorturl.at/cvWXZ

First, we get to know what is inside 3 given files. 

xorkey is the key to XOR for sure. publickey.pem contains publickey so we can get n and e from this. The last thing we need is the ciphered text, it must be included in key.enc.

Let's look at those files.

![smallee1](https://i.imgur.com/OSmPo6x.png)

Here we get:

e = 3

n = 0x00804d98aa1be38a44115931269f797b3679664b0d20aff442f4e81218d4d4976fd6bf893cd0b9e94b5499185f7164b15fcc7a767e1b908c892d7d3b62fdb133287e81df2356310e4795e1ffcf685535bf84b92b3f90110ccae27d0942538b6fccdf3b96a94e10949a6ecaa4bf1defdd45bc280c9cc4fc81e590e4356d96f8811fd42a34417b7a3db89bded031f45e615c9daa12e5f205529b2626421e689dc554283d123d7364c1b71888ff83f729627c6a95897d

c = 6227082212413071652031759584730136448940165739291015989123516964411792746722267675247227724887585971077473623502069408108397182867056358011324737255036470076968497104976179970504316493984084823513272328273178698410453586046435106124192879755925086697410678063206954537576840291931235923253224378643489372549097623686875168982132714146762501475508253685689577061107017695390392113755764763126416817697677280130139551135800363337551643

We just have to follow the above write-up for the rest of our solution:

![smallee2](https://i.imgur.com/H533ohe.png)

> HCMUS-CTF{hello_from_the_other_sidezzzzzzzzzzzzzzzzzzzzzzzz}

## Pwn
### 1. TellMe
**Point: 50 (45 solves)**

**Description:**
> Hey! I think you should log in to this portal =D

> nc 159.65.13.76 33100

> Link to file: shorturl.at/wGQU2

**Solution:**

First, let's check out what's inside "nc 159.65.13.76 33100". It is a log in screen.

![tellme1](https://i.imgur.com/SRd2m3o.png)

It requires userID to log in, so we trace back to the C file to see what we can get from there.

```C

#include <stdio.h>
#include <stdlib.h>
#include <string.h>


int main(){
	int userid;
	char passwd[32];


	fflush(stdin);
	fflush(stdout);
	printf("Hi there, please login!");
	printf("\nYour UserID: ");
	
	fflush(stdout);
 	fflush(stdin);
	scanf("%d", &userid);
	printf("\nPassword: ");
	
	fflush(stdout);
 	fflush(stdin);
	
	getchar();
	fgets(passwd, 32, stdin);
	fflush(stdout);
 	fflush(stdin);

	if(userid == 0x3211 && !strcmp("sUpErPassHCMUS\n", passwd)){
		printf("Wellcome back! Aministrator ^_^\n");
		fflush(stdout);
		fflush(stdin);
		system("/bin/cat flag");
		exit(0);
		
	}

	printf("Hey!! Who are you???\n");
	
	fflush(stdout);
 	fflush(stdin);
	return 0;

}

```

From the code, we can get right away the userid is `0x3211` and password is `sUpErPassHCMUS`. Notice that the userid is integer so remember to convert it before logging in. 

Here we go!!

![tellme2](https://i.imgur.com/sCnclTx.png)

> HCMUS-CTF{Ohhh~Just_give_me_the_credential!!Nah}

## Forensics
### 1. Docker Babe
**Point: 100 (18 solves)**

**Description:**
> Ahhhhhhhh! I have a docker, I have an image... Ahhhhhhhhhhhhhhhhhh! Flagggggggggggggggggggg =]]]]]

> Anyway, your image: https://hub.docker.com/r/pakkunandy/docker-babe

**Solution:**

The description says it all, we to inspect the Docker image from the given link.

First, before pulling the image, we must change the permissions of docker socket to be able to connect to the docker daemon.

> sudo chmod 666 /var/run/docker.sock

> docker pull pakkunandy/docker-babe

Let's see the image list in the docker.

> docker images

![docker1](https://i.imgur.com/KkEQSnQ.png)

As we can see, our image named pakkunandy/docker-babe has the ID of 6079d3143077

After that, we start the docker image pakkunandy/docker-babe:

![docker2](https://i.imgur.com/XWSZpIH.png)

Verify the new Docker container is running:

![docker3](https://i.imgur.com/BPJYkDa.png)

Docker run container:

![docker4](https://i.imgur.com/ONa5O1w.png)

Well we see something similar here ~ Flag.txt! It must contain what we're looking for!

![docker5](https://i.imgur.com/Gj5mtJT.png)

Here comes the flag!

> HCMUS-CTF{Docker_Is_an_essential_tool_You_have_to_learn_FORRRRSURRREEEE}






