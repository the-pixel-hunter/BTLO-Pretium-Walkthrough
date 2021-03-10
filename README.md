# BTLO: Pretium Walkthrough ![BTLO Logo](https://github.com/the-pixel-hunter/BTLO-Pretium-Walkthrough/blob/main/images/btlologo.png)

### Scenario
- [ ] pic 1

<details><summary>Question 1</summary>
<p>

What is the full filename of the initial payload file? (4 points)

Lets check out export Objects in Wireshark

- [ ] pic  2

Stright away we can some intrestin filenames which will remember for later as they may come into play.

- [ ] pic 3

But we can see one that was application/x-msdos-programs and its a bat file but trying to mascerade as .pdf file.

- [ ] pic 4



ANSWEAR: INVOICE_2021937.pdf.bat

</p>
</details>

### Question 2
What is the name of the module used to serve the malicious payload? (4 points)

Taking a closer look at the packets we can see that the reposen contatins the server banner "SimpleHTTP/0.6 Python/3.8.5"
Quick little google to check the full module name fo SimpleHTTP provides us with our answear.

- [ ] pic 5

ANSWEAR 2: SimpleHTTPServer

### Question 3 
From observing the traffic, can you find out what is the attacker machine IP now? (4 points)

This one isnt very hard, as it clearly displays the source addresses in the packets

- [ ] pic 6

ANSWEAR 3: 192.168.1.9

### Question 4
Now that you know the payload name and the module used to deliver the malicious files, what is the URL that was embedded in the malicious email? (5 points)

This one wasnt to hard just had to put together what we already know, but i was overthinking it at first :)
its all in the requests... and just putting together what we already know really. 

- [ ] pic 7

ANSWEAR 4: http[:]//192.168.1.9:443/INVOICE_2021937.pdf.bat

*without out the "[" and "]"*

### Question 5
Find the PowerShell launcher string (you don’t need to include the base64 encoded script) (5 points)

Another one easily show in the HTTP Stream.

- [ ] pic 8

ANSWEAR 5: powershell -noP -sta -w 1 -enc

### Question 6
What is the default user agent being used for communications? (4 points)
 
I think you get the idea by now, in the streams we stay.

ANSWEAR 6: Mozilla/5.0

### Question 7 
You are seeing a lot of HTTP traffic, what is the name of a process where malware communicates with C2 server asking for instructions at set time intervals? (4 points

This one was easy as it something i've been intrested in recently and how to detect them there are projects such as RITA by BHIS that detect becons 

ANSWEA 7: Beaconing

### Question 8
What is the URI containing ‘login’ that the victim machine is communicating to? (5 points)

Looking in one the becaons HTTP streams we can find our answear

- [ ] pic 9 

ANSWEAR 8: /login/process.php


### Question 9

We know powershell was used and a little google fu gave me  some hints 

 - [ ] pic 10
 
ANSWEAR 9: Empire

### Question 10 & 11

10. Using some Blue Team Magic, can detect data exfiltration and find out what have been exfiltrated? Provide the decoded password. (5 points)
11. What is the account’s username? (Include $ at the beginning) (5 points)

This one had me stumpted for a while but finaly filtering down the packets  did the trick and also the included resource was very helpful - https://isc.sans.edu/forums/diary/Packet+Tricks+with+xxd/10306/

1. Looking at the pcap, there seems to be a lot of ICMP traffic to the malciouse IP lets take a closer look with a filter 
`ip.dst == 192.168.1.8 and icmp`
2. lets export the data filed with tshark 
`cmd here`
3. Looks like hex let conver that
4. Looks like some lovely bit of base64 
5. BINGO!

- [ ] pics 11 - 15

ANSWEAR 10: Y0uthinky0ucAnc4tchm3$$

ANSWEAR 11: $sec-account

### Final Thoughts

Enjoyed this one! stuggled at first with the final two questiosn but having sleep and coming back at it with a fresh mind works wonders!

