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
pass: xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq

---
## Bandit 4

```shell
cat ./-file07
```
pass: 6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG

___
## Bandit 5

```shell
find . -size 1033c
cat ./maybehere07/.file2
```
pass: pXa26xhMWaC2SvDotA4r9EgZkulOeSBW

___
## bandit 6

```shell
find / -size 33c -group bandit6 -user bandit7 2> /dev/null
cat /var/lib/dpkg/info/bandit7.password
```
pass: Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3

___
## bandit 7

```shell
grep "millionth" data.txt
```
pass: VR1ljMayciFxbnUokuQmJFw6QC9VKtub

## bandit 8

```shell
sort data.txt | uniq -u
```
pass: EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl

___
## bandit 9

```shell
strings data.txt | grep "="
```
pass: B0s2khmbT9u0geKuOoVGW3JZKhndE3BG

___
## bandit 10

```shell
base64 -d data.txt
```
pass: pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro

___
## bandit 11

```shell
cat data.txt | tr 'a-z' 'n-za-m' | tr 'A-Z' 'N-ZA-M'
```
pass: GROozWPO8QyN0mGrjUkID0WCYkZiQxrN

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
pass: qQYQiHOBPR8zR61qxYqX45quvihF2uzk

___
## bandit 13
no pass just get private key and use it for 14
```shell
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
```
pass: use downloaded ssh key.

___
## bandit 14
> [!note]
> - don't make key accessible to other users via `chmod o= key.private` and `chmod g= key.private`
> - add key to ssh via `ssh -i key.private`

```bash
cat /etc/bandit_pass/bandit14 # pass: aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
echo "aaWecNkG4FhxJQxz07uiwzVP6bJiYS65" | nc localhost 30000 -t
```
pass: pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7

___
## bandit 15

```bash
openssl s_client localhost:30001 # after connect paste pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7 then enter
```

to initialize the connection
then paste the previous pass and hit enter.

pass: kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V

___
## bandit 16

```shell
nmap -sC -p 31000-32000 localhost
```

Scan for open ports. Two of them have ssl/tls connections for connecting

```shell
echo "kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V" | openssl s_client -connect localhost:31790 -quiet
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
