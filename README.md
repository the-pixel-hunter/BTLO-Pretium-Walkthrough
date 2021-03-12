# BTLO: Pretium Walkthrough ![BTLO Logo](https://blueteamlabs.online/achievement/share/32/6)

### Scenario
![Scenario](https://github.com/the-pixel-hunter/BTLO-Pretium-Walkthrough/blob/main/images/PIC1.png)

<details><summary>Question 1</summary>
<p>

1. What is the full filename of the initial payload file? (4 points)

Lets check out export Objects in Wireshark

- [ ] pic  2

Stright away we can some intrestin filenames which will remember for later as they may come into play.

- [ ] pic 3

But we can see one that was application/x-msdos-programs and its a bat file but trying to mascerade as .pdf file.

- [ ] pic 4



ANSWEAR 1: INVOICE_2021937.pdf.bat

</p>
</details>

<details><summary>Question 2</summary>
<p>

2. What is the name of the module used to serve the malicious payload? (4 points)

Taking a closer look at the packets we can see that the reposen contatins the server banner "SimpleHTTP/0.6 Python/3.8.5"
Quick little google to check the full module name fo SimpleHTTP provides us with our answear.

- [ ] pic 5

ANSWEAR 2: SimpleHTTPServer
</p>
</details>

<details><summary>Question 3</summary>
<p>

3. From observing the traffic, can you find out what is the attacker machine IP now? (4 points)

This one isnt very hard, as it clearly displays the source addresses in the packets

- [ ] pic 6

ANSWEAR 3: 192.168.1.9

</p>
</details>
<details><summary>Question 4</summary>
<p>

4. Now that you know the payload name and the module used to deliver the malicious files, what is the URL that was embedded in the malicious email? (5 points)

This one wasnt to hard just had to put together what we already know, but i was overthinking it at first :)
its all in the requests... and just putting together what we already know really. 

- [ ] pic 7

ANSWEAR 4: http[:]//192.168.1.9:443/INVOICE_2021937.pdf.bat

*without out the "[" and "]"*
</p>
</details>

<details><summary>Question 5</summary>
<p>

5. Find the PowerShell launcher string (you don’t need to include the base64 encoded script) (5 points)

Another one easily show in the HTTP Stream.

- [ ] pic 8

ANSWEAR 5: powershell -noP -sta -w 1 -enc
</p>
</details>

<details><summary>Question 6</summary>
<p>

6. What is the default user agent being used for communications? (4 points)
 
I think you get the idea by now, in the streams we stay.

ANSWEAR 6: Mozilla/5.0
</p>
</details>

<details><summary>Question 7</summary>
<p>

7. You are seeing a lot of HTTP traffic, what is the name of a process where malware communicates with C2 server asking for instructions at set time intervals? (4 points

This one was easy as it something i've been intrested in recently and how to detect them there are projects such as RITA by BHIS that detect becons 

ANSWEA 7: Beaconing
</p>
</details>

<details><summary>Question 8</summary>
<p>
8. What is the URI containing ‘login’ that the victim machine is communicating to? (5 points)

Looking in one the becaons HTTP streams we can find our answear

- [ ] pic 9 

ANSWEAR 8: /login/process.php
</p>
</details>

<details><summary>Question 9</summary>
<p>
9. Can you name the post-exploitation framework used for C2 communication now to our victim machine? (5 points)

We know powershell was used and a little google fu gave me  some hints 

 - [ ] pic 10
 
ANSWEAR 9: Empire
</p>
</details>

<details><summary>Question 10 & 11</summary>
<p>

10. Using some Blue Team Magic, can detect data exfiltration and find out what have been exfiltrated? Provide the decoded password. (5 points)
11. What is the account’s username? (Include $ at the beginning) (5 points)

This one had me stumpted for a while but finaly filtering down the packets  did the trick and also the included resource was very helpful - https://isc.sans.edu/forums/diary/Packet+Tricks+with+xxd/10306/

1. Looking at the pcap, there seems to be a lot of ICMP traffic to the malciouse IP lets take a closer look with a filter 
`ip.dst == 192.168.1.8 and icmp`
3. Save that to a file
2. Lets export with Tshark
`cmd here`
3. Looks like hex let convert that
4. Looks like base64 lets convert that
5. just remove the "." and...
6. BINGO!

- [ ] pics 11 - 15

ANSWEAR 10: Y0uthinky0ucAnc4tchm3$$

ANSWEAR 11: $sec-account
</p>
</details>
