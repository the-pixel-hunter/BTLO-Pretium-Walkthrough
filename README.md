# Pretium Walkthrough

### Scenario
- [ ] pic 1
### Question one 
What is the full filename of the initial payload file? (4 points)

Stright away we can some intrestin filenames which will remember for later as they may come into play.
- [ ] pic 2

But we can see one that was application/x-msdos-programs and its a bat file but trying to mascerade as .pdf file.
- [ ] pic3

 ANSWEAR: INVOICE_2021937.pdf.bat

### Question two
What is the name of the module used to serve the malicious payload? (4 points)

Taking a closer look at the packets we can see that the reposen contatins the server banner "SimpleHTTP/0.6 Python/3.8.5"
Quick little google to check the full module name fo SimpleHTTP provides us with our answear.
 - [ ] pic
ANSWEAR: SimpleHTTPServer

### Question Three 
From observing the traffic, can you find out what is the attacker machine IP now? (4 points)

This one isnt very hard, as it clearly displays the source addresses in the packets 
- [ ] pic4

ANSWEAR: 192.168.1.9

### Question Four
Now that you know the payload name and the module used to deliver the malicious files, what is the URL that was embedded in the malicious email? (5 points)

This one wasnt to hard just had to put together what we already know, but i was overthinking it at first :)
its all in the request...

ANSWEAR: http[:]//192.168.1.9:443/INVOICE_2021937.pdf.bat
*without out the "[" and "]"*

### Question Five
Find the PowerShell launcher string (you don’t need to include the base64 encoded script) (5 points)

Another one easily show in the HTTP Stream.

ANSWEAR: powershell -noP -sta -w 1 -enc

### Question 6
What is the default user agent being used for communications? (4 points)
 
i think you get the idea by now, in the streams we stay.

ANSWEAR: Mozilla/5.0

### Question 7 
You are seeing a lot of HTTP traffic, what is the name of a process where malware communicates with C2 server asking for instructions at set time intervals? (4 points)

This one was easy as it somthing i've been intrested in recently and detecting them there some call projects such as RITA by BHIS that detect becons 

ANSWEAR: Beaconing

### Question 8
What is the URI containing ‘login’ that the victim machine is communicating to? (5 points)

Looking in one the becaons HTTP streams we can find our answear
- [ ] pic
ANSWEAR / login/process.php


# Question 9

We know powershell was used and a little google migth give us some hints 

ANSWEAR: Empire

wYmshpXDmn-xh3bLxKNMIyDrCCdNO+vW6hh+ss=
ahKoQaRWLrGkKvQhZpDCyI1QF1E-
