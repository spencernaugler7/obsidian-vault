---
source: https://overthewire.org/wargames/bandit
tags:
---
## Bandit 0
login

```shell
ssh -p 2220 bandit0@bandit.labs.overthewire.org # pass: bandit0
```
pass: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR

---
## Bandit 1
command to solve

```shell
cat ./-
```
pass: PK8fYLZg2hnHSz83plBL1iEPKdD3QToB

---
## Bandit 2

```shell
cat ./'--spaces in this filename--'
```
pass: 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME

---
## Bandit 3

```shell
cd inhere
cat '...Hiding-From-You'
```
pass: 

---
## Bandit 4

```shell
cat ./-file07
```
pass: 

___
## Bandit 5

```shell
find . -size 1033c
cat ./maybehere07/.file2
```
pass: 

___
## bandit 6

```shell
find / -size 33c -group bandit6 -user bandit7 2> /dev/null
cat /var/lib/dpkg/info/bandit7.password
```
pass: 

___
## bandit 7

```shell
grep "millionth" data.txt
```
pass: 

## bandit 8

```shell
sort data.txt | uniq -u
```
pass: 

___
## bandit 9

```shell
strings data.txt | grep "="
```
pass: 

___
## bandit 10

```shell
base64 -d data.txt
```
pass: 

___
## bandit 11

```shell
cat data.txt | tr 'a-z' 'n-za-m' | tr 'A-Z' 'N-ZA-M'
```
pass: 

___
## bandit 12

```shell
cat data.txt | xxd -r > archive.gz
gzip -d archive.gz
mv archive archive.bz2
bzip2 -d archive.bz2
mv archive archive.tar
tar xf archive.tar
// repeat several times check teh file with the "file" command
```
pass: 

___
## bandit 13
no pass just get private key and use it for 14

```shell
cat /etc/bandit_pass/bandit14
```
pass: 

___
## bandit 14

```shell
echo "MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS" | nc localhost 30000 -t
```
pass: 

___
## bandit 15

```shell
openssl s_client localhost:30001
```

to initialize the connection
then paste the previous pass and hit enter.

pass: 

___
## bandit 16

```shell
nmap -sC -p 31000-32000 localhost
```

Scan for open ports. Two of them have ssl/tls connections for connecting

```shell
echo "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx" | openssl s_client -connect localhost:31790 -quiet
```

Initially tried the solution to bandit 15. connect to the server, paste the pass, hit enter. This would only result in a "keyupdate" message showing up in the output instead of the puzzle solution.

This happens due to openssl s_client's command interface. if you type "k" while connected to the server it initializes a key refresh, hence the "keyupdate" message.
the server still sent a response it is just covered up by the keyupdate. solution: pass the input through stdin to disable keyboard input. also add `-quiet` to disable the "keyupdate" message.

no pass private key used

___
## bandit 17

```shell
diff passwords.old passwords.new
```
pass: 

___
## bandit 18

```shell
ssh -p 2220 bandit18@bandit.labs.overthewire.org /bin/bash --norc
cat readme
```
pass: 

___
## bandit 19

```shell
./bandit20-do cat /etc/bandit_pass/bandit20
```
pass: 

___
## bandit 20

```shell

```

pass: 
